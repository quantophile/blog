---
title: Sequences and Series of Functions
date: 2022-01-17T20:38:23+01:00
math: true
tags: ["sequence-of-functions", "uniform-convergence", "real-analysis"]
categories: ["Real Analysis"]
---

In 1689, Jakob Bernoulli published his *Tractus de seriebus infinitis* summarizing what was known about the infinite series towards the end of the 17th century. Full of clever calculations and conclusions, this publication was also notable for one particular question that it didn't answer; namely, what is the precise value of the series

$$\sum_{n=1}^{\infty}\frac{1}{n^2} = 1 + \frac{1}{4} + \frac{1}{9} + \frac{1}{16} + \ldots$$

Bernoulli convincingly argued that $\sum \frac{1}{n^2}$ converged to something less than $2$, but he was unable to find an explicit expression for the limit. Generally speaking, it is much harder to sum a series than it is to determine whether or not it converges. In fact, being able to find the sum of a convergent series is the exception rather than the rule. In this case, however, the series $\sum \frac{1}{n^2}$ seemed so elementary more elementary than, say, $\sum_{n=1}^{\infty}n^2/2^n$ or $\sum_{n=1}^{\infty}1/n(n+1)$, both of which Bernoulli was able to handle.

Geometric series are the most prominent class of examples that can be readily summed. We have seen that,

$$
\frac{1}{1-x} = 1 + x + x^2 + x^3 + \ldots \tag{1}
$$

Thus, for example, $\sum_{n=0}^{\infty}1/2^n = 2$ and $\sum_{n=0}^{\infty}(-1/3)^n = 3/4$. Geometric series were part of the mathematical folklore long before Bernoulli; however what was relatively novel in Bernoulli's time was the idea of operating on infinite series such as (1) with tools from the budding theory of calculus. For instance, what happens if we take the derivative on each side of the equation (1)? The left side is easy enough - we just get $1/(1-x)^2$. But what about the right side? Adopting a 17th century mindset, a natural way to proceed is to treat the infinite series as a polynomial, albeit of infinite degree. Differentiation across equation (1) in this fashion gives:

$$
\frac{1}{(1-x)^2} = 0 + 1 + 2x + 3x^2 + 4x^3 + \ldots \tag{2}
$$

Is this a valid formula, at least for values of $x$ in $(-1,1)$? Empirical evidence suggests it is. Setting $x = 1/2$, we get

$$
4 = \sum_{n=1}^{\infty}\frac{n}{2^{n-1}} = 1 + 1 + \frac{3}{4} + \frac{4}{8} + \frac{5}{16} + \ldots 
$$

which feels plausible, and is in fact true. Although not Bernoulli's requested series, this does suggest a possible new line of attack.

Manipulations of this sort can be used to create a wide assortment of new series representations for familiar functions. Substituting $-x^2$ for $x$ in (1) gives:

$$
\frac{1}{1 + x^2} = 1 - x^2 + x^4 - x^6 + x^8 - \ldots \tag{3}
$$

for all $x \in (-1,1)$.

Once again closing our eyes to the potential danger of treating an infinite series as though it were a polynomial, let's see what happens when we take antiderivatives. Using the fact that,

$$
(\arctan x)' = \frac{1}{1 + x^2} \quad \text{ and } \arctan 0 = 0
$$

equation (3) becomes

$$
\arctan x = x - \frac{x^3}{3} + \frac{x^5}{5} - \frac{x^7}{7} + \ldots \tag{4}
$$

Plugging $x = 1$ into equation (4) yields the striking relationship

$$
\frac{\pi}{4} = 1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \frac{1}{9} - \ldots \tag{5}
$$

The constant $\pi$, which arises from the geometry of circles, has somehow found its way into an equation involving the reciprocals of the odd integers. Is this a valid formula? Can we really treat the inifinite series in (3) like a finite polynomial? Even if the answer is yes, there is still another mystery to solve in this example. Plugging $x=1$ into equations (1), (2) or (3) yields mathematical gibberish, so is it prudent to anticipate something meaningful arising from equation (4) at this same value? Will any of these ideas get us closer to computing $\sum_{n=1}^{\infty}1/n^2$?

As it turned out, Bernoulli's plea for help was answered in an unexpected way by Leonard Euler. At a young age, Euler was a student of Jakob Bernoulli's brother Johann, and the stellar pupil quickly rose to become the preeminent mathematician of his age. Euler's solution is impossible to anticipate. In 1735, he announced that

$$
1 + \frac{1}{4} + \frac{1}{9} + \frac{1}{16} + \ldots = \frac{\pi^2}{6}
$$

a provocative formula, that even more than equation (5), hints at deep connections between geometry, number theory and analysis. Euler's argument is quite short, but it needs to be viewed in the context of the time in which it was created. The *infinite polynomials* in this discussion are examples of *power series*, and a major catalyst for the expanding power of calculus in the 17th and 18th centuries was a proliferation of techniques like the ones used to generate formulas (2), (3) and (4). The machinations of both algebra and calculus are relatively straightforward when restricted to the class of polynomials. So, if in fact power series could be treated more or less like unending polynomials, then there was a great incentive to try to find power series representations for familiar functions like $e^x$, $\sqrt{1 + x}$ or $\sin (x)$.

The appearance of $\arctan x$ in (4) is an encouraging sign that this might indeed always be possible. One of Issac Newton's more significant achievements was to produce a generalization of the binomial formula. If $n \in \mathbf{N}$, then old-fashioned finite algebra leads to the formula

$$
(1 + x)^n = 1 + nx + \frac{n(n-1)}{2!}x^2 + \frac{n(n - 1)(n - 2)}{3!}x^3 + \ldots + x^n
$$

Through a process of experimentation and intuition Newton realized that for $r \notin \mathbf{N}$, the infinite series

$$
(1 + x)^r = 1 + rx + \frac{r(r-1)}{2!}x^2 + \frac{r(r-1)(r-2)}{3!}x^3 + \ldots
$$

was meaningful, atleast for $x \in (-1,1)$. Setting $r = -1$, for example, yields

$$
\frac{1}{1+x} = 1 - x + x^2 - x^3 + x^4 - \ldots
$$

which can easily be seen to be equivalent to the equation (1). Setting $r = 1/2$ we get,

$$
\sqrt{1 + x} = 1 + \frac{1}{2}x - \frac{1}{2^2 2!}x^2 + \frac{1\cdot 3}{2^3 3!}x^3 - \frac{1 \cdot 3 \cdot 5}{2^4 4!}x^4 + \ldots
$$

One way to lend a litle credence to this formula for $\sqrt{1+x}$ is to focus on the first few terms and square the series:

$$
\begin{align\*}
(\sqrt{1+x})^2 &= \left(1 + \frac{x}{2} - \frac{x^2}{8} + \frac{x^3}{16} - \ldots \right)\left(1 + \frac{x}{2} - \frac{x^2}{8} + \frac{x^3}{16} - \ldots \right)\\\\
&= 1 + \left(\frac{1}{2} + \frac{1}{2}\right)x + \left(-\frac{1}{8} - \frac{1}{8} + \frac{1}{4}\right)x^2 + \left(\frac{1}{16} + \frac{1}{16} - \frac{1}{16} - \frac{1}{16}\right)x^3 + \ldots \\\\
&= 1 + x + 0x^2 + 0x^3 + \ldots \\\\
&= 1 + x
\end{align\*}
$$

Amid all of the unfounded assumptions we are making about infinity, calculations like this induce a feeling of optimism about the legitimacy of our search for power series representations.

Newton's binomial series is the starting point for a modern proof Euler's famous sum, which is sketched out in detail further at length. Euler's original 1735 argument, however, started from the power series representation for $\sin (x)$. The formula:

$$
\sin (x) = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \frac{x^7}{7!} + \ldots 
$$

was known to Newton, Bernoulli and Euler alike. In contrast to equation (1), we will see that this formula is valid for all $x \in \mathbf{R}$. Factoring out $x$ and dividing yields a power series with leading coefficient equal to $1$:

$$
\frac{\sin x}{x} = 1 - \frac{x^2}{3!} + \frac{x^4}{5!} - \frac{x^6}{7!} + \ldots
$$

Euler's idea was to continue factoring the power in (6), and his strategy for doing this was very much in keeping with what we have seen so far - treat the power series as through it were a polynomial and then extend the pattern to infinity.

Factoring a polynomial of, say, degree three is straightforward if we know its roots. If $p(x) = 1 + ax + bx^2 + cx^3$ has roots $r_1, r_2$ and $r_3$, then

$$
p(x) = \left(1- \frac{x}{r_1}\right)\left(1- \frac{x}{r_2}\right)\left(1- \frac{x}{r_3}\right)
$$

To see this just directly substitute to get $p(0)=1$ and $p(r_1) = p(r_2) = p(r_3) = 0$. 

The roots of the power series in (6) are the non-zero roots of $\sin x$ or $x = \pm\pi,\pm 2\pi, \pm 3\pi,$ and so on. All right then - relying on his fabled intuition, Euler surmised that

$$
\begin{align\*}
&1 - \frac{x^2}{3!} + \frac{x^4}{5!} - \frac{x^6}{7!} + \ldots \\\\
=& \left(1 - \frac{x}{\pi}\right)\left(1 + \frac{x}{\pi}\right)\left(1 - \frac{x}{2\pi}\right)\left(1 + \frac{x}{2\pi}\right)\left(1 - \frac{x}{3\pi}\right)\left(1 + \frac{x}{3\pi}\right)\ldots \\\\
=& \left(1- \frac{x^2}{\pi^2}\right)\left(1- \frac{x^2}{4\pi^2}\right)\left(1- \frac{x^2}{9\pi^2}\right)\ldots
\end{align\*}
$$

where in the last step adjacent pairs of factors have been multiplied together. What happens if we continue to multiply out the factors on the right? Well, the constant term comes out to be $1$ which happily matches the constant term on the left. The magic comes when we compare the $x^2$ term on each side of (7). Multiplying out the infinite number of factors on the right (using our imagination as necessary) and collecting like powers of $x$, equation (7) becomes

$$
\begin{align\*}
1 - \frac{x^2}{3!} + \frac{x^4}{5!} - \frac{x^6}{7!} + \ldots = 1 + \left(-\frac{1}{\pi^2} - \frac{1}{4\pi^2} - \frac{1}{9\pi^2} - \ldots \right)x^2 + \left(\frac{1}{4\pi^4} + \frac{1}{9\pi^4} + \ldots \right)x^4 + \ldots 
\end{align\*}
$$

Equating the coefficients of $x^2$ on each side yields,

$$
-\frac{1}{3!} = -\frac{1}{\pi^2} - \frac{1}{4\pi^2} - \frac{1}{p\pi^2} - \ldots
$$

which when we multiply by $-\pi^2$ becomes

$$
\frac{\pi^2}{6} = 1 + \frac{1}{4} + \frac{1}{9} + \frac{1}{16} + \ldots 
$$

Numerical approximations of each side of this equation confirmed for Euler that, despite the audacious leaps in his argument, he had landed on solid groud. By our standards, this derivation falls well short of being a proper proof, and we will have to tend to this in the upcoming chapters. The takeaway of this discussion is that the hard work ahead is worth the effort. Infinite series representations of functions are both useful and surprisingly elegant, and can lead to remarkable conclusions when they are properly handled. 

The evidence so far suggests power series are quite robust when treated as if they were finite in nature. Term-by-term differentiation produced a valid conclusion in equation (2), and taking antiderivatives fared similarly well in (4). We will see these manipulations are *not* always justified for infinite series of more general types of functions. What is it about power series in particular that makes them so impervious to the dangers of the infinite? Of the many unanswered questions in this discussion, this last one is probably the most central, and the most important to understand series of functions in general.


## Uniform Converence of a Sequence of Functions

Adopting the same strategy we used in chapter 2, we will initially concern ourselves with the behaviour and properties of converging *sequences* of functions. Because convergence of the infinite series is defined in terms of the associated sequence of partial sums, the results from our study of sequences will be immediately applicable to the questions we have raised about both power series and more general infinite series of functions. 

### Pointwise Convergence.

---
**Definition. (Pointwise Convergence)** For each $n \in \mathbf{N}$, let $f_n$ be a function defined on a set $A \subseteq \mathbf{R}$. The sequence $(f_n)$ of functions *converges pointwise* on $A$ to a function $f$ if, for all $x \in A$, the sequence of real numbers $f_n(x)$ converges to $f(x)$.

---

In this case, we write $f_n \to f$, $\lim f_n = f$ or $\lim_{n \to \infty}f_n(x) = f(x)$. This last expression is helpful if there is any confusion as to whether $x$ or $n$ is the limiting variable. 

**Example.** (i) Consider 

$$
\begin{align\*}
f_n(x) = \frac{x^2 + nx}{n}
\end{align\*}
$$

on all of $\mathbf{R}$. Graphs of $f_1,f_5,f_{10}$ and $f_{20}$ give an indication of what is happening as $n$ gets larger. Algebraically, we can compute:

$$
\lim_{n \to \infty} f_n(x) = \lim_{n \to \infty} \frac{x^2 + nx}{n} = \lim_{n \to \infty} \frac{x^2}{n} + x = x
$$

Thus, $(f_n)$ converges pointwise to $f(x) = x$ on $\mathbf{R}$.

(ii) Let $g_n(x) = x^n$ on the set $[0,1]$, and consider what happens as $n$ tends to infinity. If $0 \leq x < 1$, then we have seen that $x^n \to 0$. On the other hand, if $x = 1$, then $x^n \to 1$. It follows that, $g_n \to g$ pointwise on $[0,1]$, where

$$
\begin{align\*}
g(x) &= \begin{cases}
0 & \text{ for } 0 \leq x < 1 \\\\
1 & \text{ for } x = 1
\end{cases}
\end{align\*}
$$

(iii) Consider $h_n(x) = x^{1+\frac{1}{2n-1}}$ on the set $[-1.1]$. For a fixed $x \in [-1,1]$ we have:

$$
\begin{align\*}
h_n(x) = x \lim_{n \to \infty} x^{\frac{1}{2n-1}} = |x|
\end{align\*}
$$

Examples 6.2.2. (ii) and (iii) are our first indication that there is some difficult work ahead of us. The central theme of this chapter is analysing which properties the limit function inherits from the approximating sequence. In example 6.2.2 (iii), we have a sequence of differentiable functions converging pointwise to a limit that is not differentiable at the origin. In example 6.2.2 (ii), we see an even more fundamental problem of a sequence of continuous functions converging to a limit that is not continuous.

### Continuity of the Limit Function.

With example 6.2.2 (ii) firmly in mind, we begin this discussion with a doomed attempt to prove that the pointwise limit of continuous functions is continuous. Upon discovering the problem in the argument, we will be in a better position to understand the need for a stronger notion of convergence for sequences of functions.

Assume that $(f_n)$ is a sequence of continuous functions on a set $A \subseteq \mathbf{R}$, and assume $(f_n)$ converges pointwise to a limit $f$. To argue that $f$ is continuous, fix a point $c \in A$, and let $\epsilon > 0$. To argue that $f$ is continuous, fix a point $c \in A$, and let $\epsilon > 0$. We need to find a $\delta > 0$ such that

$$
|x - c| < \delta \implies |f(x) - f(c)| < \epsilon
$$

By the triangle inequality,

$$
\begin{align\*}
|f(x) - f(c)| &= |f(x) - f_n(x) + f_n(x) - f_n(c) + f_n(c) - f(c)|\\\\
&\leq |f(x) - f_n(x)| + |f_n(x) - f_n(c)| + |f_n(c) - f(c)|
\end{align\*}
$$

Our first, optimistic impression is that each term in the sum of the right-hand side can be made small - the first and third by the fact that $f_n \to f$, and the middle term by the continuity of $f_n$. In order to use the continuity of $f_n$, we must first establish which particular $f_n$ we are talking about. Our first, optimistic impression is that each term in the sum on the right-hand can be small - the first and third by the fact that $f_n \to f$, and the middle term by the continuity of $f_n$. In order to use the continuity of $f_n$, we must first establish which particular $f_n$ we are talking about. Because $c \in A$ is fixed, there exists $N(\epsilon/3,c)$ such that 

$$
|f_N(x) - f_N(c) < \frac{\epsilon}{3}
$$

for all $x$ satisfying $|x-c|<\delta$.

Not that $N$ is chosen, the continuity of $f_N$ at $c$ implies that there exists $\delta(N,\epsilon/3) > 0$ such that

$$
|f_N(x) - f_N(c)|< \frac{\epsilon}{3}
$$

for all $x$ satisfying $|x - c| < \delta$.

But, here is the problem. We also need 
$$
|f_N(x) - f(x)| < \frac{\epsilon}{3}
$$

That is, for an arbitrary point $x$, it might very well be the case that, $f_{P} - f(x)<\epsilon/3$, where $P > N$. More, to the point, the variable $x$ is not fixed the way $c$ is in this discussion but represents any point in the interval $(c-\delta,c+\delta)$. Pointwise convergence implies that we can make $|f_n(x) - f(x)| < \epsilon/3$ for large enough values of $n$, but *the value of $n$ depends on the point $x$*. It is possible that different values of $x$ will result in the need for different - larger - choices of $n$. So, the set 

$$\\{N \in \mathbf{N}:|f_N(x) - f(x)|<\epsilon \text{ for all }x \in V_{\epsilon/3}(c)\\}$$

can be an unbounded set. 

### Uniform Convergence.

To resolve this dilemma, we define a new, stronger notion of convergence of functions. 

---
**Definition. (Uniform Convergence).** Let $(f_n)$ be a sequence of functions defined on a set $A \subseteq \mathbf{R}$. Then, $(f_n)$ *converges uniformly* on $A$ to a limit function $f$ defined on $A$ if and only if, for all $\epsilon > 0$, there exists $N = N(\epsilon)$, such that $|f_n(x) - f(x)|<\epsilon$ for all $n \geq N$ and $x \in A$. Mathematically,

$$: (\forall \epsilon >0), (\exists N(\epsilon) \in \mathbf{N}) : |f_n(x) - f(x)|<\epsilon, \forall x \in A, \forall n \geq N$$

---

To emphasize the difference between uniform convergence and pointwise convergence, we restate the definition of pointwise convergence being more explicit about the relationship between $\epsilon$, $N$ and $x$. In particular, notice where the domain point $x$ is referenced in each definition and consequently how the choice of $N$ then does or does not depend on this value.

---
**Definition (Pointwise Convergence).** Let $f_n$ be a sequence of functions defined on a set $A \subseteq \mathbf{R}$. Then, $(f_n)$ *converges  pointwise* on $A$ to a limit $f$ defined on $A$ if, for every $\epsilon > 0$ and for all $x \in A$, there exists $N=N(\epsilon,x)$ such that $|f_n(x) - f(x)| < \epsilon$ for all $n \geq N$. Mathematically,

$$: (\forall \epsilon >0), (\forall x \in A), (\exists N(\epsilon, x) \in \mathbf{N}) : |f_n(x) - f(x)|<\epsilon, \forall n \geq N$$

---

The use of the adverb *uniformly* here should be reminiscient of its use in the phrase uniformly continuous from Chapter 4. In both cases, the term uniformly is employed to express the fact that the response $\delta$ or $N$ to a prescribed $\epsilon$ can be chosen to work simultaneously for all values of $x$ in the relevant domain.

**Example.** (i) Let 

$$
g_n(x) = \frac{1}{n(1+x^2)}
$$

For any fixed $x \in \mathbf{R}$, we can see that $\lim g_n(x) = 0$ is the pointwise limit of the sequence $(g_n)$ on $\mathbf{R}$. Is this convergence uniform? The observation that,

$$
\frac{1}{1 + x^2} \leq 1
$$

for all $x \in \mathbf{R}$ implies that

$$
|g_n(x) - g(x)| = \left|\frac{1}{n(1+x^2)} - 0\right| \leq \frac{1}{n}
$$

Thus, given $\epsilon > 0$, we can choose $N > 1/\epsilon$ (which does not depend on $x$), and it follows that 

$$
n \geq N \quad \text{ implies } \quad |g_n(x) - g(x)| < \epsilon
$$

for all $x \in \mathbf{R}$. By definition, $g_n \to 0$ uniformly on $\mathbf{R}$.

(ii) Look back at example 6.2.2 (i), where we saw that $f_n(x) = (x^2 + nx)/n$ converges pointwise on $\mathbf{R}$ to $f(x) = x$. On $\mathbf{R}$, the convergence is not uniform. To see this write

$$
|f_n(x) - f(x)| = \left|\frac{x^2 + nx}{n} - x\right| = \frac{x^2}{n}
$$

and notice that in order to force $|f_n(x) - f(x)|<\epsilon$, we are going to have to choose 

$$
N > \frac{x^2}{\epsilon}
$$

Although this is possible to do for each $x \in \mathbf{R}$, there is not way to choose a single value of $N$ that will work for all values of $x$ at the same time.

On the other hand, we can show that $f_n \to f$ uniformly on the set $[-b,b]$. By restricting our attention to a bounded interval, we may now assert that 

$$
\frac{x^2}{n} \leq \frac{b^2}{n}
$$

Given $\epsilon > 0$ then, we can choose:

$$
N > \frac{b^2}{\epsilon}
$$

Graphically speaking, the uniform convergence of $f_n$ to a limit $f$ on a set $A$ can be visualized by constructing a band of radius $\pm \epsilon$ around the limit function $f$. If $f_n \to f$ uniformly, then there exists a point in the sequence after which each $f_n$ is *completely* contained in this $\epsilon-$strip. 

### Cauchy Criterion

Recall that the Cauchy criterion for convergent sequences of real numbers was an equivalent characterization of convergence which, unlike the definition, did not make explicit mention of the limit. The usefulness of the Cauchy criterion suggests the need for an analogous characterization of uniformly convergent sequences of functions. As with all statements about uniformity, pay special attention to the relationship between the response variable ($N \in \mathbf{N}$) and the domain variable ($x \in A$).

---
**Theorem (Cauchy Criterion for Uniform Convergence).** A sequence of functions $(f_n)$ defined on a set $A \subseteq \mathbf{R}$ converges uniformly on $A$, if and only if, for every $\epsilon > 0$ there exists $N \in \mathbf{N}$ such that $|f_n(x) - f_m(x)| < \epsilon$ whenever $m,n \geq N$ and $x \in A$.

---

### Continuity Revisited

The stronger assumption of uniform convergence is precisely what is required to remove the flaws from our attempted proof that the limit of continuous functions is continuous. 

---
**Theorem (Continuous Limit Theorem).** Let $(f_n)$ be a sequence of functions defined on $A \subseteq \mathbf{R}$ that converges uniformly on $A$ to a function $f$. If each $f_n$ is continuous at $c \in A$, then $f$ is continuous at $c$.

---

*Proof.* Fix $c \in A$ and let $\epsilon > 0$. Choose $N(\epsilon)$ so that:

$$
|f_N(x) - f(x)| < \frac{\epsilon}{3}
$$

for all $x \in A$. We are able to do so, because $(f_n)$ converges to $f$ uniformly. Because $f_N$ is continuous, there exists $\delta(\epsilon,N,c)>0$ for which

$$
f_N(x) - f_N(c)| < \frac{\epsilon}{3}
$$

for all $|x - c| < \delta$.

And finally, since $(f_n)$ uniformly converges to $f$ on $A$, for the same $N(\epsilon)$, it follows that

$$
f_N(c) - f(c)| < \frac{\epsilon}{3}
$$

This implies that,

$$
\begin{align\*}
|f(x) - f(c)| &= |f(x) - f_N(x) + f_N(x) - f_N(c) + f_N(c) - f(c)|\\\\
&\leq |f(x) - f_N(x)| + |f_N(x) - f_N(c)| + |f_N(c) - f(c)|\\\\
&< \frac{\epsilon}{3} + \frac{\epsilon}{3} + \frac{\epsilon}{3} = \epsilon
\end{align\*}
$$

Thus, $f$ is continuous at $c \in A$.

### Exercise Problems.

---
1. [Abbott 6.2.1] Let 

$$f_n(x) = \frac{nx}{1 + nx^2}$$

(a) Find the pointwise limit of $(f_n)$ for all $x \in (0,\infty)$.

(b) Is the convergence uniform on $(0,\infty)$?

(c) Is the convergence uniform on $(0,1)$?

(d) Is the convergence uniform on $(1,\infty)$?

---

*Proof.*

(a) We have,

$$
\begin{align\*}
\lim_{n \to \infty} f_n(x) &= \lim_{n \to \infty} \frac{nx}{1 + nx^2} =\lim_{n \to \infty}  \frac{x}{\frac{1}{n} + x^2} \\\\
&= \frac{x}{x^2} = \frac{1}{x}
\end{align\*}
$$

Define 

$$
f(x) = \frac{1}{x}
$$

Then, $(f_n)$ converges pointwise to $f$.

(b) Consider the distance 

$$
\begin{align\*}
|f_n(x) - f(x)| &= \left|\frac{nx}{1 + nx^2} - \frac{1}{x}\right| = \left|\frac{nx^2 - 1 - nx^2}{x(1+nx^2)}\right|\\\\
&= \left|\frac{1}{x(1+nx^2)}\right|\\\\
&\leq \frac{1}{n|x|^3}
\end{align\*}
$$

We are interested to make the above distance as small as we please. So, we must $N > \frac{|x|^3}{\epsilon}$. Here, $N$ is function of both the point $x$ and $\epsilon$. We cannot choose a single $N$, that works for all $x$. Hence, $(f_n)$ does not converge uniformly to $f$ on $(0,\infty)$.

(c) $(f_n)$ does not converge uniformly to $f$ on $(0,1)$.

(d) We have, 

$$
N > \frac{|x|^3}{\epsilon}
$$

If we replace the right hand by it's lower bound, we are strengthening the condition we wish to prove. Since $x \in (1,\infty)$, we have $|x| > 1$. So, pick

$$
N > \frac{1}{\epsilon}
$$

It follows that, $(f_n)$ converges to $f$ uniformly.

---
2. [Abbott 6.2.2] (a) Define a sequence of functions on $\mathbf{R}$ by,

$$
f_n(x) = \begin{cases}
1 &\text{ if } x = 1,\frac{1}{2},\frac{1}{3},\ldots,\frac{1}{n}\\\\
0 &\text{ otherwise }
\end{cases}
$$

and let $f$ be the pointwise limit of $f_n$. Is each $f_n$ continuous at zero? Does $f_n \to f$ uniformly on $\mathbf{R}$? Is $f$ continuous at zero?

(b) Repeat this exercise using the sequence of functions 

$$
g_n(x) = \begin{cases}
x \quad \text{ if } x = 1,\frac{1}{2}, \frac{1}{3}, \ldots,\frac{1}{n}\\\\
0 \quad \text{ otherwise }
\end{cases}
$$

(c) Repeat the exercise once more with the sequence

$$
h_n(x) = \begin{cases}
1 \quad \text{ if } x = \frac{1}{n} \\\\
x \quad \text{ if } x = 1, \frac{1}{2},\frac{1}{3},\ldots,\frac{1}{n-1} \\\\
0 \quad \text{ otherwise }
\end{cases}
$$

In each case, explain how the results are consistent with the content of the Continuous Limit Theorem.

---

*Proof*. 

(a) 

Define 

$$
f(x) = \begin{cases}
1 &\text{ if } x \in \\{\frac{1}{n}:n \in \mathbf{N}\\} \\\\
0 &\text{ otherwise }
\end{cases}
$$

**Pointwise convergence.**

We show that, $(f_n)$ converges to $f$ pointwise for all $x$.

Let $x \in \\{ \frac{1}{n}:n\in\mathbf{N}\\}$.

Pick an arbitrary $\epsilon > 0$. By the Archimedean property, there exists an $N \in \mathbf{N}$ such that $\frac{1}{N} < \epsilon$.

If we choose $M > N + 1$, then $\frac{1}{M} < \frac{1}{N+1} < \epsilon$. The distance

$$
|f_m(x) - f(x)| = |1 - 1| = 0 < \epsilon
$$

for all $m \geq M$ and $x \in \\{ \frac{1}{n}:n\in\mathbf{N}\\}$. Moreover, if $x$ does not belong to this set, then $|f_m(x) - f(x)| = |0 - 0| < \epsilon$. 

**Uniform convergence.**

$(f_n)$ does not converge uniformly to $f$. Carefully, negating the definition of uniform convergence, we have,

---
**Absence of uniform convergence.** Let $(f_n)$ be a sequence of functions defined on a set $A\subseteq \mathbf{R}$. Then, $(f_n)$ fails to converge uniformly on $A$ to $f$, if, there exists $\epsilon_0 > 0$, for all $N$, such that $|f_n(x) - f(x)| \geq \epsilon_0$ for atleast one $n \geq N$ and some $x \in A$.

---

Pick $\epsilon_0 = \frac{1}{2}$ and $x_0 \in \\{\frac{1}{n}:n \in \mathbf{N}, n > N\\}$. Then, $|f_N(x_0) - f(x_0)| = |0 - 1| = 1 > \frac{1}{2} = \epsilon_0$. 

**Continuity of $f_n$.**

$f_M$ is continuous at $c = 0$. Pick an arbitrary $\epsilon > 0$. By the Archimedean property, there exists a natural number $N \in\mathbf{N}$ such that, $N < \frac{1}{\epsilon}$. We are interested to make the distance $|f_M(x) - f_M(0)| < \frac{1}{N}$. Pick $\delta = \min \\{\frac{1}{2M},\frac{1}{2N}\\}$. Then, for all $x \in (-\delta,\delta)$, it follows that $|f_M(x) - f_M(0)| = |0 - 0| = 0 <\epsilon$.

**Continuity of $f$.**

$f$ is not continuous at $c = 0$. Consider the sequence $(x_n)$ defined by $x_n:= \frac{1}{n}$. We have, $(x_n) \to 0$. But, $f(x_n)$ is the sequence $(1,1,1,\ldots)$, which converges to $1$, whilst $f(0)= 0$. So, $f$ fails to be continuous at $c=0$.

(b) Define 

$$
g(x) = \begin{cases}
x \quad \text{ if } x \in \\{\frac{1}{n} : n \in \mathbf{N}\\}\\\\
0 \quad \text{ otherwise }
\end{cases}
$$

**Pointwise convergence.**

Pick an arbitrary $\epsilon > 0$. By the Archimedean property, there exists $N \in\mathbf{N}$, such that, $\frac{1}{N} < \epsilon$. 

Let $x \in \\{\frac{1}{n}:n\in\mathbf{N}\\}$. 

If $n < N$, then $x = \frac{1}{n} > \frac{1}{N}$. Pick $M > N + 1$, then $\frac{1}{M} < \frac{1}{N} < x$. Thus, $|g_m(x) - g(x)| = |x - x| = 0 < \frac{1}{N} < \epsilon$ for all $m \geq M$.

If $n > N$, then $x = \frac{1}{n} < \frac{1}{N}$. Again, pick $M > \left(\frac{1}{x} + 1\right)$. Then, $\frac{1}{M} < x < \frac{1}{N}$. Thus, $|g_m(x) - g(x)| = |x - x| = 0 < \epsilon$ for all $m \geq M$.

Consequently, $(g_n)$ converges pointwise to $g$.

**Uniform convergence.**

Consider an arbitrary $g_N(x)$. And sample $g_N(x)$ at $x = \frac{1}{n}$, $n \in\mathbf{N}$. We have,

$$
g_N(1) = 1, g_N\left(\frac{1}{2}\right) = \frac{1}{2}, g_N\left(\frac{1}{3}\right) = \frac{1}{3},\ldots, g_N\left(\frac{1}{N}\right) = \frac{1}{N}, g_N\left(\frac{1}{N+1}\right) = 0
$$

And,

$$
g(1) = 1, g\left(\frac{1}{2}\right) = \frac{1}{2}, g\left(\frac{1}{3}\right) = \frac{1}{3},\ldots, g\left(\frac{1}{N}\right) = \frac{1}{N}, g\left(\frac{1}{N+1}\right) = \frac{1}{N+1}
$$

So, $\sup_x |g_N(x) - g(x)| = \frac{1}{N+1}$.

If we pick, $N > \frac{1}{\epsilon}$, then $|g_n(x) - g(x)| < \epsilon$ for all $x \in A$ and for all $n \geq N$. Consequently, $(g_n)$ converges uniformly to $g$ on $\mathbf{R}$.

**Continuity of $g_n$.**

$(g_n)$ is continuous at $c = 0$.

**Continuity of $g$.**

By continuous limit theorem, since $(g_n)$ converges uniformly to $g$, and each $g_n$ is continuous at $c=0$, it follows that $g$ is continuous at $c = 0$.

$g$ is continuous at $c = 0$. Pick an arbitrary $\epsilon > 0$. Let $(x_n)$ be an arbitrary sequence, such that $(x_n) \to 0$, with $x_n \neq 0$. The image sequence $g(x_n) = (x_n)$, which converges to $0$. This is true for all sequences $(x_n)$. Consequently, $g$ is continuous at $c = 0$.

(c) Define 

$$
h(x) = \begin{cases}
x &\text{ if } x \in \\{\frac{1}{n}:n\in\mathbf{N}\\}\\\\
0 &\text{ otherwise }
\end{cases}
$$

**Pointwise convergence.**

Pick an arbitrary $\epsilon > 0$. By the Archimedean property, there exists $N > 0$ such that $\frac{1}{N} < \epsilon$. 


Let $x \in \\{\frac{1}{n}:n \in \mathbf{N} \\}$.

Pick $M > \max \\{N+1, \frac{1}{x}\\}$. Then, the distance $|h_m(x) - h(x)|=|x - x| = 0 <\epsilon$ for all $m \geq M$ and $x \in (0,\infty)$. Consequently, $(h_m)$ converges to $h$ pointwise.

**Uniform convergence.**

Pick $\epsilon_0 = \frac{1}{2}$. If $M = 1$, pick $x_0 = 1/2$, we have $|h_2(1/2) - h(1/2)| = 1 - \frac{1}{2} \geq \frac{1}{2}$. If $M \geq 2$, pick $x_0 = \frac{1}{M}$, for all $M \in \mathbf{N}$. Then, $|h_M(x_0) - h(x_0)|=1 - \frac{1}{M} \geq \frac{1}{2} = \epsilon_0$.

Consequently, $(h_m)$ does not converge uniformly to $h$.

**Continuity of $(h_n)$.**

$h_n$ is continuous at $c = 0$. 

**Continuity of $h$.**

$h$ is continuous at $c = 0$.

---
3. [Abbott 6.2.3] For each $n \in \mathbf{N}$ and $x \in [0,\infty)$, let 

$$
g_n(x) = \frac{x}{1 + x^n} \quad \text{ and } \quad h_n(x) = \begin{cases}
1 & \text{ if } x \geq 1/n \\\\
nx & \text{ if } 0 \leq x < 1/n 
\end{cases}
$$

Answer the following questions for the sequences $(g_n)$ and $(h_n)$:

(a) Find the pointwise limit on $[0,\infty)$.

(b) Explain how we know that the convergence *cannot* be uniform on $[0,\infty)$.

(c) Choose a smaller set over which the convergence is uniform and supply an argument to show that this is indeed the case.

---

*Proof.*