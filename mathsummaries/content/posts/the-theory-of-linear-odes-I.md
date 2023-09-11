---
title: "The Theory of Linear Odes I"
date: 2023-09-11T08:06:54+02:00
math: true
tags: ["linear-odes"]
categories: ["Differential Equations"]
---


## The general theory of linear differential equations.

### Introduction.

Consider the differential operator :

$$\begin{aligned}
D:\mathcal{C}^{1}([a,b]) & \mapsto\mathcal{C}([a,b])\\\\
y=f(x) & \mapsto\frac{dy}{dx}
\end{aligned}$$

Since $D$ preserves sums and scalar products,

$$\begin{aligned}
\frac{d}{dx}[f(x)+g(x)] & =\frac{df}{dx}+\frac{dg}{dx}\\\\
\frac{d}{dx}[kf(x)] & =k\frac{df}{dx}
\end{aligned}$$

$D$ is a linear operator. 

The operator $D^{2}[f]$ can be defined as the composition $D(D(f))$.
The essential fact about such compositions is that they are always
linear. Indeed, if $f$ and $g$ are arbitrary functions in $\mathcal{C}^{2}([a,b])$,
we have:

$$\begin{aligned}
D(D(c_{1}f+c_{2}g)) & =D(Dc_{1}f+Dc_{2}g)\\\\
 & =D(c_{1}f'+c_{2}g')\\\\
 & =c_{1}Df'+c_{2}Dg'\\\\
 & =c_{1}f''+c_{2}g''\\\\
 & =c_{1}D^{2}f+c_{2}D^{2}g
\end{aligned}$$

Hence, its linearity has been established. 

Let $a(x)$ be an arbitrary function of $x$. $a(x)D$ is also a linear
operator. Since, the space of linear operators is a vector space,
closed under addition and scalar multiplication, it follows that:

$$\begin{aligned}
L & =a_{n}(x)D^{n}+a_{n-1}(x)D^{n-1}+\ldots+a_{1}(x)D+a_{0}
\end{aligned}$$

is a linear operator.

The composition of linear operators is associative : 

$$\begin{aligned}
S(TU(f)) & =S(T(Uf))\\\\
 & =ST(Uf)
\end{aligned}$$

for all $f$. So, $S(TU)=(ST)U$. 

Moreover, if $I_{V}$ is the identity operator on the vector space
$V$, that is :

$$\begin{aligned}
I_{V}(f) & =f
\end{aligned}$$

for all $f\in V$, and $T$ is any linear operator, then:

$$\begin{aligned}
I_{V}(Tf) & =Tf\\\\
 & =T(I_{V}(f))
\end{aligned}$$

so, $I_{V}T=TI_{V}=T$.

Further, the composition of linear operators distributes well over
addition:

$$\begin{aligned}
S(T+U)[f] & =S((T+U)(f))\\\\
 & =S(Tf+Uf)\\\\
 & \\{\text{By definition of the sum of operators}\\}\\\\
 & =STf+SUf\\\\
 & \\{\text{S is linear}\\}
\end{aligned}$$

So, $S(T+U)=ST+SU$. It is an easy exercise to prove that $(S+T)U=SU+TU$. 

Thus, the composition of operators satisfies most of the properties
associated with the multiplication of ordinary numbers. Hence, we
use the term \emph{product of linear operators}, to imply composition.
In fact, observe that, for the differential operator:

$$\begin{aligned}
D^{m}\cdot D^{n} & =D^{m+n}\\\\
(D^{m})^{n} & =\underbrace{D^{m}\cdot D^{m}\cdots D^{m}}_{n\text{ terms}}\\\\
 & =D^{mn}
\end{aligned}$$

The product of linear operators differs from ordinary multiplication
in one way. Multiplication of operators is non-commutative. If $S$
and $T$ are linear operators on the vector space $V$, then

$$\begin{aligned}
ST & \neq TS
\end{aligned}$$

Consider the following counterexamples. 

**Counterexample** 1. Let $S:\mathbf{R}^{2}\to\mathbf{R}^{2}$
be the operator that rotates a vector in the plane counter-clockwise
by $90$ degrees. $S((x_{1},x_{2}))=(-x_{2},x_{1})$. And let $T:\mathbf{R}^{2}\to\mathbf{R}^{2}$
be the operator that reflects a vector about the $x-$axis. $T((x_{1},x_{2}))=(x_{1},-x_{2})$.
Then, 

$$
ST(\mathbf{e}_{1}) = S(T(1,0))= S(1,0) = (0,1) =\mathbf{e}_2
$$


Whilst,

$$
TS(\mathbf{e}_1) = T(S(1,0)) = T((0,1))=(0,-1)=-\mathbf{e}_2
$$

**Counterexample** 2. Let $S:\mathcal{C}^{1}([a,b])\to\mathcal{C}([a,b])$
be the operator $S:=xD+1$ and $T:\mathcal{C}^{1}([a,b])\to\mathcal{C}([a,b])$
be the operator $T:D-5$. Then,

$$\begin{aligned}
ST(y) & =(xD+1)(D-5)y\\\\
 & =(xD+1)(y'-5y)\\\\
 & =(xD+1)y'-5(xD+1)y\\\\
 & =xy''+y'-5xy'-5y
\end{aligned}$$

Thus, $ST=xD^{2}-(5x-1)D-5$.

On the other hand,

$$\begin{aligned}
TS(y) & =(D-5)(xD+1)y\\\\
 & =(D-5)(xy'+y)\\\\
 & =(D-5)(xy')+(D-5)y\\\\
 & =D(xy')-5xy'+y'-5y\\\\
 & =y'+xy''+y'-5xy'-5y\\\\
 & =xy''+2y'-5xy'-5y
\end{aligned}$$

Thus, $TS=xD^{2}-(5x-2)D-5$.

$ST\neq TS$ in both counterexamples.

In general, the product of linear operators is non-commutative. However,
if $p$ and $q$ are polynomials in $t$, then we know that $p(t)q(t)=q(t)p(t)$.
Polynomial multiplication is commutative. We will be interested in
a systematic study of the linear differential operator with constant
coefficients for this reason.

### Linear Differential Operator.

**Definition.** A linear transformation $L:\mathcal{C}^{n}([a,b])\to\mathcal{C}([a,b])$
is said to be a linear differential operator of order $n$ on the
interval $[a,b]$ if it can be expressed in the form:

$$\begin{aligned}
L & =a_{n}(x)D^{n}+a_{n-1}(x)D^{n-1}+\ldots+a_{1}(x)D+a_{0}(x)\quad\tag{1}
\end{aligned}$$

where the leading coefficients $a_{0}(x),a_{1}(x),\ldots,a_{n}(x)$
are continuous everywhere in $[a,b]$ and $a_{n}(x)\neq0$ on all
of $[a,b]$. 

Thus, the image of a function $f$ in $\mathcal{C}^{n}([a,b])$ under
the linear differential operator described above is the function in
$\mathcal{C}([a,b])$ defined by the identity:

$$\begin{aligned}
Lf & =a_{n}(x)\frac{d^{n}}{dx^{n}}f(x)+a_{n-1}(x)\frac{d^{n-1}}{dx^{n-1}}f(x)+\ldots+a_{1}(x)\frac{d}{dx}f(x)+a_{0}(x)f(x)\quad\tag{2}
\end{aligned}$$

or more simply by:

$$\begin{aligned}
Ly & =a_{n}(x)y^{(n)}+a_{n-1}(x)y^{(n-1)}+\ldots+a_{1}(x)y'+a_{0}(x)y
\end{aligned}$$

Strictly, the left-hand side of the above equations is the value $Lf$
at the point $x$.

An $n$th order *linear differential equation* on an interval
$[a,b]$ is, by definition, an operator equation of the form:

$$\begin{aligned}
Ly & =h(x)\quad\tag{3}
\end{aligned}$$

in which $h$ is continuous on $[a,b]$ and $L$ is the $n$th order
linear differential operator defined on $[a,b]$. Such an equation
is said to be homogenous if $h$ is identically zero on $[a,b]$,
non-homogenous otherwise.

A function $y(x)$ is said to be a solution of the equation (3) if
and only if $y(x)\in\mathcal{C}^{n}([a,b])$ and satisfies the equation
identically on $[a,b]$. 

Given such an equation, we face the problem of finding all its solutions
on $[a,b]$, provided that the solutions exist. They do. However,
save for a very few special types of equations, it is impossible to
express these solutions in terms of known functions. Thus, the systematic
study of linear differential equations must be directed towards analyzing
the general behavior of their solutions in the absence of specific
techniques for exhibiting them. It is here that linearity of the equations
becomes decisive. 

An illustration of the way in which linear algebra intervenes in the
study of differential equations, let:

$$\begin{aligned}
Ly & =0\quad\tag{4}
\end{aligned}$$

be a homogenous linear differential equation of order $n$ on an interval
$[a,b]$ of the $x$-axis. In this case, the solution set of the equation
is the null space of $L$ and hence is a subspace of $\mathcal{C}^{n}([a,b])$.
This subspace is called the \emph{solution space }of the equation,
and the task of solving $Ly=0$ may be replaced by that finding a
\emph{basis} for its solution space, provided that the solution space
is finite-dimensional. It is, and later in this section, we shall
prove the following fundamental result. 

\emph{The solution space of any $n$th order homogenous linear differential
equation is an $n$-dimensional subspace of $\mathcal{C}^{n}([a,b])$.}

Thus, if $L$ is an $n$th order linear differential operator and
$y_{1}(x),y_{2}(x),\ldots,y_{n}(x)$ are linearly independent solutions
of $Ly=0$ then every solution must be of the form:

$$\begin{aligned}
y(x) & =c_{1}y_{1}(x)+c_{2}y_{2}(x)+\ldots+c_{n}y_{n}(x)\quad\tag{5}
\end{aligned}$$

and vice-versa. For this reason, the function (5) with arbitrary $c_{i}$
is called the general solution of (4), while any function obtained
by assigning definite values to the $c_{i}$ is called the \emph{particular
solution}. 

By a familiar line of reasoning, these results are also pertinent
to the study of non-homogenous equations. Let $y_{p}$ be a particular
solution of the non-homogenous equation:

$$\begin{aligned}
Ly & =h(x)\quad\tag{6}
\end{aligned}$$

and let $y_{h}$ be the general solution of the associated homogenous
equation $Ly=0$. Then, we have:

$$\begin{aligned}
L(y_{p}+y_{h}) & =Ly_{p}+Ly_{h}\\\\
 & =Ly_{p}+0\\\\
 & =h(x)
\end{aligned}$$

Thus, the expression $y_{p}+y_{h}$ is the general solution of the
non-homogenous linear differential equation (3). In other words, the
*solution set of a non-homogenous linear differential equation
can be found by adding* **all** *solutions of the associated homogenous equation to any particular solution of the given equation.* 
This argument effectively reduces the problem of solving a non-homogenous
equation to that of finding the general solution of its associated
homogenous equation. And in the next section, we shall complete this
reduction by giving a method whereby a particular solution of (3)
can always be found, once the general solution of the associated homogenous
equation is known. 

**Example.**
The functions $\sin x$ and $\cos x$ are easily seen to be solutions
of the second-order equation:

$$\begin{aligned}
y''+y & =0
\end{aligned}$$

on the interval $(-\infty,\infty).$ Moreover, these functions are
linearly independent on $\mathcal{C}^{2}(\mathbf{R}),$ since if:

$$\begin{aligned}
c_{1}\sin x+c_{2}\cos x & =0
\end{aligned}$$

for all $x\in\mathbf{R}$, then setting $x=0$ and $x=\pi/2$, we
find that $c_{1}=c_{2}=0$. It now follows that the general solution
to $y''+y=0$ is $y(x)=c_{1}\sin x+c_{2}\cos x$, where $c_{1}$ and
$c_{2}$ are arbitrary constants. 

%
**Example.**
The function $y_{p}(x)=x$ is a solution of the non-homogenous equation

$$\begin{aligned}
y''+y & =x
\end{aligned}$$

Hence, since $c_{1}\sin x+c_{2}\cos x$ is the general solution of
the associated homogenous equation $y''+y=0$, the general solution
of the above equation is $y(x)=c_{1}\sin x+c_{2}\cos x+x$.


### First-Order Equations. 

In many ways, the simplest of all differential equations are the linear
equations of order one; that is, equations of the form:

$$\begin{aligned}
a_{1}(x)\frac{dy}{dx}+a_{0}(x)y & =h(x)\quad\tag{7}
\end{aligned}$$

where $a_{0}(x),a_{1}(x)$ and $h(x)$ are continuous on an interval
$[a,b]$. 

In this section, we shall assume, that we can divide this equation
throughout by $a_{1}(x)$ and re-write the above as:

$$\begin{aligned}
\frac{dy}{dx}+p(x)y & =q(x)\quad\tag{8}
\end{aligned}$$

where $p(x)=a_{0}(x)/a_{1}(x)$ and $q(x)=h(x)/a_{1}(x)$.

We have already seen that the general solution of (7) is $y=y_{p}+y_{h}$
where $y_{p}$ is a particular solution and $y_{h}$ is the general
solution of the homogenous equation:

$$\begin{aligned}
\frac{dy}{dx}+p(x)y & =0\quad\tag{9}
\end{aligned}$$

Moreover, by the theorem cited in the previous section, the solution
space of (7) is one-dimensional. Hence, any non-trivial solution $y$
of this equation will be a basis for its solution space and the general
solution of the equation will be $cy$, where $c$ is an arbitrary
constant. 

To find such a $y$, we rewrite (8) as:

$$\begin{aligned}
\frac{1}{y}\frac{dy}{dx} & =-p(x)\\\\
\frac{dy}{y} & =-p(x)dx\\\\
\ln y & =-\int p(x)dx\\\\
y & =e^{-\int p(x)dx}
\end{aligned}$$

Thus, the function $y=e^{-\int p(x)dx}$ is a (non-trivial) solution
of (9) and the general solution of that equation is:

$$\begin{aligned}
y & =ce^{-\int p(x)dx}\quad10
\end{aligned}$$

To complete the task of solving (8), it remains to find a particular
solution. Here, we reason as follows. Suppose that it were possible
to find a continuous function $\mu(x)$ with $\mu(x)\neq0$ everywhere
on $[a,b]$, such that:

$$\begin{aligned}
\frac{d}{dx}[\mu(x)y] & =\mu(x)\left[\frac{dy}{dx}+p(x)y\right]\quad\tag{11}
\end{aligned}$$

Then, (8) can be rewritten as:

$$\begin{aligned}
\frac{d}{dx}[\mu(x)y] & =\mu(x)q(x)
\end{aligned}$$

and the function

$$\begin{aligned}
y & =\frac{1}{\mu(x)}\int\mu(x)q(x)dx\quad\tag{12}
\end{aligned}$$

would be a solution of (8). Thus, we have reduced our problem to finding
a function $\mu$ that satisfies (11). But,

$$\begin{aligned}
\frac{d}{dx}[\mu(x)y] & =\mu(x)\frac{dy}{dx}+\frac{d\mu}{dx}y\quad\tag{13}
\end{aligned}$$

Comparing this with (11), we see that $\mu$ must be chosen so that:

$$\begin{aligned}
\frac{d\mu}{dx} & =\mu(x)p(x)
\end{aligned}$$

Thus,

$$\begin{aligned}
\frac{1}{\mu}d\mu & =p(x)dx
\end{aligned}$$

and arguing as we did above, $\mu=e^{\int p(x)dx}$. Finally, substitution
in (12) gives:

$$\begin{aligned}
y & =e^{-\int p(x)dx}\left(\int e^{\int p(x)dx}q(x)dx\right)\quad\tag{14}
\end{aligned}$$

and it follows that the general solution of (8) is:

$$\begin{aligned}
y(x) & =e^{-\int p(x)dx}\left(\int e^{\int p(x)dx}q(x)dx+c\right)\quad\tag{15}
\end{aligned}$$

These results are summarized in the following theorem:
\begin{thm*}
Let 

$$\begin{aligned}
\frac{dy}{dx}+p(x)y & =q(x)\quad\tag{17}
\end{aligned}$$

be defined on an interval $[a,b]$. Then, the general solution of
this equation is:

$$\begin{aligned}
y & =\left[c+\int q(x)e^{\int p(x)dx}dx\right]e^{-\int p(x)dx}\quad\tag{18}
\end{aligned}$$

Considering the simplicity of the technique underlying this result,
it is hardly worth the efffort to commit this result to memory. Instead
it is easier to treat each first order equation separately, as follows:

\emph{Write the equation in the form $\frac{dy}{dx}+p(x)y=q(x)$,
and then multiply by $e^{\int p(x)dx}$ and integrate.}

The function

$$\begin{aligned}
\mu(x) & =e^{\int p(x)dx}\quad\tag{19}
\end{aligned}$$

introduced above is called the integrating factor for the equation
$y'+p(x)y=q(x)$. Integrating factors will be discussed in greater
detail further ahead.

**Example.**
Find the general solution of the equation:

$$\begin{aligned}
\frac{dy}{dx}+2xy & =x
\end{aligned}$$

*Solution.*

The integrating factor $\mu(x)=e^{\int2xdx}=e^{x^{2}}$. We have:

$$\begin{aligned}
e^{x^{2}}\frac{dy}{dx}+2xe^{x^{2}}y & =xe^{x^{2}}\\\\
\frac{d}{dx}[e^{x^{2}}y] & =xe^{x^{2}}\\\\
d[e^{x^{2}}y] & =xe^{x^{2}}dx\\\\
e^{x^{2}}y & =\frac{1}{2}\int2xe^{x^{2}}dx+c\\\\
& =\frac{1}{2}\int e^{u}du+c \\\\
& \\{ \text{Upon substituting } u=x^2 \\} \\\\
& =\frac{1}{2}e^{u}+c \\\\
& =\frac{1}{2}e^{x^{2}}+c\\\\
y & =\frac{1}{2}+ce^{-x^{2}}
\end{aligned}$$


**Example.**
Solve the equation:

$$\begin{aligned}
x\frac{dy}{dx}+y & =x
\end{aligned}$$

*Solution.*

In the interval $\mathbf{R}-\{0\}$, we can rewrite the above equation
as:

$$\begin{aligned}
\frac{dy}{dx}+\frac{1}{x}y & =1
\end{aligned}$$

The integrating factor $\mu(x)=e^{\int\frac{dx}{x}}=e^{\ln x}=x$.
We have:

$$\begin{aligned}
x\left[\frac{dy}{dx}+\frac{1}{x}y\right] & =x\\\\
x\frac{dy}{dx}+y & =x\\\\
\frac{d}{dx}[xy] & =x\\\\
d(xy) & =xdx\\\\
\int d(xy) & =\int xdx+c\\\\
xy & =\frac{x^{2}}{2}+c\\\\
y & =\frac{x}{2}+\frac{c}{x}
\end{aligned}$$

**Example.**
(Bernoulli's equation) Any first-order ordinary differential equation
of the form:

$$\begin{aligned}
\frac{dy}{dx}+p(x)y & =q(x)y^{n} 
\end{aligned}$$

where $n$ is a real number, is known as the Bernoulli equation.
It is non-linear for all values of $n$ different from $0$ or $1$.
Nonetheless, it can be solved as a first-order linear differential
equation by making a change of variable, as follows:

Dismissing the cases $n=0$ and $n=1$, which were treated above,
we rewrite (\ref{eq:bernoulli-equation}) as:

$$\begin{aligned}
y^{-n}\frac{dy}{dx}+p(x)y^{1-n} & =q(x)
\end{aligned}$$

and set $u=y^{1-n}$. Then,

$$\begin{aligned}
\frac{du}{dx} & =\frac{d}{dx}[y^{1-n}]=(1-n)y^{-n}\frac{dy}{dx}
\end{aligned}$$

So,

$$\begin{aligned}
\frac{1}{(1-n)}\frac{du}{dx}+p(x)u & =q(x)
\end{aligned}$$

We can now solve this first-order linear differential equation. 

For example, to solve :

$$\begin{aligned}
\frac{dy}{dx}+y & =(xy)^{2}
\end{aligned}$$

We rewrite the equation as:

$$\begin{aligned}
y^{-2}\frac{dy}{dx}+\frac{1}{y} & =x^{2}
\end{aligned}$$

and substitute $u=\frac{1}{y}$. Thus, $\frac{du}{dx}=-\frac{1}{y^{2}}\frac{dy}{dx}$.
Consequently,

$$\begin{aligned}
-\frac{du}{dx}+u & =x^{2}
\end{aligned}$$

or equivalently,

$$\begin{aligned}
\frac{du}{dx}-u & =-x^{2}
\end{aligned}$$

The integrating factor is $e^{-\int dx}=e^{-x}$. Multiplying both
sides by the integrating factor, we get:

$$\begin{aligned}
e^{-x}\frac{du}{dx}-e^{-x}u & =-x^{2}e^{-x}\\\\
d(ue^{-x}) & =-x^{2}e^{-x}\\\\
\int d(ue^{-x}) & =-\int x^{2}e^{-x}
\end{aligned}$$

Integrating the right hand side by parts, we have:

\begin{tabular}{|c|c|}
\hline 
$u$ & $dv$\tabularnewline
\hline 
\hline 
$x^{2}$ & $e^{-x}$\tabularnewline
\hline 
$2x$ & $-e^{-x}$\tabularnewline
\hline 
$2$ & $e^{-x}$\tabularnewline
\hline 
\end{tabular}

$$\begin{aligned}
\int x^{2}e^{-x}dx & =-x^{2}e^{-x}-2xe^{-x}+2\int e^{-x}dx+c\\\\
 & =-(x^{2}+2x+2)e^{-x}+c
\end{aligned}$$

So:

$$\begin{aligned}
ue^{-x} & =(x^{2}+2x+2)e^{-x}+c\\\\
u & =(x^{2}+2x+2)+ce^{x}\\\\
y & =\frac{1}{(x^{2}+2x+2)+ce^{x}}
\end{aligned}$$


**Exercise.**
Solve the equation

$$\begin{aligned}
xy'+2y & =0
\end{aligned}$$


*Solution.*

We re-write the equation as:

$$\begin{aligned}
y'+\frac{2}{x}y & =0,\quad x\neq0
\end{aligned}$$

The integrating factor is:

$$\begin{aligned}
\mu(x) & =e^{\int p(x)dx}=e^{\int\frac{2}{x}dx}=e^{\ln x^{2}}=x^{2}
\end{aligned}$$

Multiplying by the integrating factor on both sides of the differential
equation, we have:

$$\begin{aligned}
x^{2}y'+2xy & =0\\\\
d(x^{2}y) & =0\\\\
\int d(x^{2}y) & =c\\\\
x^{2}y & =c\\\\
y & =\frac{c}{x^{2}}
\end{aligned}$$

**Exercise.**
Solve the equation:

$$\begin{aligned}
(1-x^{2})y'-y & =0
\end{aligned}$$


*Solution.*

We re-write the equation in the form $y'+p(x)y=q(x)$. We have:

$$\begin{aligned}
y' & -\frac{1}{1-x^{2}}y=0,\quad x\neq\pm1
\end{aligned}$$

The integrating factor $\mu(x)$ is :

$$\begin{aligned}
\mu(x) & =e^{\int p(x)dx}=e^{-\int\frac{dx}{1-x^{2}}}\\\\
 & =e^{\int\frac{dx}{(x-1)(x+1)}}\\\\
 & =e^{\frac{1}{2}\int\left(\frac{1}{x-1}-\frac{1}{x+1}\right)dx}\\\\
 & =e^{\frac{1}{2}\ln\left(\frac{x-1}{x+1}\right)}\\\\
 & =\left(\frac{x-1}{x+1}\right)^{1/2}
\end{aligned}$$

Multiplying the differential equation on both sides by the integrating
factor, we have:

$$\begin{aligned}
y'\sqrt{\frac{x-1}{x+1}}+\sqrt{\frac{x-1}{x+1}}\cdot\frac{1}{(x-1)(x+1)}y & =0\\\\
y'\sqrt{\frac{x-1}{x+1}}+\frac{1}{\sqrt{(x-1)}(x+1)^{3/2}}y & =0
\end{aligned}$$

Observe that:

$$\begin{aligned}
\frac{d}{dx}\left[\sqrt{\frac{x-1}{x+1}}\right] & =\frac{1}{2}\sqrt{\frac{x+1}{x-1}}\cdot\frac{d}{dx}\left(\frac{x-1}{x+1}\right)\\\\
 & =\frac{1}{2}\sqrt{\frac{x+1}{x-1}}\frac{(x+1)-(x-1)}{(x+1)^{2}}\\\\
 & =\frac{1}{2}\cdot\frac{2}{\sqrt{x-1}(x+1)^{3/2}}\\\\
 & =\frac{1}{\sqrt{x-1}(x+1)^{3/2}}
\end{aligned}$$

Consequently,

$$\begin{aligned}
d\left(y\sqrt{\frac{x-1}{x+1}}\right) & =0\\\\
\int d\left(y\sqrt{\frac{x-1}{x+1}}\right) & =c\\\\
y\sqrt{\frac{x-1}{x+1}} & =c\\\\
y & =c\sqrt{\frac{x+1}{x-1}}
\end{aligned}$$

**Exercise.**
Solve the equation:

$$\begin{aligned}
(\sin x)y'+(\cos x)y & =0
\end{aligned}$$


*Solution.*

We have:

$$\begin{aligned}
d(\sin x\cdot y) & =0\\\\
\int d(\sin x\cdot y) & =c\\\\
y\cdot\sin x & =c\\\\
y & =c\arcsin x
\end{aligned}$$

**Exercise.**
Solve the equation:

$$\begin{aligned}
3y'+ky & =0
\end{aligned}$$


*Solution.*

We re-write the equation in the form $y'+p(x)y=q(x)$. We have:

$$\begin{aligned}
y'+\frac{k}{3}y & =0
\end{aligned}$$

The integrating factor is:

$$\begin{aligned}
\mu(x) & =e^{\int\frac{k}{3}dx}\\\\
 & =e^{(k/3)x}
\end{aligned}$$

Multiplying both sides of the differential equation by $\mu(x)$,
we have:

$$\begin{aligned}
y'e^{(k/3)x}+(k/3)e^{(k/3)x}y & =0\\\\
d(e^{(k/3)x}y) & =0\\\\
\int d(e^{(k/3)x}y) & =c\\\\
e^{(k/3)x}y & =c\\\\
y & =ce^{-(k/3)x}
\end{aligned}$$

**Exercise.**
Solve the equation:

$$\begin{aligned}
2y'+3y & =e^{-x}
\end{aligned}$$


*Solution.*

We write the equation in the form:

$$\begin{aligned}
y'+\frac{3}{2}y & =e^{-x}
\end{aligned}$$

The integrating factor $\mu(x)$ is:

$$\begin{aligned}
\mu(x) & =e^{\int p(x)dx}\\\\
 & =e^{\frac{3}{2}\int dx}=e^{3x/2}
\end{aligned}$$

Multiplying both sides of the differential equation by $e^{3x/2}$,
we have:

$$\begin{aligned}
y'e^{3x/2}+\frac{3}{2}e^{3x/2}y & =e^{x/2}\\\\
d(e^{3x/2}y) & =e^{x/2}dx\\\\
\int d(e^{3x/2}y) & =\int e^{x/2}dx+c\\\\
ye^{3x/2} & =2e^{x/2}+c\\\\
y & =2e^{-x/2}+ce^{-3x/2}
\end{aligned}$$

**Exercise.**
Solve the equation:

$$\begin{aligned}
3xy'-y & =\ln x+1
\end{aligned}$$


*Solution.*

We bring the equation into the form $y'+p(x)y=q(x)$. We have:

$$\begin{aligned}
y'-\frac{1}{3x}y & =\frac{\ln x}{3x}+\frac{1}{3x}
\end{aligned}$$

The integrating factor $\mu(x)$ is:

$$\begin{aligned}
\mu(x) & =e^{\int p(x)dx}\\\\
 & =e^{\int-\frac{1}{3x}dx}\\\\
 & =e^{-1/3\ln x}\\\\
 & =x^{-1/3}
\end{aligned}$$

Multiplying both sides of the differential equation by $x^{-1/3}$,
we have:

$$\begin{aligned}
\frac{1}{x^{1/3}}y'-\frac{1}{3x^{4/3}}y & =\frac{\ln x}{3x^{4/3}}+\frac{1}{3x^{4/3}}
\end{aligned}$$

Observe that:

$$\begin{aligned}
\frac{d}{dx}\left(x^{-1/3}\right) & =-\frac{1}{3}x^{-4/3}
\end{aligned}$$

So:

$$\begin{aligned}
d\left(\frac{y}{x^{1/3}}\right) & =\frac{\ln x}{3x^{4/3}}dx+\frac{1}{3}x^{-4/3}dx\\\\
\int d\left(\frac{y}{x^{1/3}}\right) & =\int\frac{\ln x}{3x^{4/3}}dx+\frac{1}{3}\int x^{-4/3}dx+c\\\\
\frac{y}{x^{1/3}} & =\frac{1}{3}\int ue^{-u/3}du-x^{-1/3}+c
\end{aligned}$$

We have, using integration by parts:

$$\begin{aligned}
\int ue^{-u/3}du & =u\cdot\frac{e^{-u/3}}{(-1/3)}-\int\frac{e^{-u/3}}{(-1/3)}du\\\\
 & =-3ue^{-u/3}+3\int e^{-u/3}du\\\\
 & =-3ue^{-u/3}-9e^{-u/3}\\\\
 & =-\frac{3(3+\ln x)}{x^{1/3}}
\end{aligned}$$

It follows that:

$$\begin{aligned}
\frac{y}{x^{1/3}} & =-\frac{(3+\ln x)}{x^{1/3}}-\frac{1}{x^{1/3}}+c\\\\
\frac{y}{x^{1/3}} & =-\frac{4}{x^{1/3}}-\frac{\ln x}{x^{1/3}}+c\\\\
y & =-\ln x-4+cx^{1/3}
\end{aligned}$$

**Exercise.**
Solve the equation:

$$\begin{aligned}
L\frac{di}{dt}+Ri & =E
\end{aligned}$$


*Solution.*

We first write the equation in the form $y'+p(x)y=q(x)$. We have:

$$\begin{aligned}
\frac{di}{dt}+\frac{R}{L}i & =\frac{E}{L}
\end{aligned}$$

The integrating factor $\mu(x)$ is given by:

$$\begin{aligned}
\mu(i) & =e^{\int p(i)di}\\\\
 & =e^{\frac{R}{L}\int di}\\\\
 & =e^{(R/L)i}
\end{aligned}$$

Multiplying both sides of the equation by the integrating factor,
we have:

$$\begin{aligned}
e^{(R/L)i}\cdot i'+\frac{R}{L}e^{(R/L)i}\cdot i & =\frac{E}{L}e^{(R/L)i}\\\\
d\left(e^{(R/L)i}\cdot i\right) & =\frac{E}{L}e^{(R/L)i}\cdot di\\\\
\int d\left(e^{(R/L)i}\cdot i\right) & =\frac{E}{L}\int e^{(R/L)i}\cdot di+c\\\\
e^{(R/L)i}\cdot i & =\frac{E}{L}\frac{e^{(R/L)i}}{(R/L)}+c\\\\
 & =\frac{E}{R}e^{(R/L)i}+c\\\\
i & =\frac{E}{R}+ce^{-(R/L)i}
\end{aligned}$$

**Exercise.**
Solve the equation:

$$\begin{aligned}
(3x^{2}+1)y'-2xy & =6x
\end{aligned}$$


*Solution.*

Putting the equation into the form $y'+p(x)y=q(x)$, we have:

$$\begin{aligned}
y'-\frac{2x}{1+3x^{2}}y & =\frac{6x}{1+3x^{2}}
\end{aligned}$$

The integrating factor $\mu(x)$ is given by:

$$\begin{aligned}
\mu(x) & =\exp\left[-\int\frac{2x}{1+3x^{2}}dx\right]\\\\
 & =\exp\left[-\frac{1}{3}\int\frac{6x}{1+3x^{2}}dx\right]\\\\
 & \left\\{ \text{Put }u=1+3x^{2},du=6xdx\right\\} \\\\
 & =\exp\left[-\frac{1}{3}\int\frac{du}{u}\right]\\\\
 & =\exp\left[\ln u^{(-1/3)}\right]\\\\
 & =u^{(-1/3)}\\\\
 & =\frac{1}{(1+3x^{2})^{1/3}}
\end{aligned}$$

Multiplying both sides by the integrating factor $\frac{1}{(1+3x^{2})^{1/3}}$,
we get:

$$\begin{aligned}
\frac{1}{(1+3x^{2})^{1/3}}y'-\frac{2x}{(1+3x^{2})^{4/3}}y & =\frac{6x}{(1+3x^{2})^{4/3}}
\end{aligned}$$

Note that:

$$\begin{aligned}
\frac{d}{dx}\left[\frac{1}{(1+3x^{2})^{1/3}}\right] & =-\frac{1}{3}(1+3x^{2})^{-4/3}\cdot6x=-\frac{2x}{(1+3x)^{4/3}}
\end{aligned}$$

Consequently,

$$\begin{aligned}
d\left[\frac{y}{(1+3x^{2})^{1/3}}\right] & =\frac{6x}{(1+3x^{2})^{4/3}}dx\\\\
\int d\left[\frac{y}{(1+3x^{2})^{1/3}}\right] & =\int\frac{6x}{(1+3x^{2})^{4/3}}dx+c\\\\
 & \left\\{ \text{Put }(1+3x^{2})=u,6xdx=du\right\\} \\\\
 & =\int\frac{du}{u^{4/3}}+c\\\\
 & =\frac{u^{-1/3}}{(-1/3)}+c\\\\
\frac{y}{(1+3x^{2})^{1/3}} & =-\frac{3}{(1+3x^{2})^{1/3}}+c\\\\
y & =-3+c(1+3x^{2})^{1/3}
\end{aligned}$$

**Exercise.**
Solve the equation:

$$\begin{aligned}
(x^{2}+1)y'-(1-x)^{2}y & =xe^{-x}
\end{aligned}$$


*Solution.*

We bring the equation into the form $y'+p(x)y=q(x)$. We have:

$$\begin{aligned}
y'-\frac{(1-x)^{2}}{(x^{2}+1)}y & =\frac{xe^{-x}}{1+x^{2}}
\end{aligned}$$

The integrating factor $\mu(x)$ is:

$$\begin{aligned}
\mu(x) & =\exp\left[-\int\frac{(1-x)^{2}}{1+x^{2}}dx\right]\\\\
 & =\exp\left[-\int\frac{1-2x+x^{2}}{1+x^{2}}dx\right]\\\\
 & =\exp\left[-\int\left(1-\frac{2x}{1+x^{2}}\right)dx\right]\\\\
 & \left\\{ \text{Putting }1+x^{2}=u, 2xdx=du\right\\} \\\\
 & =\exp\left[-\left(\int dx-\int\frac{du}{u}\right)\right]\\\\
 & =\exp\left[-\left(x-\ln u\right)\right]\\\\
 & =\exp\left[\ln(1+x^{2})-x\right]\\\\
 & =(1+x^{2})e^{-x}
\end{aligned}$$

Multiplying both sides of the differential equation by the integrating
factor, we get:

$$\begin{aligned}
y'(1+x^{2})e^{-x}-(1-x)^{2}e^{-x}y & =xe^{-2x}\\\\
d\left((1+x^{2})e^{-x}y\right) & =xe^{-2x}dx\\\\
\int d\left((1+x^{2})e^{-x}y\right) & =\int xe^{-2x}dx+c\\\\
(1+x^{2})e^{-x}y & =-\frac{x}{2}e^{-2x}-\frac{e^{-2x}}{4}+c\\\\
y & =-\frac{xe^{-x}}{2(1+x^{2})}-\frac{e^{-x}}{4(1+x^{2})}+\frac{ce^{x}}{(1+x^{2})}
\end{aligned}$$

**Exercise.**
Solve the equation:

$$\begin{aligned}
(x^{2}+1)y'+xy & =(1-2x)\sqrt{1+x^{2}}
\end{aligned}$$


*Solution.*

Re-arranging the above equation in the form $y'+p(x)y=q(x)$, we get:

$$\begin{aligned}
y'+\frac{x}{1+x^{2}}y & =\frac{1-2x}{\sqrt{1+x^{2}}}
\end{aligned}$$

The integrating factor $\mu(x)$ is given by:

$$\begin{aligned}
\mu(x) & =e^{\int\frac{x}{1+x^{2}}dx}\\\\
 & =e^{\frac{1}{2}\int\frac{2x}{1+x^{2}}dx}\\\\
 & =e^{(1/2)\ln(1+x^{2})}\\\\
 & =\sqrt{1+x^{2}}
\end{aligned}$$

Multiplying both sides of the differential equation by $\sqrt{1+x^{2}}$,
we have:

$$\begin{aligned}
\sqrt{1+x^{2}}y'+\frac{x}{\sqrt{1+x^{2}}}y & =(1-2x)\\\\
d\left[\sqrt{1+x^{2}}\cdot y\right] & =(1-2x)dx\\\\
\int d\left[\sqrt{1+x^{2}}\cdot y\right] & =\int(1-2x)dx+c\\\\
\sqrt{1+x^{2}}y & =x-x^{2}+c\\\\
y & =\frac{c+x-x^{2}}{\sqrt{1+x^{2}}}
\end{aligned}$$

**Exercise.**
Solve the equation:

$$\begin{aligned}
x\sin x\frac{dy}{dx}+(\sin x+x\cos x)y & =xe^{x}
\end{aligned}$$


*Solution.*

We have:

$$\begin{aligned}
d(x\sin x\cdot y) & =xe^{x}dx\\\\
\int d(x\sin x\cdot y) & =\int xe^{x}dx+c\\\\
x\sin x\cdot y & =xe^{x}-e^{x}+c\\\\
y & =\frac{e^{x}}{\sin x}+\frac{c-e^{x}}{x\sin x}
\end{aligned}$$

**Exercise.**
Solve the equation:

$$\begin{aligned}
x\frac{dy}{dx}+\frac{y}{\sqrt{2x+1}} & =1+\sqrt{2x+1}
\end{aligned}$$


*Solution.*

We rewrite the equation in the form $y'+p(x)y=q(x)$. We have:

$$\begin{aligned}
y'+\frac{y}{x\sqrt{2x+1}} & =\frac{1+\sqrt{2x+1}}{x}
\end{aligned}$$

The integrating factor is:

$$\begin{aligned}
\mu(x) & =\exp\left[\int\frac{dx}{x\sqrt{2x+1}}\right]\\\\
 & \\{\text{Put }\sqrt{2x+1}=u,\:(2x+1)=u^{2},\:dx=udu\\}\\\\
 & =\exp\left[2\int\frac{udu}{(u^{2}-1)u}\right]\\\\
 & =\exp\left[2\int\frac{\cancel{u}\cdot du}{(u^{2}-1)\cdot\cancel{u}}\right]\\\\
 & =\exp\left[\int\left(\frac{1}{u-1}-\frac{1}{u+1}\right)du\right]\\\\
 & =\exp\left[\int\left(\frac{1}{u-1}-\frac{1}{u+1}\right)du\right]\\\\
 & =\exp\left[\ln\left(\frac{u-1}{u+1}\right)\right]\\\\
 & =\left(\frac{u-1}{u+1}\right)\\\\
 & =\left(\frac{\sqrt{2x+1}-1}{\sqrt{2x+1}+1}\right)
\end{aligned}$$

Multiplying both sides of the equation by the integrating factor,
we have:

$$\begin{aligned}
d\left[\left(\frac{\sqrt{2x+1}-1}{\sqrt{2x+1}+1}\right)y\right] & =\frac{\sqrt{2x+1}-1}{x}dx\\\\
\int d\left[\left(\frac{\sqrt{2x+1}-1}{\sqrt{2x+1}+1}\right)y\right] & =\int\frac{\sqrt{2x+1}-1}{x}dx+c
\end{aligned}$$

We have:

$$\begin{aligned}
\int\frac{\sqrt{2x+1}-1}{x}dx & =\int\frac{v-1}{(v^{2}-1)/2}vdv\\\\
 & =2\int\frac{vdv}{v+1}\\\\
 & =2\int\left(1-\frac{1}{v+1}\right)dv\\\\
 & =2\left(\int dv-\int\frac{dv}{v+1}\right)\\\\
 & =2v-\ln(v+1)\\\\
 & =2\sqrt{2x+1}-\ln(\sqrt{2x+1}+1)
\end{aligned}$$

Consequently, the desired solution is:

$$\begin{aligned}
y & =\frac{\sqrt{2x+1}+1}{\sqrt{2x+1}-1}\left[2\sqrt{2x+1}-\ln(\sqrt{2x+1}+1)+c\right]
\end{aligned}$$

**Exercise.**
Solve the equation:

$$\begin{aligned}
\sin x\cos x\frac{dy}{dx}+y & =\tan^{2}x
\end{aligned}$$


*Solution.*

Rearranging this equation in the form $y'+p(x)y=q(x)$, we have:

$$\begin{aligned}
y'+\frac{y}{\sin x\cos x} & =\frac{\tan^{2}x}{\sin x\cos x}
\end{aligned}$$

The integrating factor $\mu(x)$ is given by:

$$\begin{aligned}
\mu(x) & =e^{\int\frac{dx}{\sin x\cos x}}\\\\
 & =e^{2\int\frac{dx}{\sin2x}}\\\\
 & =e^{2\int cosec(2x)dx}\\\\
 & =e^{2\int cosec(2x)\cdot\frac{(cosec(2x)-\cot(2x)}{(cosec(2x)-\cot(2x)}dx}\\\\
 & =e^{\ln(cosec(2x)-\cot(2x))}\\\\
 & =cosec(2x)-\cot2x\\\\
 & =\frac{1-\cos2x}{\sin2x}=\frac{2\sin^{2}x}{2\sin x\cos x}\\\\
 & =\tan x
\end{aligned}$$

Multiplying both sides of the differential equation by $\tan x$,
we get:

$$\begin{aligned}
d(y\cdot\tan x) & =(\sec^{2}x\cdot\tan^{2}x)dx\\\\
\int d(y\cdot\tan x) & =\int\sec^{2}x\cdot\tan^{2}x\cdot dx+c\\\\
 & \\{\text{Put }u=\tan x,du=\sec^{2}x\cdot dx\\}\\\\
 & =\int u^{2}du+c\\\\
 & =\frac{u^{3}}{3}+c\\\\
y\cdot\tan x & =\frac{\tan^{3}x}{3}+c\\\\
y & =\frac{\tan^{2}x}{3}+c\cot x
\end{aligned}$$

**Exercise.**
Solve the equation:

$$\begin{aligned}
(1+\sin x)\frac{dy}{dx}+(2\cos x)y & =\tan x
\end{aligned}$$


*Solution.*

Re-arranging the given equation in the form $y'+p(x)y=q(x)$, we have:

$$\begin{aligned}
y'+\frac{2\cos x}{1+\sin x}y & =\frac{\tan x}{1+\sin x}
\end{aligned}$$

The integrating factor is:

$$\begin{aligned}
\mu(x) & =e^{\int p(x)dx}\\\\
 & =\exp\left[\int\frac{2\cos x}{1+\sin x}dx\right]\\\\
 & \\{\text{Put } u=1+\sin x,du=\cos x\cdot dx\\}\\\\
 & =\exp\left[\int\frac{2du}{u}\right]\\\\
 & =\exp\left[\ln u^{2}\right]\\\\
 & =u^{2}=(1+\sin x)^{2}
\end{aligned}$$

Multiplying both sides of the differential equation by the integrating
factor, we have:

$$\begin{aligned}
y'(1+\sin x)^{2}+2\cos x(1+\sin x)y & =\tan x(1+\sin x)\\\\
d\left[(1+\sin x)^{2}y\right] & =\tan x(1+\sin x)dx\\\\
 & =\int\tan x\cdot dx+\int\frac{\sin^{2}x}{\cos x}dx+c\\\\
 & =\ln(\cos x)+\int\frac{1-\cos^{2}x}{\cos x}dx+c\\\\
 & =\ln(\cos x)+\int(\sec x-\cos x)dx+c\\\\
 & =\ln(\cos x)+\ln(\sec x+\tan x)-\sin x+c\\\\
 & =\ln(\cos x(\sec x+\tan x))-\sin x+c\\\\
(1+\sin x)^{2}y & =\ln(1+\sin x)-\sin x+c\\\\
y & =\frac{\ln(1+\sin x)-\sin x+c}{(1+\sin x)^{2}}
\end{aligned}$$

\emph{Riccati's equation. }Any first-order differential equation of
the form:

$$\begin{aligned}
\frac{dy}{dx}+a_{2}(x)y^{2}+a_{1}(x)y+a_{0}(x) & =0\quad\tag{20}
\end{aligned}$$

in which $a_{0}(x),a_{1}(x),a_{2}(x)$ are continuous on an interval
$I=[a,b]$ and $a_{2}(x)\neq0$ on $I$ is called a \emph{Riccati
equation}. A number of elementary facts concerning the solutions of
such equations are given in the exercises which follow.

**Exercise.**
Let $y_{1}(x)$ be a particular solution of (20). Make the change
of variable $y=y_{1}+1/z$ to reduce to a first order \emph{linear}
equation in $z$ and hence deduce that the general solution of a Riccati
equation can be found as soon as a particular solution is known. 


*Solution.*

If we make the change of variable $y=y_{1}+1/z$ in the Riccati equation,
we have:

$$\begin{aligned}
\frac{d}{dx}\left[y_{1}+\frac{1}{z}\right]+a_{2}\left(y_{1}+1/z\right)^{2}+a_{1}(y_{1}+1/z)+a_{0} & =0\\\\
y_{1}'-\frac{1}{z^{2}}z'+a_{2}\left(y_{1}^{2}+2\frac{y_{1}}{z}+\frac{1}{z^{2}}\right)+a_{1}(y_{1}+\frac{1}{z})+a_{0} & =0\\\\
z^{2}y_{1}'-z'+z^{2}a_{2}y_{1}^{2}+2za_{2}y_{1}+a_{2}+z^{2}a_{1}y_{1}+a_{1}z+z^{2}a_{0} & =0\\\\
z^{2}(y_{1}'+a_{2}y_{1}^{2}+a_{1}y_{1}+a_{0})-z'+2za_{2}y_{1}+a_{2}+a_{1}z & =0
\end{aligned}$$

But, since $y_{1}$ is a particular solution of the ODE, $y_{1}'+a_{2}y_{1}^{2}+a_{1}y_{1}+a_{0}=0$.
Consequently,

$$\begin{aligned}
z'-(2a_{2}(x)+a_{1}(x))z & =a_{2}(x)
\end{aligned}$$

This is a first order linear differential equation in $z$. 

Use the technique in the preceding exercise to find the general solution
of each of the following Riccati equations:

**Exercise.**
$y'-xy^{2}+(2x-1)y=x-1$, particular solution $y=1$.


*Solution.*

Substituing $y=y_{p}+\frac{1}{z}$, we get:

$$\begin{aligned}
y_{p}'-\frac{1}{z^{2}}z'-x\left(1+\frac{1}{z}\right)^{2}+(2x-1)\left(1+\frac{1}{z}\right) & =x-1\\\\
z^{2}(y_{p}'-x+(2x-1)-(x-1))-z'-2xz-x+(2x-1)z & =0
\end{aligned}$$

Since $y_{p}'-xy_{p}+(2x-1)y_{p}-(x-1)=0$, we have:

$$\begin{aligned}
z'+2xz+x-2xz+z & =0\\\\
z'+z & =-x
\end{aligned}$$

The integrating factor for this equation is:

$$\begin{aligned}
\mu(x) & =e^{\int p(x)dx}\\\\
 & =e^{\int dx}=e^{x}
\end{aligned}$$

Multiplying both sides of the differential equation by $e^{x}$, we
have:

$$\begin{aligned}
e^{x}z'+e^{x}z & =-xe^{x}\\\\
d(e^{x}z) & =-xe^{x}dx\\\\
\int d(e^{x}z) & =-\int xe^{x}dx+c\\\\
 & =-(xe^{x}-\int e^{x}dx)+c\\\\
 & =-xe^{x}+e^{x}+c\\\\
z & =-x+1+ce^{-x}\\\\
\frac{1}{y-1} & =1-x+ce^{-x}\\\\
y & =1+\frac{1}{1-x+ce^{-x}}
\end{aligned}$$

**Exercise.**
$y'+xy^{2}-2x^{2}y+x^{3}=x+1$, particular solution $y=x-1$.


*Solution.*

Since the particular solution $y_{p}=x-1$ satisfies the given differential
equation:

$$\begin{aligned}
y_{p}'+xy_{p}^{2}-2x^{2}y_{p}+x^{3} & =x+1
\end{aligned}$$

Substituting $y=y_{p}+\frac{1}{z}=(x-1)+\frac{1}{z}$, we get:

$$\begin{aligned}
y_{p}'-\frac{1}{z^{2}}z'+x\left(y_{p}+\frac{1}{z}\right)^{2}-2x^{2}\left(y_{p}+\frac{1}{z}\right)+x^{3} & =x+1\\\\
z^{2}y_{p}'-z'+x(zy_{p}+1)^{2}-2x^{2}(z^{2}y_{p}+z)+x^{3}z^{2} & =(x+1)z^{2}\\\\
z^{2}y_{p}'-z'+x(z^{2}y_{p}^{2}+2zy_{p}+1)-2x^{2}z^{2}y_{p}-2x^{2}z+x^{3}z^{2} & =(x+1)z^{2}\\\\
\\{\text{Collecting terms in }z^{2}\\}\\\\
z^{2}\underbrace{(y_{p}'+xy_{p}^{2}-2x^{2}y_{p}+x^{3}-(x+1)}_{\text{Equals 0}} & =z'-2xzy_{p}-x+2x^{2}z\\\\
z'-2x(x-1)z+2x^{2}z & =x\\\\
z'+2xz & =x
\end{aligned}$$

The integrating factor $\mu(x)$ for the above differential equation
is:

$$\begin{aligned}
\mu(x) & =e^{\int2xdx}=e^{x^{2}}
\end{aligned}$$

Multiplying both sides of the equation by $e^{x^{2}}$, we get:

$$\begin{aligned}
z'e^{x^{2}}+2xe^{x^{2}}z & =xe^{x^{2}}\\\\
d(e^{x^{2}}z) & =xe^{x^{2}}dx\\\\
\int d(e^{x^{2}}z) & =\int xe^{x^{2}}dx+c\\\\
ze^{x^{2}} & =\frac{1}{2}\int2xe^{x^{2}}dx+c\\\\
 & \\{\text{Putting }u=x^{2}, du=2xdx\\}\\\\
 & =\frac{1}{2}\int e^{u}du+c\\\\
 & =\frac{e^{u}}{2}+c=\frac{e^{x^{2}}}{2}+c\\\\
z & =\frac{1}{2}+ce^{-x^{2}}\\\\
\frac{1}{y-(x-1)} & =\frac{1+ce^{-x^{2}}}{2}\\\\
y & =(x-1)+\frac{2}{1+ce^{-x^{2}}}
\end{aligned}$$

**Exercise.**
$2y'-(y/x)^{2}-1=0$; particular solution $y=x$.


*Solution.*

Let $y_{p}$ be the particular solution of the differential equation,
then it follows that:

$$\begin{aligned}
2y_{p}'-(y_{p}/x)^{2}-1 & =0
\end{aligned}$$

Making the substitution $y=y_{p}+1/z$, we get:

$$\begin{aligned}
2\left(y_{p}'-\frac{1}{z^{2}}z'\right)-\frac{1}{x^{2}}\left(y_{p}+\frac{1}{z}\right)^{2}-1 & =0\\\\
2z^{2}y_{p}'-2z'-\frac{1}{x^{2}}(y_{p}z+1)^{2}-z^{2} & =0\\\\
2z^{2}y_{p}'-2z'-\frac{1}{x^{2}}(y_{p}^{2}z^{2}+2y_{p}z+1)-z^{2} & =0\\\\
z^{2}\underbrace{\left(2y_{p}'-\frac{y_{p}^{2}}{x^{2}}-1\right)}_{\text{Equals 0}} & =2z'+\frac{2}{x^{2}}y_{p}z+\frac{1}{x^{2}}\\\\
z'+\frac{1}{x}z & =-\frac{1}{2x^{2}}
\end{aligned}$$

The integrating factor for the above differential equation is:

$$\begin{aligned}
\mu(x) & =e^{\int p(x)dx}\\\\
 & =e^{\int\frac{dx}{x}}\\\\
 & =x
\end{aligned}$$

Multiplying both sides of the differential equation by $x$, we have:

$$\begin{aligned}
xz'+z & =-\frac{1}{2x}\\\\
d(xz) & =-\frac{dx}{2x}\\\\
\int d(xz) & =-\int\frac{dx}{2x}+c\\\\
xz & =-\frac{1}{2}\ln x+c\\\\
z & =\frac{c-\ln x}{2x}\\\\
\frac{1}{y-x} & =\frac{c-\ln x}{2x}\\\\
y & =x+\frac{2x}{c-\ln x}
\end{aligned}$$

**Exercise.**
$y'+y^{2}-(1+2e^{x})y+e^{2x}=0$, particular solution $y=e^{x}$.


*Solution.*

Since $y_{p}$ is a particular solution of the differential equation,
we have:

$$\begin{aligned}
y_{p}'+y_{p}^{2}-(1+2e^{x})y_{p}+e^{2x} & =0
\end{aligned}$$

Making the substitution $y=y_{p}+\frac{1}{z}$, we have:

$$\begin{aligned}
y_{p}'-\frac{1}{z^{2}}z'+\left(y_{p}+\frac{1}{z}\right)^{2}-(1+2e^{x})\left(y_{p}+\frac{1}{z}\right)+e^{2x} & =0\\\\
z^{2}y_{p}'-z'+\left(zy_{p}+1\right)^{2}-(1+2e^{x})(z^{2}y_{p}+z)+z^{2}e^{2x} & =0\\\\
z^{2}y_{p}'-z'+\left(z^{2}y_{p}^{2}+2zy_{p}+1\right)-(1+2e^{x})(z^{2}y_{p}+z)+z^{2}e^{2x} & =0\\\\
z^{2}\underbrace{(y_{p}'+y_{p}^{2}-(1+2e^{x})y_{p}+e^{2x})}_{\text{Equals 0}} & =z'-2ze^{x}-1+(1+2e^{x})z\\\\
z'+z & =1
\end{aligned}$$

The integrating factor is $e^{\int dx}=e^{x}$. Multiplying both sides
of the equation by $e^{x}$, we have:

$$\begin{aligned}
d[e^{x}z] & =e^{x}dx\\\\
e^{x}z & =e^{x}+c\\\\
z & =1+ce^{-x}\\\\
\frac{1}{y-e^{x}} & =1+ce^{-x}\\\\
y & =e^{x}+\frac{1}{1+ce^{-x}}
\end{aligned}$$

**Exercise.**
$y'-(\sin^{2}x)y^{2}+\frac{1}{\sin x\cos x}y+\cos^{2}x=0$, particular
solution $y=\frac{\cos x}{\sin x}$.

*Solution.*

Since $y_{p}$ is a particular solution of the above equation, we
have:

$$\begin{aligned}
y_{p}'-(\sin^{2}x)y_{p}^{2}+\frac{1}{\sin x\cos x}y_{p}+\cos^{2}x & =0
\end{aligned}$$

Substituting $y=y_{p}+\frac{1}{z},$ we have:

$$\begin{aligned}
y_{p}'-\frac{1}{z^{2}}z'-\sin^{2}x\left(y_{p}+\frac{1}{z}\right)^{2}+\frac{1}{\sin x\cos x}\left(y_{p}+\frac{1}{z}\right)+\cos^{2}x & =0\\\\
z^{2}y_{p}'-z'-\sin^{2}x(y_{p}z+1)^{2}+\frac{1}{\sin x\cos x}(y_{p}z^{2}+z)+z^{2}\cos^{2}x & =0\\\\
z^{2}y_{p}'-z'-\sin^{2}x(y_{p}^{2}z^{2}+2y_{p}z+1)+\frac{1}{\sin x\cos x}(y_{p}z^{2}+z)+z^{2}\cos^{2}x & =0\\\\
z^{2}\underbrace{(y_{p}'-\sin^{2}xy_{p}^{2}+\frac{1}{\sin x\cos x}y_{p}+\cos^{2}x)}_{\text{Equals 0}} & =z'+2\sin^{2}xy_{p}z+\sin^{2}x-\frac{1}{\sin x\cos x}z\\\\
z'+\left(2\sin x\cos x-\frac{2}{2\sin x\cos x}\right)\cdot z & =-\sin^{2}x\\\\
z'+(\sin2x-2cosec(2x))z & =-\sin^{2}x
\end{aligned}$$

The integrating factor is:

$$\begin{aligned}
\mu(x) & =e^{\int\sin2xdx-2\int cosec(2x)dx}\\\\
 & =e^{-\frac{\cos2x}{2}-2\frac{\ln|cosec(2x)-\cot(2x)|}{2}}\\\\
 & =e^{-\frac{1}{2}\cos(2x)}\cdot\frac{1}{\csc(2x)-\cot2x}\\\\
 & =e^{-\frac{1}{2}\cos(2x)}\cdot\frac{\sin2x}{1-\cos2x}\\\\
 & =e^{-\frac{1}{2}\cos(2x)}\frac{2\sin x\cos x}{2\sin^{2}x}\\\\
 & =e^{-\frac{1}{2}\cos(2x)}\frac{\cos x}{\sin x}
\end{aligned}$$

Multiplying by the integrating factor on both sides, we get:

$$\begin{aligned}
d\left[e^{-\frac{1}{2}\cos(2x)}\frac{\cos x}{\sin x}\cdot z\right] & =-\sin^{2}x\cdot\frac{\cos x}{\sin x}\cdot e^{-\frac{1}{2}\cos2x}dx\\\\
 & =-\frac{1}{2}\sin2x\cdot e^{-\frac{1}{2}\cos2x}dx\\\\
\int d\left[e^{-\frac{1}{2}\cos(2x)}\frac{\cos x}{\sin x}\cdot z\right] & =-\frac{1}{2}\int\sin2x\cdot e^{-\frac{1}{2}\cos2x}dx+c\\\\
 & \\{\text{Put }-(1/2)\cos2x=u, (\sin2x)dx=du\\} \\\\
 & =-\frac{1}{2}\int e^{u}du+c\\\\
e^{-\frac{1}{2}\cos(2x)}\frac{\cos x}{\sin x}\cdot z & =-\frac{1}{2}e^{-\frac{1}{2}\cos(2x)}+c\\\\
z & =\frac{\sin x}{\cos x}\left[ce^{\frac{1}{2}\cos(2x)}-\frac{1}{2}\right]\\\\
\frac{1}{y-(\cos x/\sin x)} & =\frac{\sin x}{\cos x}\left[ce^{\frac{1}{2}\cos(2x)}-\frac{1}{2}\right]\\\\
y & =\frac{\cos x}{\sin x}+\frac{\sin x}{\cos x}\cdot\frac{1}{(1/2)-ce^{(1/2)\cos2x}}
\end{aligned}$$

**Exercise.**
Let $y_{1}(x)$ and $y_{2}(x)$ be two particular solutions of the
Riccati equation. Show that the general solution of the equation is:

$$\begin{aligned}
\frac{y-y_{1}}{y-y_{2}} & =ce^{\int a_{2}(x)(y_{2}-y_{1})dx}
\end{aligned}$$

where $c$ is an arbitrary constant. 

Hint: Consider the expression :

\[
\frac{y'-y_{1}'}{y-y_{1}}-\frac{y'-y_{2}'}{y-y_{2}}
\]

\emph{Proof.}

The Riccati equation is given by:

$$\begin{aligned}
y'+a_{2}(x)y^{2}+a_{1}(x)y+a_{0}(x) & =0\quad\tag{21}
\end{aligned}$$

Since $y_{1}$ and $y_{2}$ satisfy this differential equation, we
must have:

$$\begin{aligned}
y_{1}'+a_{2}(x)y_{1}^{2}+a_{1}(x)y_{1}+a_{0}(x) & =0\quad\tag{22}\\\\
y_{2}'+a_{2}(x)y_{2}^{2}+a_{1}(x)y_{2}+a_{0}(x) & =0\quad\tag{23}
\end{aligned}$$

Subtracting (22) and (23) from expression (21), we find that:

$$\begin{aligned}
y'-y_{1}'+a_{2}(x)(y^{2}-y_{1}^{2})+a_{1}(x)(y-y_{1}) & =0\\\\
\\{\text{Dividing throughout by }(y-y_{1})\\}\\\\
\frac{y'-y_{1}'}{y-y_{1}} & =-a_{2}(x)(y+y_{1})-a_{1}(x)
\end{aligned}$$

And similarly,

$$\begin{aligned}
\frac{y'-y_{2}'}{y-y_{2}} & =-a_{2}(x)(y+y_{2})-a_{1}(x)
\end{aligned}$$

Subtracting the last two equations, we find that:

$$\begin{aligned}
\frac{y'-y_{1}'}{y-y_{1}}-\frac{y'-y_{2}'}{y-y_{2}} & =a_{2}(x)(y_{2}-y_{1})
\end{aligned}$$


\subsubsection*{Existence and uniqueness of solutions; Initial Value Problems(IVP).}

On the strength of the results of the preceding section, we can assert
that every first order linear differential equation which is defined
on the interval $I=[a,b]$ has solutions. In fact, it has infinitely
many, one for each value of $c$, and the general solution of such
an equation therefore is a one-parameter family of plane curves which
traverse the strip of the $xy$-plane determined $I=[a,b]$ as shown
in the figure below. Even more important, it is easy to see that there
is a solution curve passing through any pre-assigned point $(x_{0},y_{0})$
in this strip, since we can solve

$$\begin{aligned}
a_{1}(x)\frac{dy}{dx}+a_{0}(x)y & =h(x)
\end{aligned}$$

for $c$, when $x=x_{0},y=y_{0}$.

The problem of finding a function $y=f(x)$ which is a solution of
the first-order linear differential equation and which also satisfies
this condition is called the \emph{initial-value problem }for the
given equation. This terminology is designed to serve as a reminder
of the physical interpretation which views such a solution as the
path, or trajectory of a moving particle at the point $(x_{0},y_{0})$
and whose subsequent motion was governed by the equation in question.
In these terms, our earlier results can be summarized by saying that
every initial value problem involving a first-order linear differential
equation has \emph{atleast one solution}.

At this point, it is only natural to ask whether or not such a problem
can admit more than one solution. This is the so-called \emph{uniqueness}
problem for the first-order linear differential equations, and is
anything, but an ideal question. Indeed, in applications of differential
equations to the natural sciences it is often essential to be able
to guarantee that the problem being investigated has a unique solution,
since any attempt to predict the future behavior of a physical system
governed by an initial value relies upon this knowledge. In the case,
at hand, it is not difficult to show that the desired uniqueness holds,
and hence the above assertion can be amended to read as follows:
\begin{thm*}
Every initial-value problem involving a first-order linear differential
equation has precisely one solution.
\end{thm*}
The general theory of linear differential equations can properly be
said to begin with this theorem which generalizes this result to $n$th
order equations. In the special case treated above, the theorem was
proved by the simple expedient of exhibiting all of the solutions
at issue. Unfortunately, it is impossible to give an argument of this
type for equations of higher order, and though the asserted theorem
is true, its proof is not conspicuously easy. Thus, rather than become
involved in a long and arid discussion at this time, we content ourselves
with a formal statement of the result. 
\begin{thm*}
(Existence and uniqueness theorem for linear differential equations).
Let

$$\begin{aligned}
a_{n}(x)\frac{d^{n}y}{dx^{n}}+\ldots+a_{0}(x) & =h(x)\quad\tag{24}
\end{aligned}$$

be a normal $n$th order differential equation defined on an interval
$I$, and let $x_{0}$ be any point in $I=[a,b]$. Then, if $y_{0}$,
$y_{1}$, $\ldots$, $y_{n-1}$ are arbitrary real numbers, there
exists one and only one solution $y(x)$ of with the property that 

\[
y(x_{0})=y_{0},y'(x_{0})=y_{1},\ldots,y^{(n-1)}(x_{0})=y_{n-1}\quad\tag{25}
\]

As in the case of first-order equations, the problem of finding a
solution of (24) which satisfies the $n$ additional conditions given
in (25) is called an initial-value problem with initial conditions:

\[
y(x_{0})=y_{0},y'(x_{0})=y_{1},\ldots,y^{(n-1)}(x_{0})=y_{n-1}
\]

It is also worth noting that the theorem can be phrased in the language
of linear operators, in which case it assumes the following suggestive
form:

\emph{If $L:\mathcal{C}^{n}([a,b])\to\mathcal{C}([a,b])$ is a $n$th-order
linear differential operator, there exists a unique inverse operator
$G:\mathcal{C}([a,b])\to\mathcal{C}^{n}([a,b])$ such that:}

$$\begin{aligned}
L([G(h)] & =h,\quad\text{for all }h \text{ in }\mathcal{C}([a,b])
\end{aligned}$$

and 

\[
G(h)(x_{0})=y_{0},G(h)'(x_{0})=y_{1},\ldots,G(h)^{(n-1)}(x_{0})=y_{n-1}
\]

When stated in these terms, it is clear that the task of solving an
initial-value problem for a linear differential equation comes down
to finding an explicit form for the inverse operator $G$, since once
$G$ is known, the problem:

$$\begin{aligned}
Ly & =h
\end{aligned}$$

\[
y(x_{0})=y_{0},y'(x_{0})=y_{1},\ldots,y^{(n-1)}(x_{0})=y_{n-1}
\]

can be solved by computing the value of $G(h)$. This point of view
will be exploited in later chapters where much of our work will be
directed towards finding $G$ for specific classes of linear differential
operators. As we shall see, $G$ will turn out to be an integral operator. 

Find the solution of each of the following initial-value problems
and specify the domain of the solution.
\end{thm*}
**Exercise.**
$xy'+2y=0$, $y(1)=-1$.

*Solution.*

Bringing the equation to the form $y'+p(x)y=q(x)$, we have:

$$\begin{aligned}
y'+2\frac{1}{x}y & =0
\end{aligned}$$

The integrating factor $\mu(x)$ is given by:

$$\begin{aligned}
\mu(x) & =e^{2\int p(x)dx}\\\\
 & =e^{2\int\frac{dx}{x}}\\\\
 & =x^{2}
\end{aligned}$$

Multiplying both sides of the equation by $x^{2}$, we get:

$$\begin{aligned}
x^{2}y'+2xy & =0\\\\
d(x^{2}y) & =0\\\\
\int d(x^{2}y) & =c\\\\
y & =\frac{c}{x^{2}}
\end{aligned}$$

Since $y(1)=-1$, we have: $c=-1$. Therefore,

$$\begin{aligned}
y & =-\frac{1}{x^{2}}
\end{aligned}$$

**Exercise.**
$(\sin x)y'+(\cos x)y=0,\quad y\left(\frac{3\pi}{4}\right)=2$.

*Solution.*

Observe that $\frac{d}{dx}(\sin x\cdot y)=\sin x\cdot\frac{dy}{dx}+\cos x\cdot y=\sin x\cdot y'+\cos x\cdot y$.
We have:

$$\begin{aligned}
d(\sin x\cdot y) & =0\\\\
\int d(\sin x\cdot y) & =c\\\\
y & =\frac{c}{\sin x}
\end{aligned}$$

The given IVP is $y(3\pi/4)=2$. We have:

$$\begin{aligned}
\frac{c}{(1/\sqrt{2})} & =2\\\\
c & =\sqrt{2}
\end{aligned}$$

Hence, the particular solution to this IVP is:

$$\begin{aligned}
y & =\frac{\sqrt{2}}{\sin x}
\end{aligned}$$

**Exercise.**
$2y'+3y=e^{-x}$, $y(-3)=-3$.

*Solution.*

Bringing the equation into the form $y'+p(x)y=q(x)$, we have:

$$\begin{aligned}
y'+\frac{3}{2}y & =\frac{1}{2}e^{-x}
\end{aligned}$$

The integrating factor $\mu(x)$ is given by:

$$\begin{aligned}
\mu(x) & =e^{\int\frac{3}{2}dx}\\\\
 & =e^{3x/2}
\end{aligned}$$

Multiplying both sides of the differential equation by $e^{3x/2}$,
we have:

$$\begin{aligned}
e^{3x/2}y'+\frac{3}{2}e^{3x/2}y & =\frac{1}{2}e^{x/2}\\\\
d(e^{3x/2}y) & =\frac{1}{2}e^{x/2}dx\\\\
\int d(e^{3x/2}y) & =\frac{1}{2}\int e^{x/2}dx+c\\\\
ye^{3x/2} & =e^{x/2}+c\\\\
y & =e^{-x}+ce^{-3x/2}
\end{aligned}$$

Since $y(-3)=-3$, we have:

$$\begin{aligned}
e^{-3}+ce^{-9/2} & =-3\\\\
c & =\frac{-3-\frac{1}{e^{3}}}{(1/e^{9/2})}\\\\
 & =-(3e^{9/2}+e^{3/2})
\end{aligned}$$

Hence, the particular solution to this IVP is:

$$\begin{aligned}
y & =e^{-x}-(3e^{9/2}+e^{3/2})e^{-3x/2}
\end{aligned}$$

**Exercise.**
$(x^{2}+1)y'-(1-x^{2})y=e^{-x}$, $y(-2)=0$.

*Solution.*

We have:

$$\begin{aligned}
y'-\frac{1-x^{2}}{1+x^{2}}y & =\frac{e^{-x}}{1+x^{2}}
\end{aligned}$$

The integrating factor is:

$$\begin{aligned}
\mu(x) & =e^{\int p(x)dx}\\\\
 & =\exp\left[-\int\frac{1-x^{2}}{1+x^{2}}dx\right]\\\\
 & =\exp\left[-\int\left\{ -1+\frac{2}{1+x^{2}}\right\} dx\right]\\\\
 & =\exp\left[\int dx-\int\frac{2dx}{1+x^{2}}\right]\\\\
 & =\exp(x-2\arctan x)\\\\
 & =\frac{e^{x}}{e^{2\arctan x}}
\end{aligned}$$

Multiplying both sides of the differential equation by $\mu(x)$,
we get:

$$\begin{aligned}
d\left(\frac{e^{x}}{e^{2\arctan x}}\cdot y\right) & =\frac{dx}{(1+x^{2})e^{2\arctan x}}\\\\
\int d\left(\frac{e^{x}}{e^{2\arctan x}}\cdot y\right) & =\int\frac{dx}{(1+x^{2})e^{2\arctan x}}+c\\\\
 & \\{\text{Put }u=\arctan x,du=\frac{dx}{1+x^{2}}\\}\\\\
 & =\int e^{-2u}du+c\\\\
 & =\frac{e^{-2u}}{-2}+c\\\\
 & =\frac{-1}{2}\frac{1}{e^{2\arctan x}}+c\\\\
y\cdot e^{x} & =-\frac{1}{2}+ce^{2\arctan x}\\\\
y & =e^{-x}(ce^{2\arctan x}-\frac{1}{2})
\end{aligned}$$


###Dimensions of the solution space.}

We cna use the existence and the uniqueness theorem to give a simple
and elegant proof of the fact, that the dimension of the solution
space of every homogenous linear differential equation is equal to
the order of the equation. 
\begin{thm*}
The solution space of any $n$th order homogenous linear differential
equation

$$\begin{aligned}
a_{n}(x)\frac{d^{n}y}{dx^{n}}+\ldots+a_{0}(x)y & =0\quad\tag{26}
\end{aligned}$$

defined on an interval $I=[a,b]$ is an n-dimensional subspace of
$\mathcal{C}([a,b])$.
\end{thm*}
\emph{Proof.}

Let $x_{0}$ be a fixed point in $I=[a,b]$. Then, by the existence
and uniqueness theorem, we know that this equation admits the unique
solutions $y_{1}(x),y_{2}(x),\ldots,y_{n}(x_{0})$ satisfying the
initial conditions:

$\begin{array}{cccc}
y_{1}(x_{0})=1, & y_{1}'(x_{0})=0, & \ldots, & y_{1}^{(n-1)}(x_{0})=0\\\\
y_{2}(x_{0})=0, & y_{2}'(x_{0})=1, & \ldots, & y_{2}^{(n-1)}(x_{0})=0\\\\
\vdots\\\\
y_{n}(x_{0})=0, & y_{n}'(x_{0})=0 & \ldots, & y_{n}^{(n-1)}(x_{0})=1
\end{array}\quad\tag{27}$

In other words, $y_{1}(x),\ldots,y_{n}(x)$ have the property that
the vectors 

$$\begin{aligned}
(y_{i}(x_{0}),y_{i}'(x_{0}),\ldots,y_{i}^{(n-1)}(x_{0})) & =\mathbf{e}_{i}\quad\tag{28}
\end{aligned}$$

for all $i=1,2,\ldots,n$ are the standard basis vectors in $\mathbf{R}^{n}$.
We assert that these solutions form a basis for the solution space.

Indeed, suppose that $c_{1},c_{2},\ldots,c_{n}$ are real numbers
such that:

$$\begin{aligned}
c_{1}y_{1}(x)+\ldots+c_{n}y_{n}(x) & \equiv0\quad\tag{29}
\end{aligned}$$

on $[a,b]$. Then this identity, together with its first $n-1$ derivatives,
yields the system:

$$\begin{aligned}
c_{1}y_{1}(x)+\ldots+c_{n}y_{n}(x) & \equiv0\\\\
c_{1}y_{1}'(x)+\ldots+c_{n}y_{n}'(x) & \equiv0\\\\
\vdots\\\\
c_{1}y_{1}^{(n-1)}(x)+\ldots+c_{n}y_{n}^{(n-1)}(x) & \equiv0\quad\tag{30}
\end{aligned}$$

Setting $x=x_{0}$, we obtain:

$$\begin{aligned}
c_{1}y_{1}(x_{0})+\ldots+c_{n}y_{n}(x_{0}) & \equiv0\\\\
c_{1}y_{1}'(x_{0})+\ldots+c_{n}y_{n}'(x_{0}) & \equiv0\\\\
\vdots\\\\
c_{1}y_{1}^{(n-1)}(x_{0})+\ldots+c_{n}y_{n}^{(n-1)}(x_{0}) & \equiv0\quad\tag{31}
\end{aligned}$$

And now (27) implies that $c_{1}=c_{2}=\ldots=c_{n}=0$. Thus, $y_{1}(x),y_{2}(x),\ldots,y_{n}(x)$
are linearly independent in $\mathcal{C}([a,b])$.

It remains to prove that every solution of (26) can be written as
a linear combination of $y_{1}(x),y_{2}(x),\ldots,y_{n}(x)$. 

Since $y_{1}$, $y_{2}$, $\ldots$, $y_{n}$ are solutions of the
linear differential equation (26), and the initial conditions $(y_{i}(x_{0}),y_{i}'(x_{0}),\ldots,y_{i}^{(n-1)}(x_{0}))=\mathbf{e}_{i}$ 

$$\begin{aligned}
Ly_{1}(x_{0}) & =0\\\\
Ly_{2}(x_{0}) & =0\\\\
\vdots\\\\
Ly_{n}(x_{0}) & =0
\end{aligned}$$

Every linear combination of $(y_{1}(x_{0}),\ldots,y_{n}(x_{0}))$
also satisfies the same initial value problem:

$$\begin{aligned}
L(\gamma_{1}y_{1}(x_{0})+\ldots+\gamma_{n}y_{n}(x_{0})) & =0\quad\tag{32}
\end{aligned}$$

Hence, any solution $y(x)$ of the initial value problem $Ly=x$,
$(y_{i}(x_{0}),y_{i}'(x_{0}),\ldots,y_{i}^{(n-1)}(x_{0}))=\mathbf{e}_{i}$
must be of the form $\sum\gamma_{i}y_{i}(x)$. 

This closes the proof.
**Example.**
The second-order equation

$$\begin{aligned}
\frac{d^{2}y}{dx^{2}}-y & =0\quad\tag{33}
\end{aligned}$$

has a $2$-dimensional solution space. It is easy to see that $y_{1}(x)=\frac{e^{x}+e^{-x}}{2}$,
and $y_{2}(x)=\frac{e^{x}-e^{-x}}{2}$ are solutions to the initial
value problems:

\[
y(0)=1,\quad y'(0)=0\quad\tag{34}
\]

and 

\[
y(0)=0,\quad y'(0)=1\quad\tag{35}
\]

Thus, $y_{1}(x)$ and $y_{2}(x)$ form a basis for the solution space
of the differential equation. Hence, the general solution to (33)
is given by:

$$\begin{aligned}
y(x) & =c_{1}y_{1}(x)+c_{2}y_{2}(x)
\end{aligned}$$

%
**Example.**
The functions 

$$\begin{aligned}
y_{1}(x) & =e^{x},\quad y_{2}(x)=e^{-x}
\end{aligned}$$

provide a second pair of solutions to the equation (33) and the initial
value problem:

$$\begin{aligned}
y_{1}(0)=1, & y_{1}'(0)=1\\\\
y_{2}(0)=1, & y_{2}'(0)=-1
\end{aligned}$$

and since the vectors $(1,1)$ and $(1,-1)$ are linearly independent
in $\mathbf{R}^{2}$, $e^{x}$ and $e^{-x}$ also form a basis for
the solution space of the equation. It follows that the general solution
can also be written as:

$$\begin{aligned}
y & =c_{1}e^{x}+c_{2}e^{-x}
\end{aligned}$$

\begin{cor*}
Let $y_{1}(x),\ldots,y_{n}(x)$ be functions in $\mathcal{C}[a,b]$,
each of which possesses derivatives upto order $n-1$ everywhere in
$[a,b]$ and suppose that at some point $x_{0}$ in $[a,b]$, the
vectors:

\[
y_{i}(x_{0}),y_{i}'(x_{0}),\ldots,y_{i}^{(n-1)}(x_{0}),\quad i=1,2,\ldots,n
\]
 are linearly independent in $\mathbf{R}^{n}$. Then, $y_{1}(x),y_{2}(x),\ldots,y_{n}(x)$
are linearly independent in $\mathcal{C}[a,b]$.
\end{cor*}

###The Wronskian.}

In the preceding section, we proved that $y_{1},y_{2},\ldots,y_{n}$
are linearly independent functions in $\mathcal{C}^{n-1}[a,b]$ whenever
there exists a point $x_{0}$ in $[a,b]$ such that the vectors 

\[
y_{i}(x_{0}),y_{i}'(x_{0}),\ldots,y_{i}^{(n-1)}(x_{0}),\quad i=1,2,\ldots,n\quad\tag{36}
\]

are linearly independent in $\mathbf{R}^{n}$. For our present purposes,
this result can be stated more conveniently in terms of the determinant
of a certain matrix, as follows :

Let $y_{1},y_{2},\ldots,y_{n}$ be arbitrary functions in $\mathcal{C}^{n-1}[a,b]$
and for each $x\in[a,b]$, consider the matrix :

\[
\left[\begin{array}{cccc}
y_{1}(x) & y_{2}(x) & \ldots & y_{n}(x)\\\\
y_{1}'(x) & y_{2}'(x) & \ldots & y_{n}'(x)\\\\
\vdots &  & \ddots\\\\
y_{1}^{(n-1)}(x) & y_{2}^{(n-1)}(x) & \ldots & y_{n}^{(n-1)}(x)
\end{array}\right]\quad\tag{37}
\]

Then, (37) defines a function on the interval $[a,b]$ whose value
at $x$ is the indicated matrix, and by forming the determinant of
the matrix we obtain a real-valued function on $[a,b]$ called the
\emph{Wronskian} of $y_{1},y_{2},\ldots,y_{n}$. This function will
be denoted by $W[y_{1},\ldots,y_{n}]$ to indicate its dependence
on $y_{1},\ldots,y_{n}$ and its value at $x$ by $W[y_{1}(x),\ldots,y_{n}(x)]$.
In short the Wronskian of $y_{1},\ldots,y_{n}$ is the real-valued
function whose defining equation is:

$$\begin{aligned}
W[y_{1}(x),\ldots,y_{n}(x)] & =\left|\begin{array}{cccc}
y_{1}(x) & y_{2}(x) & \ldots & y_{n}(x)\\\\
y_{1}'(x) & y_{2}'(x) & \ldots & y_{n}'(x)\\\\
\vdots &  & \ddots\\\\
y_{1}^{(n-1)}(x) & y_{2}^{(n-1)}(x) & \ldots & y_{n}^{(n-1)}(x)
\end{array}\right|\quad\tag{38}
\end{aligned}$$

For example,

$$\begin{aligned}
W[x,\sin x] & =\left|\begin{array}{cc}
x & \sin x\\\\
1 & \cos x
\end{array}\right|\\\\
 & =x\cos x-\sin x
\end{aligned}$$

and 

$$\begin{aligned}
W[x,2x] & =\left|\begin{array}{cc}
x & 2x\\\\
1 & 2
\end{array}\right|\\\\
 & =0
\end{aligned}$$

We now recall that the determinant of an $n\times n$ matrix is non-zero
if and only if the columns of the matrix are linearly independent
vectors in $\mathbf{R}^{n}$. Thus, the Wronskian of $y_{1},\ldots,y_{n}$
is different from zero, if and only if the columns are linearly independent
when $x=x_{0}$. But, for each $x_{0}\in[a,b]$, the columns of (38)
are none other than the vectors in (36), and therefore we have the
following theorem.
\begin{thm*}
(Sufficient condition for linear independence) The functions $y_{1},\ldots,y_{n}$
are linearly independent in $\mathcal{C}^{n-1}[a,b]$ and hence also
in $\mathcal{C}[a,b]$ whenever their Wronskian is not identically
equal to zero on $[a,b]$.
\end{thm*}
**Example.**
Since 

$$\begin{aligned}
W[e^{x},e^{-x}] & =\left|\begin{array}{cc}
e^{x} & e^{-x}\\\\
e^{x} & -e^{-x}
\end{array}\right|\\\\
 & =-1-1=2
\end{aligned}$$

the functions $e^{x}$ and $e^{-x}$ are linearly independent in $\mathbf{R}$.

%
**Example.**
The functions $x$, $x^{1/2}$, $x^{3/2}$ are linearly independent
on $\mathcal{C}[a,b]$ for any subinterval $[a,b]$ of the positive
$x$-axis since:

$$\begin{aligned}
W[x,x^{1/2},x^{3/2}] & =\left|\begin{array}{ccc}
x & x^{1/2} & x^{3/2}\\\\
1 & \frac{1}{2\sqrt{x}} & \frac{3}{2}x^{1/2}\\\\
0 & -\frac{1}{4}x^{-3/2} & \frac{3}{4}x^{-1/2}
\end{array}\right|\\\\
 & =x\left|\begin{array}{cc}
\frac{1}{2}x^{-1/2} & \frac{3}{2}x^{1/2}\\\\
-\frac{1}{4}x^{-3/2} & \frac{3}{2}x^{-1/2}
\end{array}\right|-\left|\begin{array}{cc}
x^{1/2} & x^{3/2}\\\\
-\frac{1}{4}x^{-3/2} & \frac{3}{4}x^{-1/2}
\end{array}\right|\\\\
 & =x\left(\frac{3}{8}x^{-1}+\frac{3}{8}x^{-1}\right)-\left(\frac{3}{4}+\frac{1}{4}\right)\\\\
 & =\frac{3}{4}-1\\\\
 & =-\frac{1}{4}
\end{aligned}$$

More generally, $x^{\alpha}$, $x^{\beta}$ and $x^{\gamma}$ are
linearly independent in $\mathcal{C}[a,b]$ if and only if $\alpha,\beta,\gamma$
are distinct real numbers.

The theorem above says that, if $W[y_{1},\ldots,y_{n}]\neq0$ on all
of $[a,b]$, then $y_{1},\ldots,y_{n}$ are linearly independent.
Equivalently, if $y_{1},y_{2},\ldots,y_{n}$ are linearly dependent,
then their Wronskian is identically equal to zero. However, the converse
of the theorem is not true. But, rather than abandon the search for
a converse to the above theorem, we may weaken our requirements and
ask whether it is possible to impose additional conditions on the
set of functions which, together with the vanishing of their Wronskian,
will imply linear dependence. This can in fact be done simply by requiring
that the functions be solutions of a homogenous linear differential
equation. 

\begin{thm*}
Let $y_{1},\ldots,y_{n}$ be solutions of a $n$th order homogeonous
linear differential equation

$$\begin{aligned}
Ly=\left[a_{n}(x)\frac{d^{n}}{dx^{n}}+\ldots+a_{0}(x)\right](y) & =0\quad\tag{39}
\end{aligned}$$

on the interval $I=[a,b]$ and suppose that $W[y_{1},\ldots,y_{n}]$
is identically zero on $[a,b]$. Then, $y_{1},y_{2},\ldots,y_{n}$
are linearly dependent in $\mathcal{C}[a,b]$.
\end{thm*}
\emph{Proof.}

Let $x_{0}$ be any point in $[a,b]$ and consider the system of equations:

$\begin{array}{cc}
c_{1}y_{1}(x_{0})+\ldots+c_{n}y_{n}(x_{0}) & =0\\\\
c_{1}y_{1}'(x_{0})+\ldots+c_{n}y_{n}'(x_{0}) & =0\\\\
\vdots\\\\
c_{1}y_{1}^{(n-1)}(x_{0})+\ldots+c_{n}y_{n}^{(n-1)}(x_{0}) & =0
\end{array}\quad\tag{40}$

in the unknowns $c_{1},c_{2},\ldots,c_{n}$. Since the Wronskian of
$y_{1},\ldots,y_{n}$ vanishes on $[a,b]$, the determinant of (40)
is zero, and its column vectors are linearly dependent. Consequently,
the system :

$$\begin{aligned}
\left[\begin{array}{cccc}
y_{1}(x_{0}) & y_{2}(x_{0}) & \ldots & y_{n}(x_{0})\\\\
y_{1}'(x_{0}) & y_{2}'(x_{0}) & \ldots & y_{n}'(x_{0})\\\\
\vdots &  & \ddots\\\\
y_{1}^{(n-1)}(x_{0}) & y_{2}^{(n-1)}(x_{0}) & \ldots & y_{n}^{(n-1)}(x_{0})
\end{array}\right]\left[\begin{array}{c}
c_{1}\\\\
c_{2}\\\\
\vdots\\\\
c_{n}
\end{array}\right] & =\left[\begin{array}{c}
0\\\\
0\\\\
\vdots\\\\
0
\end{array}\right]\quad\tag{41}
\end{aligned}$$

has more variables then the number of equations and the system is
under-determined.

$$\begin{aligned}
c_{1}\left[\begin{array}{c}
y_{1}(x_{0})\\\\
y_{1}'(x_{0})\\\\
\vdots\\\\
y_{1}^{(n-1)}(x_{0})
\end{array}\right]+\ldots+c_{n}\left[\begin{array}{c}
y_{n}(x_{0})\\\\
y_{n}'(x_{0})\\\\
\vdots\\\\
y_{n}^{(n-1)}(x_{0})
\end{array}\right] & =0\quad\tag{42}
\end{aligned}$$

For such a system, we must have $\bar{c_{1}},\bar{c_{2}},\ldots,\bar{c_{n}}\in\mathbf{R}$,
such that there exists $\bar{c_{i}}\neq0$. So, the system has a non-trivial
solution. Thus, it follows that the function:

$$\begin{aligned}
y(x) & =\sum_{i=1}^{n}\bar{c_{i}}y_{i}(x)\quad\tag{43}
\end{aligned}$$
 is solution to the differential equation consisting of (39) since
$Ly=L\left(\sum_{i=1}^{n}\bar{c_{i}}y_{i}(x)\right)=\sum_{i=1}^{n}\bar{c_{i}}Ly_{i}=0$
and moreover from (40) it follows that, they satisfy

the initial conditions:

\[
y(x_{0})=0,y'(x_{0})=0,\ldots,y^{(n-1)}(x_{0})=0\quad\tag{44}
\]

Hence, $y(x)$ is unique. But, the zero function is also a solution
to the problem and hence $y(x)$ must be equal to zero for all $x$.
So, the functions $y_{1}(x),\ldots,y_{n}(x)$ are linearly dependent. 

This closes the proof.

Once again, we have established a result that is stronger than the
one we advertised. For the above proof, we only made use of the fact,
that the Wronskian of $y_{1},\ldots,y_{n}$ vanished at a single point
in $[a,b]$ and hence the conclusion remains true under this more
restrictive hypotheses.
\begin{thm*}
(Necessary and sufficient condition for linear independence) A set
of solutions of the $n$th order homogenous linear differential equation
is linearly independent in $\mathcal{C}[a,b]$ and hence is a basis
for the solution space, if and only if its Wronskian \textbf{never}
vanishes on $[a,b]$.
\end{thm*}
By computing Wronskians, show that each of the following sets of functions
is linearly independent in $\mathcal{C}[a,b]$ for the indicated interval
$[a,b]$.
**Exercise.**
$1$, $e^{-x}$ and $2e^{2x}$ on any interval $I=[a,b]$.

*Solution.*

We have:

$$\begin{aligned}
W[1,e^{-x},2e^{2x}] & =\left|\begin{array}{ccc}
1 & e^{-x} & e^{2x}\\\\
0 & -e^{-x} & 2e^{2x}\\\\
0 & e^{-x} & 4e^{2x}
\end{array}\right|\\\\
 & =-e^{x}-2e^{x}\\\\
 & =-3e^{x}
\end{aligned}$$

The Wronskian is non-zero at some point in any interval in $\mathbf{R}$.
Consequently, $1$, $e^{-x}$ and $e^{2x}$ are linearly independent.
**Exercise.**
$e^{x}$ and $\sin2x$ on any interval $[a,b]$. 

*Solution.*

We have:

$$\begin{aligned}
W[e^{x},\sin2x] & =\left|\begin{array}{cc}
e^{x} & \sin2x\\\\
e^{x} & 2\cos2x
\end{array}\right|\\\\
 & e^{x}(2\cos2x-\sin2x)
\end{aligned}$$

The Wronskian is non-zero at atleast one point in an interval $[a,b]$.
Hence, by the sufficient condition for linear independence, $e^{x}$
and $\sin2x$ are linearly independent.
**Exercise.**
$1,x,x^{2},\ldots,x^{n}$ on any interval $I=[a,b]$.

*Solution.*

We have:

$$\begin{aligned}
W[1,x,x^{2},\ldots,x^{n}] & =\left|\begin{array}{ccccc}
1 & x & x^{2} & \ldots & x^{n}\\\\
0 & 1 & 2x & \ldots & nx^{n-1}\\\\
0 & 0 & 2 & \ldots & n(n-1)x^{n-2}\\\\
\vdots & \vdots & \vdots &  & \vdots\\\\
0 & 0 & 0 & \ldots & n!
\end{array}\right|\\\\
 & =1!\times2!\times3!\times\cdots\times n!
\end{aligned}$$

This quantity is non-zero. Consequently, by the sufficient condition
for linear independence, $1,x,x^{2},\ldots,x^{n}$ are linearly independent
over any interval $[a,b]$ in $\mathbf{R}$.

**Exercise.**
$\ln x$ and $x\ln x$ on $(0,\infty)$.

*Solution.*

We have:

$$\begin{aligned}
W[\ln x,x\ln x] & =\left|\begin{array}{cc}
\ln x & x\ln x\\\\
\frac{1}{x} & 1+\ln x
\end{array}\right|\\\\
 & =\ln x(1+\ln x)-\ln x\\\\
 & =(\ln x)^{2}
\end{aligned}$$

The Wronskian is non-zero at some point in any sub-interval of $(0,\infty)$.
Hence, $\ln x$ and $x\ln x$ are linearly independent. 

**Exercise.**
$x^{1/2}$ and $x^{1/3}$ on $(0,\infty)$.

*Solution.*

We have:

$$\begin{aligned}
W[x^{1/2},x^{1/3}] & =\left|\begin{array}{cc}
x^{1/2} & x^{1/3}\\\\
(1/2)x^{-1/2} & 1/3x^{-2/3}
\end{array}\right|\\\\
 & =\frac{1}{3}x^{\left(\frac{1}{2}-\frac{2}{3}\right)}-\frac{1}{2}x^{\left(\frac{1}{3}-\frac{1}{2}\right)}\\\\
 & =\frac{1}{3}x^{-\frac{1}{6}}-\frac{1}{2}x^{-\frac{1}{6}}\\\\
 & =-\frac{1}{6}x^{-1/6}
\end{aligned}$$

The function $\frac{1}{\sqrt[6]{x}}$ is non-zero on any interval
in $(0,\infty)$. Hence, by the sufficient condition on linear independence,
$x^{1/2}$ and $x^{1/3}$ are linearly independent.

**Exercise.**
$e^{ax}\sin bx$ and $e^{ax}\cos bx$ on any interval $[a,b]$.

*Solution.*

We have:

$$\begin{aligned}
W[e^{ax}\sin bx,e^{ax}\cos bx] & =\left|\begin{array}{cc}
e^{ax}\sin bx & e^{ax}\cos bx\\\\
ae^{ax}\sin bx+be^{ax}\cos bx & ae^{ax}\cos bx-be^{ax}\sin bx
\end{array}\right|\\\\
 & =e^{ax}\sin bx(ae^{ax}\cos bx-be^{ax}\sin bx)-e^{ax}\cos bx(ae^{ax}\sin bx+be^{ax}\cos bx)\\\\
 & =e^{2ax}[a\sin bx\cos bx-b\sin^{2}bx-a\cos bx\sin bx-b\cos^{2}bx]\\\\
 & =-be^{2ax}(\sin^{2}bx+\cos^{2}bx)\\\\
 & =-be^{2ax}
\end{aligned}$$

**Exercise.**
$e^{x}$, $e^{x}\sin x$ on any interval $[a,b]$.

*Solution.*

We have:

$$\begin{aligned}
W[e^{x},e^{x}\sin x] & =\left|\begin{array}{cc}
e^{x} & e^{x}\sin x\\\\
e^{x} & e^{x}\sin x+e^{x}\cos x
\end{array}\right|\\\\
 & =e^{2x}\left|\begin{array}{cc}
1 & \sin x\\\\
1 & \sin x+\cos x
\end{array}\right|\\\\
 & =e^{2x}(\sin x+\cos x-\sin x)\\\\
 & =e^{2x}\cos x
\end{aligned}$$

The Wronskian is non-zero at some point in any interval $[a,b]$ of
the real line. Consequently, $e^{x}$, $e^{x}\sin x$ are linearly
independent.
**Exercise.**
$e^{-x}$, $xe^{-x}$, $x^{2}e^{-x}$ on any interval $[a,b]$ of
the real line.

*Solution.*

We have:

$$\begin{aligned}
W[e^{-x},xe^{-x},x^{2}e^{-x}] & =\left|\begin{array}{ccc}
e^{-x} & xe^{-x} & x^{2}e^{-x}\\\\
-e^{-x} & e^{-x}-xe^{-x} & 2xe^{-x}-x^{2}e^{-x}\\\\
e^{-x} & -e^{-x}-(e^{-x}-xe^{-x}) & 2(e^{-x}-xe^{-x})-(2xe^{-x}-x^{2}e^{-x})
\end{array}\right|\\\\
 & =e^{-3x}\left|\begin{array}{ccc}
1 & x & x^{2}\\\\
-1 & 1-x & 2x-x^{2}\\\\
1 & -2+x & 2-4x+x^{2}
\end{array}\right|\\\\
 & \{R_{2}\leftarrow R_{2}+R_{1},R_{3}\leftarrow R_{3}-R_{1}\}\\\\
 & =e^{-3x}\left|\begin{array}{ccc}
1 & x & x^{2}\\\\
0 & 1 & 2x\\\\
0 & -2 & 2-4x
\end{array}\right|\\\\
 & =e^{-3x}((2-4x)+4x)\\\\
 & =2e^{-3x}
\end{aligned}$$

Hence, the wronskian never vanishes at any point of a subinterval
$[a,b]$ of the real-line. Consequently, $e^{-x}$, $xe^{-x}$ and
$x^{2}e^{-x}$ are linearly independent.
**Exercise.**
$1$, $\sin^{2}x$ and $1-\cos x$ on any interval $[a,b]$.

*Solution.*

We have:

$$\begin{aligned}
W[1,\sin^{2}x,1-\cos x] & =\left|\begin{array}{ccc}
1 & \sin^{2}x & 1-\cos x\\\\
0 & \sin2x & \sin x\\\\
0 & 2\cos2x & \cos x
\end{array}\right|\\\\
 & =\sin2x\cos x-2\cos2x\sin x\\\\
 & =\sin x-\cos2x\sin x\\\\
 & =\sin x(1-\cos2x)\\\\
 & =2\sin^{3}x
\end{aligned}$$

If we choose any subinterval $[a,b]$ of the real line, there exists
a point in $[a,b]$ such that the Wronskian is non-zero. Consequently,
by the sufficient condition on linear independence, $1$, $\sin^{2}x$
and $1-\cos x$ are linearly independent.
**Exercise.**
$\ln\left(\frac{x-1}{x+1}\right)$, $1$ on the interval $(-\infty,-1)$.

*Solution.*

We have:

$$\begin{aligned}
W[\ln((x-1)/(x+1)),1] & =\left|\begin{array}{cc}
\ln\frac{x-1}{x+1} & 1\\\\
\frac{x+1}{x-1}\cdot\frac{(x+1)-(x-1)}{(x+1)^{2}} & 0
\end{array}\right|\\\\
 & =\left|\begin{array}{cc}
\ln\frac{x-1}{x+1} & 1\\\\
\frac{x+1}{x-1}\cdot\frac{2}{(x+1)^{2}} & 0
\end{array}\right|\\\\
 & =\left|\begin{array}{cc}
\ln\frac{x-1}{x+1} & 1\\\\
\frac{2}{(x^{2}-1)} & 0
\end{array}\right|\\\\
 & =\frac{2}{x^{2}-1}
\end{aligned}$$

Since the Wronskian does not vanish in the interval $(-\infty,-1)$,
we conclude that the $\ln\frac{x-1}{x+1}$, $1$ are linearly independent
on this interval.
**Exercise.**
$\sqrt{1-x^{2}}$, $x$ on the interval $(-1,-1)$.

*Solution.*

We have:

$$\begin{aligned}
W[\sqrt{1-x^{2}},x] & =\left|\begin{array}{cc}
\sqrt{1-x^{2}} & x\\\\
\frac{-2x}{\sqrt{1-x^{2}}} & 1
\end{array}\right|\\\\
 & =\sqrt{1-x^{2}}+\frac{2x^{2}}{\sqrt{1-x^{2}}}\\\\
 & =\frac{1+x^{2}}{\sqrt{1-x^{2}}}
\end{aligned}$$

which never vanishes in the interval $(-1,1)$. Hence, $\sqrt{1-x^{2}}$,
$x$ are linearly independent in this interval.
**Exercise.**
$\sin x/2$, $\cos^{2}x$ on any interval $I=[a,b]$.

*Solution.*

We have:

$$\begin{aligned}
W[\sin x/2,\cos^{2}x] & =\left|\begin{array}{cc}
\sin x/2 & \cos^{2}x\\\\
\frac{1}{2}\cos x/2 & 2\cos x\cdot(-\sin x)
\end{array}\right|\\\\
 & =\left|\begin{array}{cc}
\sin x/2 & \cos^{2}x\\\\
\frac{1}{2}\cos x/2 & -\sin2x
\end{array}\right|
\end{aligned}$$

The Wronskian is non-zero for atleast one point in any subinteval
$I=[a,b]$ of the real line. Hence, $\sin x/2$ and $\cos^{2}x$ are
linearly independent.
**Exercise.**
Show that $x^{\alpha}$, $x^{\beta}$and $x^{\gamma}$ are linearly
independent in $\mathcal{C}(0,\infty)$ if and only if they are linearly
independent for every subinterval of $(0,\infty)$. {[}Hint: first
establish the following assertions, then use the necessary and sufficient
condition for linear independence.)

(a) $x^{\alpha}$, $x^{\beta}$ and $x^{\gamma}$ satisfy the linear
differential equation

$$\begin{aligned}
x^{3}y'''+a_{2}x^{2}y''+a_{1}xy'+a_{0}y & =0
\end{aligned}$$

where $a_{2}=3-\alpha-\beta-\gamma$, $a_{1}=1-\alpha-\beta-\gamma+\alpha\beta+\alpha\gamma+\beta\gamma$,
$a_{0}=-\alpha\beta\gamma$.

*Solution.*

Let $y=x^{n}$. Then, $y'=nx^{n-1}$, $y''=n(n-1)x^{n-2}$ and $y'''=n(n-1)(n-2)x^{n-3}$.
Assume that $x^{\alpha}$, $x^{\beta}$ and $x^{\gamma}$ satisfy
the differential equation 

$$\begin{aligned}
x^{3}y'''+a_{2}x^{2}y''+a_{1}xy'+a_{0}y & =0
\end{aligned}$$

Then, we must have:

$$\begin{aligned}
n(n-1)(n-2)+a_{2}n(n-1)+a_{1}n+a_{0} & =0\\\\
n(n^{2}-3n+2)+a_{2}(n^{2}-n)+a_{1}n+a_{0} & =0\\\\
n^{3}-3n^{2}+2n+a_{2}n^{2}-a_{2}n+a_{1}n+a_{0} & =0\\\\
n^{3}+(a_{2}-3)n^{2}+(a_{1}-a_{2}+2)n+a_{0} & =0
\end{aligned}$$

where $n=\alpha,\beta,\gamma$. This is a cubic polynomial in $n$,
whose roots are $\alpha$, $\beta$ and $\gamma$. So, we must have:

$$\begin{aligned}
\alpha+\beta+\gamma & =-(a_{2}-3)\\\\
\alpha\beta+\beta\gamma+\gamma\alpha & =(a_{1}-a_{2}+2)\\\\
\alpha\beta\gamma & =-a_{0}
\end{aligned}$$

Therefore, $a_{2}=3-\alpha-\beta-\gamma$. 

Next,$a_{1}=a_{2}+\alpha\beta+\beta\gamma+\gamma\alpha-2=1-\alpha-\beta-\gamma+\alpha\beta+\beta\gamma+\gamma\alpha$. 

And finally, $a_{0}=-\alpha\beta\gamma$.

(b) Show that:

$$\begin{aligned}
W[x^{\alpha},x^{\beta},x^{\gamma}] & =x^{\alpha+\beta+\gamma-3}\left|\begin{array}{ccc}
1 & 1 & 1\\\\
\alpha & \beta & \gamma\\\\
\alpha(\alpha-1) & \beta(\beta-1) & \gamma(\gamma-1)
\end{array}\right|
\end{aligned}$$

and hence $W[x^{\alpha},x^{\beta},x^{\gamma}]$ vanishes nowhere in
$(0,\infty)$.

*Solution.*

We have:

$$\begin{aligned}
W[x^{\alpha},x^{\beta},x^{\gamma}] & =\left|\begin{array}{ccc}
x^{\alpha} & x^{\beta} & x^{\gamma}\\\\
\alpha x^{\alpha-1} & \beta x^{\beta-1} & \gamma x^{\gamma-1}\\\\
\alpha(\alpha-1)x^{\alpha-2} & \beta(\beta-1)x^{\beta-2} & \gamma(\gamma-1)x^{\gamma-2}
\end{array}\right|\\\\
 & =\left|\begin{array}{ccc}
x^{\alpha} & x^{\beta} & x^{\gamma}\\\\
\alpha x^{\alpha-1} & \beta x^{\beta-1} & \gamma x^{\gamma-1}\\\\
\alpha(\alpha-1)x^{\alpha-2} & \beta(\beta-1)x^{\beta-2} & \gamma(\gamma-1)x^{\gamma-2}
\end{array}\right|\\\\
 & =x^{\alpha-2}\cdot x^{\beta-2}\cdot x^{\gamma-2}\left|\begin{array}{ccc}
x^{2} & x^{2} & x^{2}\\\\
\alpha x & \beta x & \gamma x\\\\
\alpha(\alpha-1) & \beta(\beta-1) & \gamma(\gamma-1)
\end{array}\right|\\\\
 & =x^{\alpha-2}\cdot x^{\beta-2}\cdot x^{\gamma-2}\cdot x^{2}\cdot x\left|\begin{array}{ccc}
1 & 1 & 1\\\\
\alpha & \beta & \gamma\\\\
\alpha(\alpha-1) & \beta(\beta-1) & \gamma(\gamma-1)
\end{array}\right|\\\\
 & =x^{\alpha+\beta+\gamma-3}\left|\begin{array}{ccc}
1 & \alpha & \alpha(\alpha-1)\\\\
1 & \beta & \beta(\beta-1)\\\\
1 & \gamma & \gamma(\gamma-1)
\end{array}\right|\\\\
 & \{R_{2}\leftarrow R_{2}-R_{1},R_{3}\leftarrow R_{3}-R_{1}\}\\\\
 & =x^{\alpha+\beta+\gamma-3}\left|\begin{array}{ccc}
1 & \alpha & \alpha(\alpha-1)\\\\
0 & \beta-\alpha & (\beta-\alpha)(\beta+\alpha-1)\\\\
0 & \gamma-\alpha & (\gamma-\alpha)(\gamma+\alpha-1)
\end{array}\right|\\\\
 & =x^{\alpha+\beta+\gamma-3}(\beta-\alpha)(\gamma-\alpha)\left|\begin{array}{ccc}
1 & \alpha & \alpha(\alpha-1)\\\\
0 & 1 & (\beta+\alpha-1)\\\\
0 & 1 & (\gamma+\alpha-1)
\end{array}\right|\\\\
 & =x^{\alpha+\beta+\gamma-3}(\beta-\alpha)(\gamma-\alpha)(\gamma-\beta)
\end{aligned}$$

Since $\alpha$, $\beta$ and $\gamma$ are distinct real numbers,
$W[x^{\alpha},x^{\beta},x^{\gamma}]$ vanishes nowhere in $(0,\infty)$.
Consequently, by the necessary and sufficient condition of linear
independence, $x^{\alpha}$, $x^{\beta}$and $x^{\gamma}$ are linearly
independent.

**Exercise.**
Show that $f(x)$ and $xf(x)$ are linearly independent in $\mathcal{C}[a,b]$
if $f$ is continuous and not identically zero on $[a,b]$.

*Solution.*

We have:

$$\begin{aligned}
W[f(x),xf(x)] & =\left|\begin{array}{cc}
f(x) & xf(x)\\\\
f'(x) & f(x)+xf'(x)
\end{array}\right|\\\\
 & =f(x)^{2}+xf(x)f'(x)-xf(x)f'(x)\\\\
 & =f(x)^{2}
\end{aligned}$$

If $f$ is continuous and not identically equal to zero, there exists
a point in $\mathbf{R}$, where it is non-zero. Hence, by the sufficient
condition on linear independence, $f(x)$ and $xf(x)$ are linearly
independent.

**Exercise.**
Let $f$, $g$ be two functions in $\mathcal{C}^{1}[a,b]$ and suppose
that $g$ never vanishes in $I$. Prove that if $W=[f(x),g(x)]$ is
identically equal to zero on $I$, then $f$ and $g$ are linearly
dependent in $\mathcal{C}^{1}(I)$.

*Solution.*

We have:

$$\begin{aligned}
W[f(x),g(x)] & =f(x)g'(x)-g(x)f'(x)\\\\
 & =-g(x)^{2}\frac{d}{dx}\left(\frac{f(x)}{g(x)}\right)
\end{aligned}$$

Since $f$ and $g$ are the solutions of the differential equation
$d(u/v)=0$, and their Wronskian is identically equal to zero, the
functions $f(x)$ and $g(x)$ are linearly dependent.
**Exercise.**
(a) Show that:

$$\begin{aligned}
W[e^{a_{1}x},\ldots,e^{a_{n}x}] & =e^{(a_{1}+\ldots+a_{n})x}\left|\begin{array}{cccc}
1 & 1 & \ldots & 1\\\\
a_{1} & a_{2} & \ldots & a_{n}\\\\
a_{1}^{2} & a_{2}^{2} & \ldots & a_{n}^{2}\\\\
\vdots &  &  & \vdots\\\\
a_{1}^{n-1} & a_{2}^{n-1} & \ldots & a_{n}^{n-1}
\end{array}\right|
\end{aligned}$$

*Solution.*

###Abel's Formula.}

The Wronskian for a set of solutions for an $n$th order linear differential
equation either vanishes identically or not at all. This fact can
also be deduced from the Abel's theorem, which gives an explicit formula
for the Wronskian.
\begin{thm*}
Let $y_{1},\ldots,y_{n}$ be solutions on an interval $I=[a,b]$ of
the $n$th order equation:

$$\begin{aligned}
a_{n}(x)\frac{d^{n}y}{dx^{n}}+a_{n-1}(x)\frac{d^{n-1}y}{dx^{n-1}}+\ldots+a_{0}(x)y & =0
\end{aligned}$$

Then,

$$\begin{aligned}
W[y_{1}(x),\ldots,y_{n}(x)] & =ce^{-\int[a_{n-1}(x)/a_{n}(x)]dx}
\end{aligned}$$

This result is known as Abel's formula for the Wronskian.
\end{thm*}
\emph{Proof.}

In order to avoid using the properties of determinants, we shall prove
only in the case $n=2$. The general proof is identical, except that
it uses the formula for the derivative of an $n$th order determinant.
Thus, suppose that $y_{1}$ and $y_{2}$ are solutions of 

$$\begin{aligned}
a_{2}(x)\frac{d^{2}y}{dx^{2}}+a_{1}(x)\frac{dy}{dx}+a_{0}(x)y & =0
\end{aligned}$$

on an interval $I$. Then,

$$\begin{aligned}
\frac{d}{dx}W[y_{1}(x),y_{2}(x)] & =\frac{d}{dx}\left|\begin{array}{cc}
y_{1}(x) & y_{2}(x)\\\\
y_{1}'(x) & y_{2}'(x)
\end{array}\right|\\\\
 & =\frac{d}{dx}(y_{1}(x)y_{2}'(x)-y_{2}(x)y_{1}'(x))\\\\
 & =y_{1}'(x)y_{2}'(x)+y_{1}(x)y_{2}''(x)-y_{2}'(x)y_{1}'(x)-y_{2}(x)y_{1}''(x)\\\\
 & =y_{1}(x)y_{2}''(x)-y_{2}(x)y_{1}''(x)\\\\
 & =y_{1}(x)\left[-\frac{a_{1}(x)}{a_{2}(x)}y_{2}'(x)-\frac{a_{0}(x)}{a_{2}(x)}y_{2}(x)\right]-y_{2}(x)\left[-\frac{a_{1}(x)}{a_{2}(x)}y_{1}'(x)-\frac{a_{0}(x)}{a_{2}(x)}y_{1}(x)\right]\\\\
 & =-\frac{a_{1}(x)}{a_{2}(x)}(y_{1}(x)y_{2}'(x)-y_{2}(x)y_{1}'(x))\\\\
 & -\frac{a_{1}(x)}{a_{2}(x)}W[y_{1}(x),y_{2}(x)]
\end{aligned}$$

Thus, $W[y_{1}(x),y_{2}(x)]$ is differentiable on $I$ and satisfies
the first order linear differential equation:

$$\begin{aligned}
\frac{dy}{dx}+\frac{a_{1}(x)}{a_{2}(x)}y & =0
\end{aligned}$$

But, the general solution of this equation is:

$$\begin{aligned}
y & =c_{1}e^{-\int[a_{1}(x)/a_{2}(x)]dx}
\end{aligned}$$

and hence, for an appropriate value of $c$, we have:

$$\begin{aligned}
W[y_{1}(x),y_{2}(x)] & =ce^{-\int[a_{1}(x)/a_{2}(x)]dx}
\end{aligned}$$


