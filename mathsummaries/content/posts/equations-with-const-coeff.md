---
title: "[ODE-02] Equations with constant coefficients"
date: 2023-09-11T12:42:55+02:00
math: true
tags: ["linear-odes"]
categories: ["Differential Equations"]
---

# Equations with constant coefficients. {#equations-with-constant-coefficients. .unnumbered}

Linear differential equations with constant coefficients, that is
equations of the form:

$$\begin{aligned}
a_{n}y^{(n)}+a_{n-1}y^{(n-1)}+\ldots+a_{0}y & =h(x)\quad\tag{1}
\end{aligned}$$

in which $a_{0},a_{1},\ldots,a_{n}\neq0$ are real constants, are in many
respects the simplest of all differential equations. For one thing, they
can be discussed entirely within the context of linear algebra and form
the only substantial class of equations with order greater than one that
can be explicitly solved. This, plus the fact, that such equations arise
in a surprisingly wide variety of physical problems, accounts for a
special place they occupy in the theory of linear differential
equations.

We shall begin the discussion in this chapter, by considering the
homogenous version of equation (1), which can be written in the form:

$$\begin{aligned}
(D^{n}+a_{n-1}D^{n-1}+\ldots+a_{0})y & =0\quad\tag{2}
\end{aligned}$$

or as

$$\begin{aligned}
Ly & =0\quad\tag{3}
\end{aligned}$$

where $L$ is constant coefficient linear differential operator
$D^{n}+a_{n-1}D^{n-1}+\ldots+a_{0}$. Algebraically, such operators
behave exactly as if they were ordinary polynomials in $D$, and
therefore can be factored according to the rules of elementary algebra.
In particular, it follows that every linear differential operator with
constant coefficients can be expressed as a product of constant
coefficient operators of degrees one and two. That's because, by the
fundamental theorem of algebra, every polynomial of degree $n$ has
atleast one complex root. As we shall see, this essentially reduces the
task of solving (2) to the second-order case, where complete results can
be obtained with relative ease.

This done, we will take up the problem of finding a particular solution
of $Ly=h$, given the general solution of the associated homogenous
equation $Ly=0$. Here the restriction on the coefficients of $L$ will be
dropped and much more far reaching results are obtained. The language of
operator theory and the ideas of linear algebra will dominate this
portion of our discussion and furnish just that measure of insight
needed to make it intelligible.

## Homogenous equations of order two. {#homogenous-equations-of-order-two. .unnumbered}

We have already emphasized that the technique for solving constant
coefficient linear differential equations depends on the commutativity
of the operator multiplication involved. To make this dependence
explicit, and at the same time phrase it in the form best suited to our
immediate needs, we begin by establishing :

::: lem*
** 1**. *If $L_{1},\ldots,L_{n}$ are constant coefficient linear
differential operators, then the null space of each of them is contained
in the null space of their product.*
:::

*Proof.*

To prove this assertion we must show that $(L_{1}L_{2}\ldots L_{n})y=0$
whenever $L_{i}y=0$. But this is a triviality, since:

$$\begin{aligned}
(L_{1}L_{2}\ldots L_{n})y & =L_{1}L_{2}\ldots L_{i-1}L_{i+1}\ldots L_{n}L_{i}y\\\\
 & =L_{1}L_{2}\ldots L_{i-1}L_{i+1}\ldots L_{n}(L_{i}y)\\\\
 & =L_{1}L_{2}\ldots L_{i-1}L_{i+1}\ldots L_{n}(0)\\\\
 & =0
\end{aligned}$$

::: example*
** 1**. The second order equation

$$\begin{aligned}
(D^{2}-4)y & =0\quad\tag{4}
\end{aligned}$$

may be rewritten as:

$$\begin{aligned}
(D+2)(D-2)y & =0
\end{aligned}$$

Hence, $e^{2x}$ and $e^{-2x}$ are the solutions of (4), since they are
respectively the solutions of the first order equations $(D-2)y=0$ and
$(D+2)y=0$. Furthermore, these functions are linearly independent in
$\mathcal{C}(-\infty,\infty)$ and therefore it follows that the general
solution of (4) is :

$$\begin{aligned}
y & =c_{1}e^{2x}+c_{2}e^{-2x}
\end{aligned}$$
:::

This example suggests that we attempt to solve the general second-order
equation

$$\begin{aligned}
(D^{2}+a_{1}D+a_{0})y & =0\quad\tag{5}
\end{aligned}$$

by decomposing the operator $D^{2}+a_{1}D+a_{0}$ into linear factors. To
this end, we find the roots $\alpha_{1},\alpha_{2}$ of the quadratic
equation:

$$\begin{aligned}
m^{2}+a_{1}m+a_{0} & =0\quad\tag{6}
\end{aligned}$$

known as the auxiliary or characteristic equation of (5) and then
rewrite (5) as:

$$\begin{aligned}
(D-\alpha_{1})(D-\alpha_{2})y & =0\quad\tag{7}
\end{aligned}$$

In solving the characteristic equation, the following three
possibilities may occur.

1\. All its roots are distinct and real.

2\. All its roots are real but some of its roots repeat.

3.All its roots are imaginary.

We shall discuss each of the above three possibilities separately.

Case I. **Roots of the Characteristic Equation real and distinct**.

Here the reasoning used in the above example carries over without
change. The functions $e^{\alpha_{1}x}$ and $e^{\alpha_{2}x}$ are
linearly independent solutions of (7), and hence the general solution of
the equation is:

$$\begin{aligned}
y & =c_{1}e^{\alpha_{1}x}+c_{2}e^{\alpha_{2}x}\quad\tag{8}
\end{aligned}$$

Case II. **Roots of the Characteristic equation are real and equal.**

In this case, the equation (7) becomes:

$$\begin{aligned}
(D-\alpha)^{2}y & =0\quad\tag{9}
\end{aligned}$$

Our earlier argument yields but one solution of the equation namely,
$e^{\alpha x}$. Using it, however, we can apply the following method to
find a second linearly independent solution. We know that, if $y_{1}(x)$
and $y_{2}(x)$ are the solutions of the ODE:

$$\begin{aligned}
y''+a_{1}y'+a_{0}y & =0\quad\tag{10}
\end{aligned}$$

then the Wronskian $W[y_{1}(x),y_{2}(x)]$ satisfies the first-order
equation:

$$\begin{aligned}
\frac{dy}{dx}+\frac{a_{1}}{a_{2}}y & =0\quad\tag{11}
\end{aligned}$$

That, is

$$\begin{aligned}
W[y_{1}(x),y_{2}(x)] & =ce^{-\int(a_{1}/a_{2})dx}\\\\
 & =ce^{-(a_{1}/a_{2})x}\quad\tag{12}
\end{aligned}$$

But, the Wronskian $W[y_{1}(x),y_{2}(x)]$ is given by :

$$\begin{aligned}
W[y_{1}(x),y_{2}(x)] & =y_{1}(x)y_{2}'(x)-y_{2}(x)y_{1}'(x)\\\\
 & =y_{1}y_{2}'-y_{2}y_{1}'\\\\
 & =y_{1}(x)\frac{dy_{2}}{dx}-y_{1}'(x)y_{2}\quad\tag{13}
\end{aligned}$$ Putting together (12) and (13), we have the first-order
equation:

$$\begin{aligned}
y_{1}(x)\frac{dy_{2}}{dx}-y_{1}'(x)y_{2} & =ce^{-(a_{1}/a_{2})x}\quad\tag{14}
\end{aligned}$$

Dividing both sides by $y_{1}(x)^{2}$, we get:

$$\begin{aligned}
\frac{y_{1}(x)\frac{dy_{2}}{dx}-y_{1}'(x)y_{2}}{y_{1}(x)^{2}} & =c\frac{e^{-(a_{1}/a_{2})x}}{y_{1}(x)^{2}}\quad\tag{15}
\end{aligned}$$

The left-hand side is now an exact differential and we have:

$$\begin{aligned}
d\left[\frac{y_{2}(x)}{y_{1}(x)}\right] & =c_{2}\frac{e^{-(a_{1}/a_{2})x}}{y_{1}(x)^{2}}dx\\\\
\int d\left[\frac{y_{2}(x)}{y_{1}(x)}\right] & =c_{2}\int\frac{e^{-(a_{1}/a_{2})x}}{y_{1}(x)^{2}}dx+c_{1}\\\\
y_{2}(x) & =c_{2}y_{1}(x)\int\frac{e^{-(a_{1}/a_{2})x}}{y_{1}(x)^{2}}dx+c_{1}y_{1}(x)\quad\tag{16}
\end{aligned}$$

Since the roots are repeated, the equation (9) can be expressed as:

$$\begin{aligned}
(D^{2}-2\alpha D+\alpha^{2})y & =0\quad\tag{17}
\end{aligned}$$

Hence, $a_{2}=1$, $a_{1}=2\alpha$. We also know that,
$y_{1}(x)=e^{\alpha x}$. Hence, the general solution to the equation is:

$$\begin{aligned}
y_{2}(x) & =c_{2}e^{\alpha x}\int\frac{e^{2\alpha x}}{e^{2\alpha x}}dx+c_{1}e^{\alpha x}\\\\
 & =e^{\alpha x}(c_{1}+c_{2}x)\quad\tag{18}
\end{aligned}$$

The second linearly independent solution is $xe^{\alpha x}$. We have
already seen that the two functions $e^{x}$, $xe^{x}$ are linearly
independent.

In general, it can be shown that if the characteristic equation has a
root $m=\alpha$, which has a multiplicity of $n$, then the general
solution is:

$$\begin{aligned}
y & =(c_{1}+c_{2}x+c_{3}x^{2}+\ldots+c_{n}x^{n-1})e^{\alpha x}\quad\tag{19}
\end{aligned}$$

Case III. $\alpha_{1}$ and $\alpha_{2}$ are complex. Any imaginary roots
must occur in conjugate pairs. Hence, if $\alpha+i\beta$ is one root,
then the other root must be $\alpha-i\beta.$ Assume now that
$\alpha+i\beta$ and $\alpha-i\beta$ are two imaginary roots of the
characteristic equation of a second order linear differential equation.
Then, its general solution by (8) is given as:

$$\begin{aligned}
y & =c_{1}'e^{(\alpha+i\beta)x}+c_{2}'e^{(\alpha-i\beta)x}\\\\
 & =e^{\alpha x}(c_{1}'e^{i\beta x}+c_{2}'e^{-i\beta x})\quad\tag{20}
\end{aligned}$$

By Euler's formula, we know that
$e^{i\beta x}=\cos\beta x+i\sin\beta x$, and
$e^{-i\beta x}=\cos\beta x-i\sin\beta x$. Substituting these in (20), we
get:

$$\begin{aligned}
y & =e^{\alpha x}\[(c_{1}'+c_{2}')\cos\beta x+(c_{1}'-c_{2}')i\sin\beta x\]\quad\tag{21}
\end{aligned}$$

We may now replace the constants $c_{1}'+c_{2}'=c_{1}$ and
$i(c_{1}'-c_{2}')=c_{2}$. Then, (21) becomes:

$$\begin{aligned}
y & =e^{\alpha x}(c_{1}\cos\beta x+c_{2}\sin\beta x)\quad\tag{22}
\end{aligned}$$

Another form of writing the general solution (22) more useful for
practical purposes may be obtained as follows. Write the equality:

$$\begin{aligned}
c_{1}\cos\beta x+c_{2}\sin\beta x & =\sqrt{c_{1}^{2}+c_{2}^{2}}\left(\frac{c_{1}}{\sqrt{c_{1}^{2}+c_{2}^{2}}}\cos\beta x+\frac{c_{2}}{\sqrt{c_{1}^{2}+c_{2}^{2}}}\sin\beta x\right)\quad\tag{23}
\end{aligned}$$


From the above figure, we see that

$$
\sin\delta = \frac{c_{1}}{\sqrt{c_{1}^{2}+c_{2}^{2}}}, \quad \cos\delta=\frac{c_{2}}{\sqrt{c_{1}^{2}+c_{2}^{2}}} \tag{24}$$

The susbstitution of these values in the right hand side of (23) gives:

$$\begin{aligned}
c_{1}\cos\beta x+c_{2}\sin\beta x & =\sqrt{c_{1}^{2}+c_{2}^{2}}(\sin\delta\cos\beta x+\sin\beta x\cos\delta)\\\\
 & =\sqrt{c_{1}^{2}+c_{2}^{2}}\sin(\beta x+\delta)\quad\tag{25}
\end{aligned}$$

If we interchange the positions of $c_{1}$ and $c_{2}$, we can also
write:

$$\begin{aligned}
c_{1}\cos\beta x+c_{2}\sin\beta x & =\sqrt{c_{1}^{2}+c_{2}^{2}}(\cos\delta\cos\beta x+\sin\beta x\sin\delta)\\\\
 & =\sqrt{c_{1}^{2}+c_{2}^{2}}\cos(\beta x-\delta)\quad\tag{26}
\end{aligned}$$

Replacing in (23) a new constant $c$ for the constant
$\sqrt{c_{1}^{2}+c_{2}^{2}}$, we may write the general solution (23) in
either of the forms:

$$\begin{aligned}
y & =ce^{\alpha x}\sin(\beta x+\delta)\quad\tag{27}
\end{aligned}$$

$$\begin{aligned}
y & =ce^{\alpha x}\cos(\beta x-\delta)\quad\tag{28}
\end{aligned}$$

::: example*
** 2**. Find the general solution of

$$\begin{aligned}
y''-2y'+2y & =0\quad\tag{29}
\end{aligned}$$
:::

*Solution.*

The roots of the characteristic equation of (29) are given by:

$$\begin{aligned}
D^{2}-2D+2 & =0\\\\
(D-1)^{2}+1 & =0\\\\
(D-1+i)(D-1-i) & =0
\end{aligned}$$

So, $\alpha_{1}=1-i$ and $\alpha_{2}=1+i$. Therefore, the general
solution of (29) can be written in any of the forms:

$$\begin{aligned}
y & =e^{x}(c_{1}\cos x+c_{2}\sin x)\\\\
 & =c_{1}e^{(1+i)x}+c_{2}e^{(1-i)x}\\\\
 & =ce^{x}\sin(x+\delta)\\\\
 & =ce^{x}\cos(x-\delta)
\end{aligned}$$

If the linear differential equation