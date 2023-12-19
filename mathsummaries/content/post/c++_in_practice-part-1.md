---
title: "C++ Refresher - Part 1"
date: 2023-12-18T13:02:33+01:00
math: katex
tags: ["C++"]
categories: ["C++"]
---

### Hazards of dynamic memory allocation.

#### Dangling pointers and multiple deallocations.

A *dangling pointer* is a pointer variable that still contains the address to the free store memory that has already been deallocated using `delete` or `delete[]`. Dereferencing a dangling pointer makes you read from, or even worse write to memory that might already be allocated to and used by other parts of the program, resulting in all kinds of unpredictable results. 

Multiple deallocations which occur when you deallocate an already deallocated memory (and hence dangling) pointer for a second time is a recipe for disaster.

One basic strategy to guard yourself against dangling pointers is to always reset a pointer to `nullptr`, after the memory it points to is released. However, in more complex programs, different parts of the code often collaborate by accessing the same memory - an object or an array of objects - all through distinct copies of the same pointer. In such cases, our simple strategy falls short. Which part of the code is going to call `delete`/`delete[]`? And when? How do you ensure that no other part of the code is still using the same dynamically allocated memory.

#### Allocation/Deallocation mismatch.

A dynamically allocated array, allocated using `new[]`, is captured in a regular pointer cariable. But, so is a single allocated value that is allocated using `new`.

```cpp
double* single_df {new double {0.95}};
double* array_of_dfs {new double[3] {1.00, 0.95, 0.90}};
```

After this the compiler has no way to distinguish between the two, especially once such a pointer gets passed around different parts of the program. This means that the following two statements will compile without error.

```cpp
delete[] single_df;
delete array_of_dfs;
```

Every `new` must be paired with a single `delete`; every `new[]` must be paired with a single `delete[]`.

#### Memory Leaks.

A memory leak occurs when you allocate memory using `new` or `new[]` and fail to release it. If you lose the address of free store memory you have allocated by overwriting the address in the pointer you were using to access it, for instance, you have a memory leak. 

When it comes to scope, pointers are just like any other variable. The lifetime of a pointer extends from the point at which you define it in a block to the closing brace of the block. After that it no longer exists, the free store goes out of scope and it's no longer possible to delete the memory. 

It's still relatively easy to see, where you've simply forgotten to use `delete` to free memory when use of the memory ceases at a point close to where you allocated it, but you'd be surprised how often programmers make mistakes like this, especially if, for instance, `return` statements creep in between allocation and deallocation of your variable. And naturally, memory leaks are even more difficult to spot in complex programs, where memory may be allocated in part of the the program and should be released in a completely separate part.

One basic strategy for avoiding memory leaks is to immediately add `delete` operation at an appropriate place each time you use the `new` operator. But this strategy by no means is fail-safe. Even C++ programmers are fallible creatures.

#### Fragmentation of the Free-Store.

Memory fragmentation can arise in programs that frequently dynamically allocate and release memory blocks. Each time, the `new` operator is used, it allocates a contiguous block of bytes. If you create and destroy many memory blocks of different sizes, it's possible to arrive at a situation in which the allocated memory is interspersed with small blocks of free memory, non of which is large enough to accomodate a new memory allocation request by your program. The aggregate of the free memory can be quite largbe, but if all the individual blocks are small (smaller than a current allocation request), the allocation request will fail.

### Golden rule of dynamic memory allocation.

Never use the operators `new`, `new[]`, `delete` and `delete[]` directly in day-to-day coding. These operators have no place in modern C++ code. Always use either the `std::vector<T>` container to replace dynamic arrays or a smart pointer to dynamically allocate individual objects and manage their lifetimes. 

## Raw pointers and Smart Pointers.

Pointer types `int*`, `double*` are referred to as *raw pointers* because variables of these types contain nothing more than an address. A raw pointer can store the address of an automatic variable or a memory-block allocated in the free-store. 

A *smart pointer* is an object that mimics a raw pointer in that, it contains an address, and you can use it in the same way in many respects. Smart pointers are normally used only to store the address of memory allocated in the free store. A smart pointer does much more than a raw pointer, though. The most notable feature of a smart pointer, is that we don't have to worry about using the `delete` or `delete[]` operator to free memory. It will be released automatically, when it is no longer needed. This means that multiple allocations, allocation/deallocation mismatches and memory leaks will no longer be possible. 

- A `std::unique_ptr<T>` object behaves as a pointer to type `T` and is unique in the sense that there can be only one single `unique_ptr<>` object containing the same address. In other words, there can never be two or more `unique_ptr<T>` objects pointing to the same memory address at the same time. A `unique_ptr<>` object is said to own the object it points to exclusively. The uniqueness is enforced by the fact, that a compiler will never allow you to copy a `unique_ptr<>`.

- A `std::shared_ptr<T>` object also behaves as a pointer to type `T`, but in contrast with `unique_ptr<T>` there can be any number of `shared_ptr<>` objects that allow *shared ownership* of an object in the free-store. At any given moment, the number of `shared_ptr<>` objects that contain a given address in time is known by the runtime. This is called *reference counting*. The reference count for a `shared_ptr<>` containing a given free store address is incremented each time a new `shared_ptr` object is creating containing that address, and its decremented when a `shared_ptr` containing the address is destroyed or assigned to point to a different address. When there are no `shared_ptr` objects containing a given address, the reference count will have dropped to zero, and the memory for the object at that address is released automatically. All `shared_ptr<>` objects that point to the same address have access to the the count of how many there are.

- A `weak_ptr<T>` is linked to a `shared_ptr<T>` and contains the same address. Creating a `weak_ptr<>` does not increment the reference count associated with the linked `shared_ptr<>` object, though, so a `weak_ptr<>` does not prevent the object pointered to from being destroyed. Its memory will still be released when the last `shared_ptr<>` referencing it is destroyed or reassigned to point to a different address, even when associated `weak_ptr<>` objects still exist. If this happens, the `weak_ptr<>` will nevertheless not contain a dangling pointer, atleast not one that you could inadvertently access. The reason is that you cannot access the address encapsulated by a `weak_ptr<T>` directly. The compiler forces you to first create a `shared_ptr<T>` object out of it that refers to the same address. If the memory address for the `weak_ptr<>` is still valid, forcing you to create a `shared_ptr<>` first ensures that the reference count is again incremented and that the pointer can be used safely again. If the memory is released already, however, this operation will result in a `shared_ptr<>1` containing a `nullptr`.

One use for having `weak_ptr<>` objects is to avoid so called reference cycles with `shared_ptr<>` objects. Conceptually, a reference cycle is where a `shared_ptr<Y>` inside the object `x` points to some other object `y` that contains a `shared_ptr<X>`, which points back to `x`. With this situation, neither `x` nor `y` can be destroyed. In practice, this may occur in many ways. `weak_ptr` allows you to break such cycles. Another use of weak pointers is in the implementation of object caches. 

### Using `unique_ptr<T>` and `shared_ptr<T>` pointers.

A `unique_ptr<T>` object stores an address uniquely, so the value to which it points is owned exlusively by the `unique_ptr<T>` smart pointer. When the `unique_ptr<T>` is destroyed, so is the value to which it points. Like all smart pointers, a `unique_ptr<>` is most useful when working with dynamically allocated objects. Objects then should not be shared by multiple parts of the program, or where the lifetime of the dynamic pobject is naturally tied to a single other object in your program. 

One common use for a `unique_ptr<>` is to hold something called a *polymorphic pointer*, which in essence is a pointer to a dynamically allocated object that can be of any number of related class types.

To create and initialize a double variable on the free-store, we write:

```cpp
#include <iostream>
#include <memory>

int main()
{
    std::unique_ptr<double> pDiscountFactor {std::make_unique<double>(0.95)};
    
    std::cout << "Discount Factor = " << *pDiscountFactor;
    
    return 0;
}
```

```
Discount Factor = 0.95
```

The memory allocated on the free store holding `0.95` is released once `pDiscountFactor` goes out of scope and is destroyed after the `return` statement.

The below code snippet shows how smart pointers work.

```cpp
#include <iostream>
#include <memory>

class X{
    public:
        X()
        {
          std::cout << "\nX created";
        }
        
        ~X()
        {
          std::cout << "\nX destroyed";
        }
};

class Y{
    
    public:
        Y()
        {
          std::cout << "\nY created";
        }
        
        ~Y()
        {
          std::cout << "\nY destroyed";
        } 
};

int main()
{
    std::cout << "\nInside main";
    std::shared_ptr<Y> sPtrY1 {std::make_shared<Y>()};
    
    
    {
        //inner scope
        std::cout << "\nInside inner";
        
        std::unique_ptr<X> uPtrX1 {std::make_unique<X>()};
        std::shared_ptr<Y> sPtrY2 {sPtrY1};
        
        // copy assignment and copy construction is not allowed on unique_ptr objects
        //std::unique_ptr<X> uPtrX2 = uPtrX1;
        
        std::cout << "\nExiting inner";
    }
    
    std::cout << "\nExiting main";
    return 0;
}
```

```
Inside main
Y created
Inside inner
X created
Exiting inner
X destroyed
Exiting main
Y destroyed
```

## References.

A reference is a name that you can use as an alias for another variable. Unlike a pointer, you cannot declare a reference and not initialize it. Because a reference is an alias, the variable which it is an alias must be provided when the reference is initialized. Also, a reference cannot be modified to be an alias for something else.

```cpp
#include <iostream>
#include <memory>


void swap(int& a, int& b)
{
    int temp {a};
    a = b;
    b = temp;
}

int main()
{
    int x {10}; 
    int y {15};
    
    std::cout << "\n Before swap:";
    std::cout << "\n x = " << x ;
    std::cout << "\n y = " << y;
    
    swap(x,y);
    
    std::cout << "\n After swap:";
    std::cout << "\n x = " << x ;
    std::cout << "\n y = " << y;
    return 0;
}
```

```
 Before swap:
 x = 10
 y = 15
 After swap:
 x = 15
 y = 10
 ```
 
Never return a pointer or reference to an automatic stack-allocated local variable from within a function. Automatic variables are destroyed and the stack is popped, once the control goes outside the scope in which they are declared.

## Function Templates.

A function template itself is not a definition of a function; it is a blueprint or a recipe for definining an entire family of functions. A function template is a parametric function definition, where a particular function instance is created by one or more parameter values. The compiler uses a function template to generate a function definition when necessary. If it is never necessary, no code results from the template. A function definition that is generated from a template is an *instance* or *instantiation* of the template. 

The parameters of a function template are usually data-types, where an instance can be generated for a parameter value of type `int`, for example, and another with parameter valuer of type `string`. But parameters are not necessarily types. They can be other things such as a dimension, for example. 

```cpp
template <class T>
T larger(T a, T b)
{
    return a > b ? a : b;
}
```

The compiler creates instances of the template from any statement that uses the `larger()` function. Here's an example:

```cpp
int main()
{
    std::cout << "\nLarger of 1.50 and 2.50 is : "  << larger(1.5,2.5);
    return 0;
}
```

```
Larger of 1.50 and 2.50 is : 2.5
```

You just use the function in the normal way. You don't need to specify a value for the template parameter `T`. The compiler deduces the type that is to replace `T` from the arguments in the `larger` function call. This mechanism is referred to as *template argument deduction*. The arguments to `larger()` are literals of type `double`, so this call causes the compiler to search for an existing definition of `larger()` with `double` parameters. If it doesn't find one, the compiler creates this version of `larger()` from the template by susbstituting `double` for `T` in the template definition. 

The resulting function accepts arguments of type `double` and returs a `double` value.

The compiler makes sure to generate each template instance only once. If a subsequent function call requires the same instance, then it calls the instance that exists.

### Template type parameters.

The name of the template type parameter can be used anywhere in the template's function signature, return type and body. It is a placeholder for a type and can thus be put in any context you would normally put a concrete type.

```cpp
template <class T>
const T& larger(const T& a,const T& b)
{
    return a > b ? a : b;
}
```

### Function Template overloading.

Templated functions can be overloaded.

```cpp
#include <iostream>
#include <vector>

template <typename T>
const T& largest(const T& a,const T& b)
{
    return a > b ? a : b;
}

template <typename T>
const T largest(const std::vector<T>& data)
{
    T max {};
    for(auto v:data)
    {
        if (v >= max)
            max = v;
    }
    return max;
}

int main()
{
    std::cout << "\nLarger of 1.50 and 2.50 is : "  << largest(1.5,2.5);
    std::vector<int> data {
        2, 5, 8, 4, 7, 3
    };
    std::cout << "\nLargest of [2,5,8,4,7,3] is : " << largest(data);
    return 0;
}
```

```
Larger of 1.50 and 2.50 is : 2.5
Largest of [2,5,8,4,7,3] is : 8
```

## Classes and Object Oriented Programming.

An interesting exercise to write a `Matrix<T>` class.

```cpp
// Matrix.h
#include <iostream>
#include <vector>
#include <initializer_list>
#include <stdexcept>

template <typename T = double>
class Matrix {
public:
    //Default constructor
    Matrix() : Matrix(3, 3) {}

    //Parameterized constructor with number of rows, cols as 
    // as arguments.
    Matrix(std::size_t m, std::size_t n) : m_rows(m), m_cols(n)
    {
        m_data.resize(m_rows * m_cols, 0);
    }

    //Parameterized constructor with matrix elements provided 
    // in brace initializer lists.
    Matrix(std::initializer_list<std::initializer_list<T>> m) {
        int i{}, j{};
        for (auto row : m)
        {
            for (auto el : row)
            {
                m_data.push_back(el);
                if (i == 0)
                    ++j;
            }
            ++i;
        }

        m_rows = i;
        m_cols = j;
    }


    //Copy constructor
    Matrix(const Matrix& A) : m_rows{ A.m_rows }, m_cols{ A.m_cols }, m_data{ A.m_data } {}

    std::size_t rows() const
    {
        return m_rows;
    }

    std::size_t cols() const
    {
        return m_cols;
    }

    T& at(int i, int j)
    {
        return m_data[i * m_cols + j];
    }

    const T& at(int i, int j) const
    {
        return m_data[i * m_cols + j];
    }

    T& operator()(int i, int j)
    {
        if (i < 0)
            throw std::invalid_argument("The row index must be non-negative!");

        if (j < 0)
            throw std::invalid_argument("The column index must be non-negative!");

        if (i >= m_rows)
            throw std::invalid_argument("The row index must be less than " + m_rows);

        if (j >= m_cols)
            throw std::invalid_argument("The col index must be less than " + m_cols);

        return at(i, j);
    }

    const T operator()(int i, int j) const
    {
        if (i < 0)
            throw std::invalid_argument("The row index must be non-negative!");

        if (j < 0)
            throw std::invalid_argument("The column index must be non-negative!");

        if (i >= m_rows)
            throw std::invalid_argument("The row index must be less than " + m_rows);

        if (j >= m_cols)
            throw std::invalid_argument("The col index must be less than " + m_cols);

        return at(i, j);
    }

    const Matrix operator+(const Matrix& mat)
    {
        if (mat.rows() != rows())
            throw std::runtime_error("In A + B, matrices A, B should have the same number of rows!");

        if (mat.cols() != cols())
            throw std::runtime_error("In A + B, matrices A, B should have the same number of cols!");

        Matrix result(rows(), cols());

        for (int i{}; i < rows(); ++i)
        {
            for (int j{}; j < cols(); ++j)
            {
                result(i, j) = at(i, j) + mat(i, j);
            }
        }
        return result;
    }

    const Matrix operator-(const Matrix& mat)
    {
        if (mat.rows() != rows())
            throw std::runtime_error("In A - B, matrices A, B should have the same number of rows!");

        if (mat.cols() != cols())
            throw std::runtime_error("In A - B, matrices A, B should have the same number of cols!");

        Matrix result(rows(), cols());

        for (int i{}; i < rows(); ++i)
        {
            for (int j{}; j < cols(); ++j)
            {
                result(i, j) = at(i, j) - mat(i, j);
            }
        }
        return result;
    }

    Matrix& operator=(const Matrix& mat)
    {
        m_data = mat.m_data;
        m_rows = mat.rows();
        m_cols = mat.cols();

        return *this;
    }

    const Matrix operator*(const Matrix& mat)
    {
        if (cols() != mat.rows())
            throw std::runtime_error("In A * B, cols of A must equal rows of B!");

        Matrix result{ rows(), mat.cols() };

        for (int i{}; i < rows(); ++i)
        {
            for (int k{}; k < cols(); ++k)
            {
                for (int j{}; j < mat.cols(); ++j)
                {
                    result(i, j) += at(i, k) * mat(k, j);
                }
            }
        }

        return result;
    }


private:
    std::vector<T> m_data{};
    int m_rows;
    int m_cols;
};
```

```cpp
//Matrix.cpp

#include <iostream>
#include "Matrix.h"

int main()
{
    Matrix<double> A{
        {1, 0},
        {0, 1}
    };

    Matrix<double> B{
        {1, 0},
        {0, 1}
    };

    Matrix<double> result = A + B;

    std::cout << result(0, 0) << "\t" << result(0, 1) << "\n";
    std::cout << result(1, 0) << "\t" << result(1, 1);

    return 0;
}
```

### Access specifiers and class hierarchies.

- When the base class specifier is `public`, the access status of the inherited members remains unchanged. Thus, inherited `public` members are `public`, and inherited `protected` members are `protected` in a derived class.

- When the base class specifier is `protected`, both public and protected members of the base class are inherited as `protected` members in the child class.

- When the base class specifier is `private`, inherited `public` and `protected` members become `private` to the derived class, so that they're accessible by member functions of the the derived class, but they cannot be accessed if they're inherited in another derived class.

### Constructors and Destructors in derived classes.

Every constructor of the derived class always starts by invoking a constructor of the base class. And that base class constructor then invokes the constructor of its base class, and so on.

*Remark.* You cannot initialize the member variables of a base class in the initialization list for the derived class constructor. Not even if thos members are public or protected. 

```cpp
#include <iostream>
#include <vector>
#include <string>

class A{
    public:
    A(){
        std::cout << "\nInside A's constructor";
    }
    ~A()
    {
        std::cout << "\nInside A's destructor";
    }
};

class B : public A
{
    public:
    B()
    {
        std::cout << "\nInside B's constructor";
    }
    
    ~B()
    {
        std::cout << "\nInside B's destructor";
    }
};

int main()
{
    B b;
    
    return 0;
}
```

```
Inside A's constructor
Inside B's constructor
Inside B's destructor
Inside A's destructor
```

Suppose you have a base class `Parent`, two child classes `Child_1` and `Child_2` that inherit from `Parent` and a `Grandchild` class that inherits from `Child_1` and `Child_2`. This is the diamond problem, named after the shape of such inheritance diagrams. The `Grandchild` inherits two copies of `Parent` : one through `Child_1` and another through `Child_2`. 

To prevent the duplication of the base class, we identify to the compiler that the base class should appear only once within the derived class. We do this by specifying the class as a *virtual base class* using the `virtual` keword. The `Child_1` and `Child_2` classes would be defined like this:

```
class Child_1 : public virtual Parent
{
	//...
};

class Child_2 : public virtual Parent
{
	//...
};
```

### Polymorphism.

Every derived class object is a base class object. So, you can use a base class pointer/reference to store the address of a derived class object. It is easy to implement dynamic dispatch through virtual methods.

The below code snippet is instructive in understanding run-time polymorphism.

```cpp
#include <iostream>
#include <memory>
#include <string>

class A {
public:
    void foo() {
        std::cout << "\nGreetings from a!";
    }
};

class B :public A {
public:
    virtual void foo()
    {
        std::cout << "\nGreetings from b!";
    }
};


class C : public B {
private:
    virtual void foo()
    {
        std::cout << "\nGreetings from c!";
    }
};

class D : public C {
public:
    void foo()
    {
        std::cout << "\nGreetings from d!";
    }
};

int main()
{
    D d{};
    A* aptr = &d;
    aptr->foo();

    B* bptr = &d;
    bptr->foo();

    C* cptr = &d;
    //This should not compile. The virtual method foo() is private in C, which is not allowed.
    //cptr->foo();
    
    D* dptr = &d;
    dptr->foo();

    return 0;
}
```

When you specify a function as `virtual` in a base class, you indicate to the compiler that you want dynamic binding for function calls in any class that's derived from this base class. A function that you specifyn as `virtual` in the base class will be `virtual` in all classes that directly or indirectly derive from the base class. This is the case, whether or not you specify the function as `virtual` in the derived class. 

The call to a virtual function using an **object** is always resolved statically. You only get dybamic resolution of calls to virtual functions through a pointer or a reference. Consider the below code snippet:

```cpp
    D d{};
    
    A& aRef = d;
    B& bRef = d;
    A a; B b;
    
    aRef.foo();
    bRef.foo();
    
    a.foo();
    b.foo();
```

```
Greetings from a!
Greetings from d!
Greetings from a!
Greetings from b!
```

#### Requirements for a virtual function.

For a function to be `virtual`, its definition in a derived class must have the same signature as it has in the base class. If the base class function is `const`, for instance, then the derive class function must also be `const`. Generally, the return type of a virtual function in a derived class must be the same as in the base class as well, but there's an exception when the return type in the base class is a pointer or a reference to a class type. In this case, the derived class version of a virtual function may return a pointer or a reference to a more specialized type than that of the base. This is called *covariance*.

Another restriction is that a virtual function can't be a template function. 

In standard object-oriented programming terms, a function in a derived class that redefines a function of the base class is said to *override* this function. A function with the same name as a virtual function in a base class only **overrides** that function if the remainder of their signatures match exactly as well; if they do not, the function in the derived class is a new function that *hides* the one in the base class. 
This means that if you try to use different parameters for a virtual function in a derived class or use different `const` specifiers, then the virtual function mechanism won't work. The function in the derived class then defines, a new different function - and this new function will therefore operate with static binding that is established and fixed at compile time. 

#### `override` specifier.

The `override` specification guarantees that you don't make mistakes in function overrides and these exactly match the virtual function signatures in base class. 

#### `final` qualifier.

Sometimes, we may want to prevent a member function from being overriden in a derived class. We can do this by specifying that a function is `final`.

### Virtual destructors.

Along with the other function, the destructor methods of classes should also be resolved dynamically. That is, if a `Base*` pointer points to `Derived` object, the `Derived` class destructor method should be called first. (Object creation is top-down, destruction is bottom-up in an inheritance hierarchy). So, it's always prudent to declare destructor methods as `virtual`.

### Calling the base class version of a virtual function.

It's easy to call the derived class version of a virtual function through a pointer or reference to a derived class object - the call is made dynamically. However, what do you do when you actually want to call the base class function for a derived class object?

Consider the `Box` and `ToughPack` classes.

```cpp
#include <iostream>
#include <memory>
#include <string>

class Box{
    public:
    
    Box() : Box(1.0) {}
    Box(double side) : Box(side, side, side) {}
    Box(double length, double width, double height) : m_length(length), m_width(width), m_height(height) {}
  
    double virtual volume()
    {
        return m_length * m_width * m_height;
    }
    
    ~Box()
    {
        std::cout << "\nBox dtor";
    }
    protected:
    double m_length;
    double m_width;
    double m_height;
};

class ToughPack : public Box
{
    public:
    ToughPack() : Box() {}
    ToughPack(double side) : Box(side) {}
    ToughPack(double x, double y, double z) : Box(x,y,z) {}
    
    //Function to calculate volume allowing for 15% of packing
    double volume() override
    {
        return 0.85 * m_length * m_width * m_height ;
    }
    
    ~ToughPack()
    {
        std::cout << "\nToughPack dtor";
    }
};
```

In `ToughPack`'s `volume()` method, the `m_length*m_width*m_height` part of the `return` statement is exactly the formula used to compute the `volume()` inside the base class `Box`. In this case, the amount of code we had to retype was limited, but this won't always be the case. It would therefore be much better if you could simply call the base class version of this function isntead.

A plausible first attempt to do so would be:

```
double volume() const override
{
	return 0.85 * volume(); // Infinite recursion!
}
```


However, this would call `volume()` override itself, which would then be calling itself again, which would then be calling itself again! This leads to infinite recursion and a crash.

Calling the base class version from within a function override like this is common. The solution is to explicitly ask the compiler to call the base class version of the function.

```
double volume() const override
{
	return 0.85 * Box::volume(); 
}
```

### When my base class’s constructor calls a virtual function on its this object, why doesn’t my derived class’s override of that virtual function get invoked?

What happens when we call virtual functions from inside constructors and destructors? Calling a polymorphic function from inside a constructor/desctructor is a recipe for disaster in most cases. It should be avoided whenver possible. 

In a constructor, the virtual call mechanism is disabled, because overriding from derived classes hasn't happened yet. Objects are constructed from `Base` up, "Base before derived".

Since `Base` object must be constructed before `Derived`, the call to `f()` always resolves statically to `Base::f()` from inside the constructor.  

```cpp
#include<string>
#include<iostream>
using namespace std;
class B {
public:
	B(const string& ss) { cout << "B constructor\n"; f(ss); }
	virtual void f(const string&) { cout << "B::f\n";}
};
class D : public B {
public:
	D(const string & ss) :B(ss) { cout << "D constructor\n";}
	void f(const string& ss) { cout << "D::f\n"; s = ss; }
private:
	string s;
};
int main()
{
	D d("Hello");
}

```

```
B constructor
B::f
D constructor
```

### How can I set up my class so it won't be inherited from?

Just declare the class as `final`. 

## Pure virtual functions.

There are situations where we require a base class with a virtual function that's redefined in each of the derived classes, but hwere there's no meaningful definition for the function in the base class. For example, you might define a base class `Shape`, from which you derive classes definining specific shapes, such as `Circle`, `Ellipse`, `Rectangle`, `Hexagon` and so on. The `Shape` class could include a virtual function `area()`, that you'd call for the derived class object to compute the area of a particular shape. The `Shape` class itself, though, cannot possibly provide a meaningful implementation of the `area()` function, one that caters, for instance, to both `Circle`s and `Rectangle`s. This is a job for a *pure virtual function*.

The purpose of a pure virtual function is to enable the derived class versions of the function to be called polymorphically. To declare a pure virtual function rather than an ordinary virtual function that has a definition, you use the same syntax but add `=0` to it's declaration within the class. 

```cpp
#include <iostream>
#include <memory>
#include <vector>

class Shape {
public:
    Shape() = default;
    virtual double area() = 0; //pure virtual function

};

class Rectangle : public Shape {
public:
    Rectangle(double l, double w) : m_length(l), m_width(w) {}

    double area() override {
        return m_length * m_width;
    }
private:
    double m_length;
    double m_width;
};

class Circle : public Shape {

public:
    Circle(double r) : m_radius(r) {}

    double area() override {
        return 3.14159 * m_radius * m_radius;
    }

private:
    double m_radius;
};

int main()
{
    //Let's create a container to hold different kinds of shapes
    std::vector<std::unique_ptr<Shape>> shapes{};

    shapes.push_back(std::make_unique<Rectangle>(5.0, 5.0));
    shapes.push_back(std::make_unique<Circle>(3.0));
    shapes.push_back(std::make_unique<Rectangle>(10.0, 12.0));
    shapes.push_back(std::make_unique<Circle>(5.0));

    for (int i{}; i < shapes.size(); ++i)
    {
        std::cout << "\nArea = " << shapes[i]->area();
    }

    return 0;
}
```

```
Area = 25
Area = 28.2743
Area = 120
Area = 78.5397
```

## Abstract Classes.

An abstract class purely exists for the purpose of deriving classes from it and cannot be instantiated.

Any class that contains atleast one pure virtual function is an abstract class. Because an abstract class cannot be instantiated, you cannot pass it by value to a function, a parameter of type `Shape` will not compile. Similarly, you cannot return a `Shape` object from a functiojn. However, pointers or references to an abstract class can be used as parameter or return types, so types such as `Shape*` `std::shared_ptr<Shape*>` and `Shape&` are fine in these settings. 

Any class that inherits from `Shape` is obligated to provide an implementation of the `area()` method. If it doesn't, it too is an abstract class. More specifically, if any pure virtual function of an abstract base class isn't in a derived class, then the pure virtual function will be inherited as such, and the derived class becomes an abstract class.

Thus, abstract base classes (ABCs) are often used as interfaces.