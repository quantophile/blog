---
title: "Numerical methods for ODEs"
date: 2023-09-09T11:33:41+02:00
math: katex
categories: ["Differential Equations"]
---

### Difference operators.

Difference operators are handy tools for derivation, analysis and practical applications of numerical methods for many problems of interpolation, differentiation and quadrature of a function in terms of its values at equidistant arguments. 

Consider the sequence $(y_n)$. Then, we define the **shift operator** $E$ and the **forward difference operator** $\Delta$ by the relations:

$$Ey_n = (y_{n+1}), \quad \Delta y_n = (y_{n+1} - y_n)$$

$E$ and $\Delta$ are thus operators which map one sequence to another sequence. These operators are linear, that is $\alpha$ and $\beta$ are real constants, and $(y_n)$ and $(z_n)$ are two sequences then $E(\alpha y_n + \beta z_n) = \alpha Ey_n + \beta Ez_n$ and similarly for $\Delta$.

Powers of $E$ and $\Delta$ are defined recursively, that is:

$$E^{k}(y) = E(E^{k-1}(y)), \quad \Delta^k (y) = \Delta(\Delta^{k-1} y)$$

By induction, the first equation yields $E^k y_n = y_{n+k}$. We extend the validity of this relation to $k=0$ by setting $E^0 y = y$ and to negative values of $k$. $\Delta^k y$ is called the $k$th difference of the sequence $y$. We make the convention that $\Delta^0 y = 1$. There will be little use of $\Delta^k$ for negative values of $k$, since $\Delta^{-1}$ can be interpreted as the summation operator.

Note that $\Delta y = Ey - y$ and $Ey = y + \Delta y$ for any sequence $y$. It is therefore convenient to express these equations between the operators:

$$\Delta = E - 1, \quad E = 1 + \Delta$$

The identity operator in this context is traditionally denoted by $1$. It can be shown that all formulas derived by the axioms of commutative algebra can be used for these operators. For example, the binomial theorem for positive integral $k$ is:

$$\Delta^k = (E - 1)^k = \sum_{j=0}^k {k \choose j} (-1)^{k-j} E^j \tag{1a}$$

$$E^k = (1 + \Delta)^k = \sum_{j=0}^k {k \choose j} \Delta^j \tag{1b}$$

giving:

$$\Delta^k y_n = \sum_{j=0}^k {k \choose j} (-1)^{k-j} y_{n+j} \tag{2a}$$ 

$$y_{n+k} = \sum_{j=0}^k {k \choose j} \Delta^j y_n \tag{2b}$$

We abbreviate the notation further and write, for example, $Ey_n = y_{n+1}$ instead of $(Ey)_n = y\_{n+1}$. But it is important to remember that these operators *operate on sequences* and not on elements of sequences. 

A difference scheme consists of a sequence and its difference sequences arranged in the following way.


$$
\begin{array}{cccccc}
	y_0 \\\\
		& \Delta y_0 \\\\
	y_1 &  & \Delta^2 y_0\\\\
		& \Delta y_1 & & \Delta^3 y_0 \\\\
	y_2 &  & \Delta^2 y_1 & & \Delta^4 y_0\\\\
		& \Delta y_2 & & \Delta^3 y_1 & & \Delta^5 y_0 \\\\
	y_3 &  & \Delta^2 y_2 & & \Delta^4 y_1 \\\\
		& \Delta y_3 & & \Delta^3 y_2\\\\
	y_4 &  & \Delta^2 y_3\\\\
		& \Delta y_4 \\\\
	y_5
\end{array}
$$

A difference scheme is best computed by successive subtractions, the formulas in (1a) and (1b) are used mostly in theoretical contexts.

In many applications the quantities $y_n$ are computed in increasing order $n=0,1,2,\ldots$ and it is natural that a difference scheme is constructed by means of the quantities previously computed. One therefore introduces the **backward difference operator**:

$$\nabla y_n = y_n - y_{n-1} = (1 - E^{-1})y_n$$

For this operator, we have:

$$\nabla^k  = (1 - E^{-1})^k, \quad E^{-k} = (1 - \nabla)^k$$

Note the reciprocity between the relations $\nabla$ and $E^{-1}$.

*Any linear combination of the elements $y_n$, $y_{n-1}$, $\ldots$, $y_{n-k}$ can also be expressed as a linear combination of $y_n$, $\nabla y_n$, $\ldots$, $\nabla^k y_n$ and vice versa*. For example,

$$
\begin{aligned}
  y_n + y_{n-1} + y_{n-2} &= (1 + E^{-1} + E^{-2}) y_n\\\\
  &= (1 + (1-\nabla) + (1-\nabla)^2) y_n \\\\
  &= (1 + 1 - \nabla + 1 - 2\nabla +\nabla^2) y_n \\\\
  &= (3 - 3\nabla + \nabla^2) y_n \\\\
  &= 3y_n - 3 \nabla y_n + \nabla^2 y_n
\end{aligned}
$$

In this notation, the backward difference scheme reads:

$$
\begin{array}{cccccc}
	y_0 \\\\
		& \nabla y_1 \\\\
	y_1 &  & \nabla^2 y_2\\\\
		& \nabla y_2 & & \nabla^3 y_3 \\\\
	y_2 &  & \nabla^2 y_3 & & \nabla^4 y_4\\\\
		& \nabla y_3 & & \nabla^3 y_4 & & \nabla^5 y_5 \\\\
	y_3 &  & \nabla^2 y_4 & & \nabla^4 y_5 \\\\
		& \nabla y_4 & & \nabla^3 y_5\\\\
	y_4 &  & \nabla^2 y_5\\\\
		& \nabla y_5 \\\\
	y_5
\end{array}
$$

In the backward difference scheme, the subscripts are constant along the diagonals directed upward (backward) to the right, while in the forward difference scheme subscripts are constant along diagonals directed downward (forward). In a computer, a backward difference scheme is preferably stored as a lower-triangular matrix.

**Example.** Consider the difference scheme for the sequence $y = \{\ldots,0,0,0,1,0,0,0,\ldots \}$ that is given below.

$$
\begin{array}{ccccccccc}
					&&&& 0 \\\\
				&&& 0 \\\
			&& 0 	&&   1\\\\
		& 0 	&&  1\\\\
	0 		&& 1	&&   -4\\\\
		& 1 	&& -3\\\\
	1 		&& -2	&&   6\\\\
		& -1 	&& 3\\\\
	0 		&& 1	&& 	 -4\\\\
		& 0 	&& -1\\\\
			&& 0 	&&	 1\\\\
				&&& 0 \\\\
					&&&& 0 
\end{array}
$$

This example shows the **effect of a disturbance in one element** on the sequence of higher differences. Because the effect broadens out and grows quickly, difference schemes are useful in the investigation and correction of computational errors, so called **difference checks**. Notice that, since the differences are linear functions of the sequence, a **superposition** principle holds.

**Lemma 1.** It holds that :

$$\Delta^k (a^x) = (a^h - 1)^k a^x , \quad \nabla^k (a^x) = (1 - a^{-h})^k $$ 

Solution.

We have:

$$
\begin{aligned}
  \Delta^k (a^x) &= \Delta^{k-1}(\Delta a^x)\\\\
  &= \Delta^{k-1} (a^{x+h} - a^{x}) \\\\
  &= (a^h - 1) \Delta^{k-1} (a^x)
\end{aligned}
$$

Applying the above argument repeatedly, it follows that $\Delta^k (a^x) = (a^h - 1)^k a^x$. 

Similarly,

$$
\begin{aligned}
  \nabla^k (a^x) &= \nabla^{k-1}(\nabla a^x)\\\\
  &= \nabla^{k-1} (a^{x} - a^{x-h}) \\\\
  &= (1-a^{-h}) \nabla^{k-1} (a^x)
\end{aligned}
$$

Applying the above argument repeatedly, it follows that $\nabla^k (a^x) = (1 - a^{-h})^k $. 

**Lemma 2.** (Difference of a product). 

$$\Delta (u_n v_n) = u_n \Delta v_n + \Delta u_n v_{n+1}$$

Solution.

The left hand side can be written as :

$$ \Delta (u_n v_n) = u_{n+1} v_{n+1} - u_n v_n$$

The right hand side can be expressed as:

$$u_n \Delta v_n + \Delta u_n v_{n+1} = u_n (v_{n+1} - v_n) + (u_{n+1} - u_n) v_{n+1} = u_{n+1} v_{n+1} - u_n v_n$$

Hence, the identity holds.

### The Calculus of Operators.

Formal calculations with operators, using the rules of algebra and analysis are often an elegant means of assistance in finding approximation formulas that are exact for all polynomials of degree less than (say) $k$, and they should therefore be useful for functions that can be accurately approximated by such a polynomial. Operator calculations also provide error estimates.

Just a small a digression about terminology. An **operator** is a linear transformation from a space $V$ into another linear space $W$. $V$ can be the space of functions, a coordinate space or a space of sequences. The dimension of these spaces can be finite or infinite. For example, the differential operator $D$ maps the infinite dimensional space $C^1 [a,b]$ of functions with a continuous derivative defined on an interval $[a,b]$ to the space of $C[a,b]$ of continuous functions. 

$\mathcal{P}_n$ denotes the space of polynomials of degree less than $n$. $\mathcal{P}_n$ is an $n$-dimensional linear space for which $\{1,x,x^2,\ldots,x^{n-1}\}$ is a basis, called the *power basis*; the coefficients $(c_1,\ldots,c_n)$ are then the coordinates of the polynomial $p$ defined by $p(x) = \sum{i=1}^n c_i x^{i-1}$. We define the following operators:

$$
\begin{aligned}
  E f(x) &= f(x + h)	& \text{Shift operator} \\\\
  \Delta f(x) &= f(x + h) - f(x) & \text{Forward difference operator } \\\\
  \nabla f(x) &= f(x) - f(x-h) & \text{Backward difference operator } \\\\
  Df(x) &= f'(x) & \text{Differentiation operator } \\\\
  \delta f(x) &= f(x + h/2) - f(x - h/2) & \text{Central difference operator}
\end{aligned}
$$

These are all linear operators. They are associative, and they distribute well over addition. In addition, they form a commutative ring. So, their products are commutative. 

Now, we shall go outside of polynomial algebra and consider also the infinite series of operators. The Taylor's series:

$$f(x + h) = f(x) + h f'(x) + \frac{h^2}{2!} f''(x) + \frac{h^3}{3!} f'''(x)+\mathcal{O}(h^4)$$

can be written symbolically as:

$$Ef = \left(1 + hD + \frac{(hd)^2}{2!}+ \frac{(hD)^3}{3!} + \right)f$$

**Theorem.** We have:

$$e^{hD} = E = 1 + \Delta, \quad e^{-hD} = E^{-1} = 1 - \nabla$$

$$2 \sin \frac{hD}{2} = e^{hD/2} - e^{-hD/2}$$

$$(1 + \Delta)^{\theta} = (e^{hD})^{\theta} = e^{\theta hD}, \quad \theta \in \mathbf{R}$$

It is an easy exercise to prove these results.

It follows from the power-series expansion, that,

$$(e^{hD})^\theta f(x) = e^{\theta hD} f(x) = f(x + \theta h)$$

Since, $E = e^{hD}$, it is natural to define:

$$E^{\theta} f(x) = f(x + \theta h)$$

### Adam-Moulton's implicit and Adam-Bashforth's explicit formula.

The above ideas can be used to compute the coefficients of the following relations due to John Adams, which are of great interest in the numerical integration of differential equations of the form $y' = f(t,y)$. 

(a) **Adam-Moulton's implicit formula**:

$$y_{n+1} - y_n = h(a_0 y_{n+1}' + a_1 \nabla y_{n+1}' + a_2 \nabla^2 y_{n+1}' + \ldots )$$

We can show that $\nabla = - \log (1 - \nabla) \sum a_i \nabla^ i $, and find a recurrence relation for the coefficients. 

Solution.

We have:

$$
\begin{aligned}
  \nabla y_{n+1}  &= h(a_0 D + a_1 h \nabla D + a_2 \nabla^2 D + \ldots ) y_{n+1} \\\\
  &= hD (a_0 + a_1 \nabla + a_2 \nabla^2 + \ldots ) y_{n+1} \\\\
  & \\{ \text{ Multiplication is commutative } \\} \\\\
  &= -\log (1 - \nabla) (a_0 + a_1 \nabla + a_2 \nabla^2 + \ldots ) y_{n+1} 
\end{aligned}
$$

Equating both sides, we get:

$$\nabla = \left( \nabla + \frac{\nabla^2}{2} + \frac{\nabla^3}{3} + \frac{\nabla^4}{4} + \ldots \right) (a_0 + a_1 \nabla + a_2 \nabla^2 + \ldots )$$

Collecting the cofficients of $\nabla$, $\nabla^2$, $\nabla^3$, $\nabla^4$, $\ldots$, we have:

$$a_0 = 1$$

$$\frac{a_0}{2} + a_1 = 0$$

$$\frac{a_0}{3} + \frac{a_1}{2} + a_2 = 0$$

In general, we solve the recurrence relation:

$$a_m = -\left(\frac{a_{m-1}}{2} + \frac{a_{m-2}}{3} + \frac{a_{m-3}}{4} + \ldots + \frac{a_{1}}{m-1} + \frac{a_0}{m}\right)$$

for AM($m$).

(b) **Adam-Bashforth's explicit formula**:

$$y_{n+1} - y_n = h(b_0 y_{n}' + b_1 \nabla y_{n}' + b_2 \nabla^2 y_{n}' + \ldots )$$

We can show that $\sum b_i \nabla^i E^{-1} = \sum a_i \nabla ^i $ and that $b_n - b_{n-1} = a_n$.

Solution.

From the previous derivation, it follows that: 

$$y_{n+1} - y_n = hD (a_0 + a_1 \nabla + a_2 \nabla^2 + \ldots ) y_{n+1} = hD (b_0 + b_1 \nabla + b_2 \nabla^2 + \ldots ) E^{-1} y_{n+1}$$

Consequently,

$$(a_0 + a_1 \nabla + a_2 \nabla^2 + \ldots ) = (b_0 + b_1 \nabla + b_2 \nabla^2 + \ldots ) E^{-1}$$

Or,

$$
\begin{aligned}
  \sum a_i \nabla^i &= \sum b_i \nabla^i E^{-1} \\\\
  &= \sum b_i \nabla^i (1 - \nabla) \\\\
  &= b_0 (1 - \nabla) + b_1 (\nabla - \nabla^2) + b_2 (\nabla^2 - \nabla^3) + \ldots \\\\
  &= b_0 + (b_1 - b_0) \nabla + (b_2 - b_1) \nabla^2 + (b_3 - b_2) \nabla^3 + \ldots\\\\
  \sum a_i \nabla^i &= \sum (b_i - b_{i-1}) \nabla_i
\end{aligned}
$$

Consequently, $b_0 = a_0 = 1$, $b_i - b_{i-1} = a_i$.
 
### Implementation.

I coded a few numerical methods from first principles for solving a scalar IVP. The objective is to properly map algorithms to code. 

We are interested to solve the scalar IVP:

$$x'(t) = (1 - 2t)x, \quad x(0) = 1, \quad t \in [0,1]$$

The analytic solution to this ODE by separation of variables is:

$$x(t) = e^{t - t^2}$$

### Adams-Bashforth(2) method.

In the AB(2) method, $$x_{n+1} = x_n + \frac{h}{2}(3f_n - f_{n-1})$$ 

```python
import numpy as np
import math
import matplotlib.pyplot as plt
from matplotlib import style

plt.style.use('seaborn-bright')

# Adam's Bashforth 2-step
def adamsBashforth2(funct, x_0, startTime, endTime, h, epsilon):
    N = int((endTime - startTime)/h)
    f = np.zeros(N+1) ; x = np.zeros(N+1); t= np.linspace(start=startTime,stop=endTime,num=N+1)
    x[0] = x_0;

    # Euler's method to compute x_1
    f[0] = funct(startTime, x[0])
    x[1] = x[0] + h * f[0]
    f[1] = funct(t[1], x[1])

    for i in range(1,N):
        x[i+1] = x[i] + (h/2)*(3*f[i] - f[i-1])
        f[i+1] = funct(t[i+1],x[i+1])

    return t, x, f
```

![Adams-Bashforth](../adams-bashforth2.png)