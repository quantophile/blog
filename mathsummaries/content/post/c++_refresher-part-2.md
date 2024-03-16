---
title: "C++ Refresher - Part 2"
date: 2023-12-19T15:41:24+01:00
math: katex
tags: ["C++"]
categories: ["C++"]
---

# Move Semantics.

## Writing the move constructor and move assignment operator.

### `lvalue` and `rvalue`.

Every single expression has a value category: an `lvalue` or an `rvalue`. An lvalue is an expression that refers to a persistent memory location and allows us to take the address of that memory location via the address-of `&` operator. An `rvalue` evaluates to a result that is stored only transiently. `rvalue`s are typically things you can't take an address of e.g. unnamed temporary objects. 

Historically, `lvalue`s and `rvalue`s were so called because an `lvalue` typically appears on the left of an expression, whereas an `rvalue` could appear only on the right side. If an expression is not an `lvalue`, its an `rvalue`.

Most function call expressions are `rvalue`s. Only, function calls that return a reference `T&` are `lvalue`s.

The memory that stores the result of expressions such as `b + c` and `std::abs()` is reclaimed immediately.

### `rvalue` references.

A reference is a name that you can use an alias for something else. All references that we encountered thus far were `lvalue` references. Normally, an `lvalue` reference is an alias for another variable; it is called an `lvalue` reference because it normally refers to a persistent storage location in which you can store data, so it can appear on the left of an assignment operator. We say normally because C++ does allow reference-to-`const` `lvalue` references - so variables of the type `const T&` to be bound to temporary `rvalue`s.

An `rvalue` reference can be an alias for a variable, just like an `lvalue` reference, but it differs from an `lvalue` reference in that it refer the outcome of an `rvalue` expression, even though this value is generally transient. Being bound to an `rvalue` reference extends the lifetime of such a transient value. Its memory will not be discarded as long as the `rvalue` reference is in scope. 

An `lvalue` binds to `lvalue` reference, an `rvalue` binds to an `rvalue` reference.

We specify an `rvalue` reference using ref-ref `&&`. 

```cpp
int count {5};
int&& rtemp {count + 3}; 				// rvalue reference
std::cout << rtemp << std::endl;		// Output value of expression
int& rcount {count};					// lvalue reference
```

## The basics of `move` semantics.

Consider the code snippet:

```
std::vector<int> v1 {1,2,3,4,5};
std::vector<int> v2 {};
v2 = v1
```

The `vector<int> v1` object has a static part that lives on the stack, and a contigous block of memory allocated dynamically on the free store. The static part consists of the `begin()`, `end()` pointers that hold the addresses of the start and end of the array as well as a third pointer to the very end of the memory you have; something you could use to compute the capacity. The memory block on the free store stores the actual contents `{1,2,3,4,5}`. 

The `vector<int> v2` object in the static part has its `begin()` and `end()` pointers zeroed out, since it's still an empty vector.

Now, I assign `v1` to `v2`. 

```
v2 = v1
```

Now, what do we expect to happen? We would like to have a deep-copy of `v1`. This exactly turns out to be the case. A contigous block of $5$ `int`'s is allocated on the free-store, the starting and ending addresses of memory block are stored in the static part of `v2`, and the contents `{1,2,3,4,5}` is copied to the array. This is also called as value semantics.

Consider another example:

```cpp
#include <iostream>
#include <random>
#include <vector>
#include <functional>

using namespace std;

vector<double> createVector(double value, int N)
{
    return std::vector<double>(value, N);
}

int main(){
	std::vector<double> v2 {};
	
	v2 = createVector(1,5);
	
	return 0;
}
```

The function `createVector` returns a vector of size `N` filled with `value`. 

To begin with, again the vector `v2` is an empty vector, just like earlier with its pointers zeroed out. Then we directly assign `createVector(1,5)` to `v2`. Now, the first thing that happens is, of course, we return a vector from the function. That value is something we don't really have a name for (in the calling scope), we can call it `__tmp__`. This is assigned to `v2`. But, do we really want to create a deep-copy at this point. That would be a shame, because, if we do a deep-copy, `__tmp__` would be destroyed at the end of the statement and we've wasted a lot of energy copying the elements.

What we really want to do is, actually, we would like to transfer the contents of `__tmp__` to `v2`, in a very simple way. We simply want to copy the pointers of `__tmp__` to `v2`. We cannot, however, stop at this point, because effectively, now there are two `vector<double>` objects owning the same memory block. They do not know about each other. The second step is therefore, we have to just zero out the pointers of `__tmp__` vector. 

So, the idea is to do the minimum amount of work to transfer `__tmp__` vector to `v2`. 

Note that, this kind of optimization is only possible, because nobody knows about this `__tmp__` vector except the assignment operation `operator=()`. No one else holds reference to `__tmp__`. If there would be somebody else holding a reference, then we would have a problem. 

At the end of this assignment statement, `__tmp__` goes out of scope, and the final result, the vector we created is in `v2`. Perfecto! 

This is cool stuff! Now, can we do something similar with our earlier code snippet:

```
std::vector<int> v1 {1,2,3,4,5};
std::vector<int> v2 {};
v2 = v1;
```

If indeed we want to transfer(move) the contents of `v1` to `v2`, then all we need to do is, use `std::move`. 

```
v2 = std::move(v1);
```

`std::move` is basically telling us, this is a **transfer of ownership**. We'll look at the details later, but we basically proclaim we want to transfer the contents of `v1` to `v2`. We do exactly the same as before. We, first of all, copy the pointers from `v1` to `v2` and the second step is we zero them out in `v1`. `v1` however in this case lives on a little longer. It will be an empty vector for quite sometime, until it goes out of scope.

## The details of move semantics.

Consider again:

```
std::vector<int> v1 {1,2,3,4,5};
std::vector<int> v2 {};
v2 = v1;
```

`v1` is an `lvalue`. The statement `v2 = v1` invokes the copy assignment operator `operator=(const vector<int>& v)` on `v2`. The `lvalue` `v1` binds to an `lvalue` reference `const vector<int>&`. This assignment operator would now do a copy. It assumes that you indeed want to have this copy. Everything's fine.

Now, let's go to the second assignment.

```
v2 = createVector(1,5);
```

`createVector(1,5)` creates a vector of $5$ elements initialized to $1$. Prior to C++ 11, this would actually have created a copy. And that was the problem. One could not distinguish between the first case and the second case. 

For that reason, they've introduced `rvalue` references. The statement `v2=createVector(1,5)` invokes the move assignment operator `operator=(const vector<int>&& v)` inside the `vector<T>` class. The temporary vector `__tmp__` returned from the function is an `rvalue` and binds to the `rvalue` reference `const vector<int>&&`. Remember, the ref count of the `__tmp__` vector equals $1$, only the move assignment operator function knows about it, so I can do a move. `__tmp__` is not needed afterwards. The move assignment operator will re-wire the pointers, it will copy the pointers of `v2` to `v1`. It will then hollow out the pointers of `v2`. 

## Writing a move constructor and a move assignment operator.


```cpp
#include<iostream>
#include<memory>

using namespace std;

class Resource{
    private:
    int i;
    int* data {nullptr};
    
    public:
    //Move constructor
    Resource(Resource&& r) noexcept
        : i(std::move(r.i))
        , data(std::move(r.data)) //This just copies the pointer
        {
            r.i = 0; //Purely optional, not done by default!
            r.data = nullptr;
        }
    
    //Move assignment operator - canonical form
    Resource& operator=(Resource&& r) noexcept
    {
        //1. Clean up all visible resources
        delete data;
        
        //2. Transfer the content of r into this
        i = std::move(r.i);
        data = std::move(r.data);
        
        //3. Leave r in a valid but undefined state
        r.data = nullptr;
        r.i = 0;
        
        return *this;
    }
};
```

# Forwarding references.

Forwarding references represent :

- an `lvalue` reference, if they are initialized by an `lvalue`.
- an `rvalue` reference, if they are initialized by an `rvalue`. 

`rvalue` references are forwarding references if they:

- involve type deduction
- appear exactly in the form `T&&` or `auto&&`.

A programming language is said to offer first-class function if it allows you to treat functions like any other variable. In such a language, for instance, you can assign a function as a value to a variable, just as an `int` or `string`. You can pass a function as an argument to another function or return one as the result of another function. 

# Lambda expressions.

Lambda expressions offer a convenient, compact syntax to quickly define callback functions or functors. And not only is the syntax compact, lambda expressions also allow you to define the callback's logic right there where you want to use it. 

A *lambda expression* has a lot in common with a function definition. In its most basic form, a lambda expression basically provides a way to define a function with no name, an *anonymous function*. But, lambda expressions are far more powerful than that. In general, a lambda expression effectively defines a full-blown functor that can carry any number of member variables. The beauty is that there's no need for an explicit definition of this type of object anymore; the compiler generate this type automatically for us.

Practically speaking, we'll find that a lambda expression is different from a regular function in that it can access variables that exist in the enclosing scope where it is defined. 

### Defining a lambda expression. 

Consider the following basic lambda expression:

```
[] (int x, int y) {return x < y}
```

The definition of a lambda expression looks very much like the definition of a function. The main difference is that a lambda expression starts with square brackets instead of a return type and a function name. The opening square brackets are called the *lambda introducer*. They mark the beginning of the lambda expression. The lambda introducer is followed by the *lambda parameter list* between the round brackets. This list is exactly like a regular function parameter list. In this case, there's two `int` parameters, `x` and `y`.

The body of the lambda expression between the braces follows the parameter list, again just like a normal function. In general, the body can contain any number of statements. 

It's educational to have atleast a basic notion of how lambda expressions are compiled. Whenever the compiler encounters a lambda expression, it internally generates a new class type. Such a class might look something like this:

```
class __Lambda8C1
{
	public:
		auto operator()(int x, int y) {return x < y;}
};
```

Note that, the data-type of the lambda expression, i.e. the class name `__Lambda8C1` is generated by the compiler. 

### Naming a lambda closure.

A lambda expression evaluates to a function object. The function object is formally called a *lambda closure*, although many people also refer to it informally as either a lambda function or lambda. Since we do not, apriori know what the data-type of the lambda closure will be, only the compiler does, the only way to store a lambda object in a variable is thus to have the compiler deduce the type for you:

```
auto less {[] (int x, int y) {return x < y;} };
```

The `auto` keyword tells the compiler to figure out the type that the variable `less` should have from what appears on the right of the assignment. 

### Generic Lambdas.

A *generic lambda* is a lambda expression where atleast one placeholder type such as `auto`, `auto&` or `const auto&` is used as a parameter type. Doing so effectively turns the function call operator of the generated class into a *template*. 

```
auto less {[] (const auto x, const auto y) {return x < y;}};
```

## The Capture clause.

The lambda introducer `[]` is not necessarily empty. It can contain a *capture clause* that specifies how variables in the enclosing scope can be accessed from within the body of the lambda. The body of the lambda expression with nothing between the square brackets can work only with the arguments and with the variables that are defined locally within the lambda. A lambda with no capture clause is often called a *stateless lambda expression* because it cannot access anything in its enclosing scope. 

### Capturing by value.

If you put `=` between the square brackets, the body of the lambda can access all automatic variables in the enclosing scope by value. That is, while the values of all variables are made available within the lambda expression, the values stored in the original variables cannot be changed.

```
int x {100};

auto square {[=]() { return x * x; }};
```

It should come as no surprise that the closure object should have one member per local variable of the surrounding scope that is used inside the lambda's function body. We say that these variables are captured by the lambda.

### Capturing by reference.

```
int x {25}, y{30};

auto swap {[&]() {
	auto temp = x;
	x = y;
	y = temp;
}};
```

## The `std::function<>` template.

The type of a function pointer is very different from that of a function object or a lambda closure. The former is a pointer, and the latter is a class. At first sight, it might thus seem that the only way to write code that works for any conceivable callback - that is, a function pointer, function object or lambda closure - is to use either `auto` or a template type parameter. 

Using templates does have its cost. You risk template code bloat, where the compiler has to generate specialized code for all different types of callbacks, even when it's not required for performance reasons. It also has its limitations: what if you needed say a `vector<>` of callback functions - a `vector<>` that is potentially filled with a mixture of function pointers, function objects and lambda closures?

To cater to these types of scenarious, the `<functional>` module defines `std::function<>` template. With objects of the type `std::function<>` you can store, copy, move and invoke any kind of function-like entity - be it a function pointer, a function object or a lambda closure. The below example demonstrates precisely this:

```cpp

// Online IDE - Code Editor, Compiler, Interpreter

#include<iostream>
#include<functional>
#include<cmath>
    
// A global less function
bool less(int x, int y) {return x < y;}
    
int main()
{
    int a {18}, b{8};

    std::cout << std::boolalpha; //print true/false, instead of 1/0
    
    std::function<bool(int, int)> compare;
    
    compare = less; //Storing the function pointer less
    std::cout << "\n" << a << " < " << b << ": " << compare(a,b);
    
    compare = std::greater<>{}; //Storing a functor from the standard library
    std::cout << "\n" << a << " > " << b << ": " << compare(a,b);
    
    int n{10};
	//Storing a lambda closure
    compare = [=] (int x, int y) {
        return std::abs(x - n) < std::abs(y - n);
    };
    std::cout << "\n" << a << " nearer to " << n << " than " << b << ": " << compare(a,b);
    
    return 0;
}
```

```
18 < 8: false
18 > 8: true
18 nearer to 10 than 8: false
```

The `std::function<>` variable `compare` is assigned all three different kinds of first class functions - a function pointer, a function object from the standard template library and a lambda closure. In between, all three first class functions are called. More precisely, they are invoked through the `compare` variable's function call operator. A `std::function<>` itself is, in other words, a function object - that encapsulates any other kind of first class function.