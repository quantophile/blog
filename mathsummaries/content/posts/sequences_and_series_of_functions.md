---
title: Sequences and Series of Functions
date: 2022-01-17T20:38:23+01:00
math: true
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
\frac{1}{(1-x)^2} = 0 + 1 + 2x + 3x^2 + 4x^3 + \ldots
$$

Is this a valid formula, at least for values of $x$ in $(-1,1)$? Empirical evidence suggests it is. Setting $x = 1/2$, we get

$$
4 = \sum_{n=1}^{\infty}\frac{n}{2^{n-1}} = 1 + 1 + \frac{3}{4} + \frac{4}{8} + \frac{5}{16} + \ldots
$$

---
**Definition.** For each $n \in \mathbf{N}$, let $f_n$ be a function

---