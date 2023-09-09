---
title: "Numerical methods for ODEs"
date: 2023-09-09T11:33:41+02:00
math: true
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