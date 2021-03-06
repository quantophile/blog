---
title: Null Sets
date: 2022-03-18T19:24:24+01:00
math: true
tags: ["null-sets", "measure-theory"]
categories: ["Measure Theory"]
---

The idea of a 'negligible' set relates to one of the limitations of the Riemann integral, as we saw in the previous chapter. Since the function $f = \mathbf{1}_\mathbf{Q}$ takes a non-zero value only on $\mathbf{Q}$ and equals $1$ there, the area under it's graph (if such makes sense) must be very closely linked to the length of the set $\mathbf{Q}$. This is why it turns out we cannot integrate $f$ in the Riemann sense: the sets $\mathbf{Q}$ and $\mathbf{R}\setminus \mathbf{Q}$ are so different from intervals that it is not clear how we should measure their lengths and it is clear that the integral of $f$ over $[0,1]$ should equal the length of the set of rationals in $[0,1]$. So, how should we define this concept for more general sets?

The obvious way of defining the length of a set is to start with intervals nonetheless. Suppose that $I$ is a bounded interval of any kind $I = [a,b]$, $I=(a,b]$ or $I = (a,b)$. We simply define the length of $I$ as $l(I) = b - a$ in each case.

As a particular case, we have $l(\\{a\\}) = l([a,a]) = 0$. It is then natural to say that the one-element set is null. Before we extend this idea to more general sets, first consider the length of a finite set. A finite set is not an interval but since a single point has length $0$, adding finitely many such lengths together should still give $0$. The underlying concept here is, if we decompose a set into a finite number of disjoint intervals, we compute the the length of this set by adding the lengths of the pieces. 

As we have seen, in general, it may not always be possible actually to decompose a set into intervals. Therefore, we consider systems of intervals that cover a given set. We shall generalize the above idea by allowing a countable number of covering intervals. Thus, we arrive at the following more general definition of sets of zero length:

---
**Definition.** (Null Set) A null set $A \subseteq \mathbf{R}$ is a set that may be covered by a sequence of intervals of arbitrarily small total length, i.e. given any $\epsilon > 0$, we can find a sequence $\\{I_n: n\geq 1\\}$ of intervals such that 

$$A \subseteq \bigcup_{k=1}^{\infty} I_n$$

and 

$$\sum_{n=1}^{\infty}l(I_n) < \epsilon$$

---

Note that the intervals do not need to be disjoint. It follows at once from the definition that the empty set is null. Next, any one-element $\\{x\\}$ is a null set. For, let $\epsilon > 0$ and take $I_1=(x - \epsilon/4,x+\epsilon/4)$, $I_n=(0,0)$ for $n \geq 2$. Now,

$$\sum_{n=1}^{\infty} l(I_n) = l(I_1) = \frac{\epsilon}{2} < \epsilon$$

More generally, any countable set $A = \{x_1,x_2,\ldots,\}$ is null. The simplest way to show this is to take $I_n = [x_n,x_n]$ for all $n$. However, as a gentle introduction to the next theorem we will cover $A$ by open intervals. This way it is more fun.

For let $\epsilon > 0$ and cover $A$ with the following sequence of intervals:

\begin{align\*}
I_1 &= \left(x_1 - \frac{\epsilon}{8}, x_1 + \frac{\epsilon}{8}\right) \quad &l(I_1) &= \frac{\epsilon}{4}\\\\
I_2 &= \left(x_2 - \frac{\epsilon}{16}, x_2 + \frac{\epsilon}{16}\right) \quad &l(I_2) &= \frac{\epsilon}{8}\\\\
I_3 &= \left(x_3 - \frac{\epsilon}{32}, x_2 + \frac{\epsilon}{32}\right) \quad &l(I_3) &= \frac{\epsilon}{16}\\\\
\vdots\\\\
I_n &= \left(x_n - \frac{\epsilon}{2^{n+2}}, x_2 + \frac{\epsilon}{2^{n+2}}\right) \quad &l(I_n) &= \frac{\epsilon}{2^{n+1}}
\end{align\*}

Since $\sum_{n=1}^{\infty}\frac{1}{2^n} = 1$,

$$\sum_{n=1}^{\infty}l(I_n) = \epsilon/2 < \epsilon$$

as needed.

Here we have the following situation: $A$ is the union of countably many one-element sets. Each of them is null and $A$ turns out to be null as well. We can generalize this simple observation. 

---
**Theorem**. If $(A_n)_{n \geq 1}$ is sequence of null sets, then their countable union 

$$A = \bigcup_{n=1}^{\infty}A_n$$

is also null. 

---

***Proof.***

We are interested to prove that the countable union of null sets is null. We assume that all $A_j$, $j\geq 1$ are null and to show that the same is true for $A$, we pick any arbitrary $\epsilon > 0$. Our goal is to cover the set $N$ by countably many intervals with total length less than $\epsilon$. The proof goes in three steps, each being a little tricky.

**Step 1.** We carefully cover each $A_j$ by open intervals.

Carefully, means that the lengths have to be small. 'Small' means that we are going to add them up later to end up with a small number (and 'small' here means less than $\epsilon$).

Since $A_1$ is null, there exists intervals $I_k^1,k \geq 1$, such that:

$$\sum_{k=1}^{\infty}l(I_k^1) < \frac{\epsilon}{2}, A_1 \subseteq \bigcup_{k=1}^{\infty}I_k^1$$ 

For $A_2$, we find a system of intervals $I_k^2$, $k \geq 1$, with

$$\sum_{k=1}^{\infty}l(I_k^2) < \frac{\epsilon}{4}, A_2 \subseteq \bigcup_{k=1}^{\infty}I_k^2$$ 

You can see a cunning plan of making the total lengths smaller at each step at a geometric rate. In general, we cover $A_n$ with the intervals $I_k^n$, $k \geq 1$ whose total length is less than $\frac{\epsilon}{2^n}$:

$$\sum_{k=1}^{\infty}l(I_k^n) < \frac{\epsilon}{2^n}, A_n \subseteq \bigcup_{k=1}^{\infty}I_k^n$$ 

**Step 2.** We arrange the countable family of intervals $\\{I_k^n\\}$ into a sequence $J_j$, $j \geq 1$. For instance, we put $J_1 = I_1^1$, $J_2 = I_2^1$, $J_3 = I_1^2$, $J_4 = I_3^1$, $J_5 = I_2^2$, $J_6 = I_1^3$ etc. This way, none of the $I_k^n$ are skipped. The union of the new system of intervals is the same as the union of the old one and so

$$A = \bigcup_{n=1}^{\infty}A_n \subseteq \bigcup_{n=1}^{\infty}\bigcup_{k=1}^{\infty}I_k^n = \bigcup_{j=1}^{\infty}J_j$$

**Step 3.** Compute the total length of $J_j$.

This is tricky because we have a series of numbers of two indices:

$$\sum_{j=1}^{\infty}l(J_j) = \sum_{n=1}^{\infty}\sum_{k=1}^{\infty}l(I_k^n)$$

Now, we wish to write this series of numbers each being the sum of a series. We can rearrange the double sum because the components are non-negative (a fact from elementary calculus).

$$\sum_{n=1}^{\infty}\sum_{k=1}^{\infty}l(I_k^n) < \sum_{n=1}^{\infty}\frac{\epsilon}{2^n} = \epsilon$$

which completes the proof.

Thus any countable set is null, and null sets appear to be closely related to countable sets - this is no surprise as any proper interval is uncountable, so any countable subset is quite sparse when compared with an interval, hence makes no real contribution to its length. (You may have also noticed the similarity between step 2 in the above proof and the diagonal argument which is used to show that $\mathbf{Q}$ is a countable set).

However, uncountable sets can be null, provided their points are sufficiently sparsely distributed as the following famous example, due to Cantor, shows:

1. Start with the interval $C_0=[0,1]$ and remove the open middle one third, that is the interval $\left(\frac{1}{3},\frac{2}{3}\right)$, obtaining the set $C_1$, which consists of the two intervals $\left[0,\frac{1}{3}\right]$ and $\left[\frac{2}{3},1\right]$.

2. Next remove the open middle one third 

[Capinski 2.1] Show that we get an equivalent notion if in the above definition, we replace the word *intervals* by any of (i) open intervals (ii) closed intervals (iii) intervals of the form $(a,b]$ (iv) intervals of the form $[a,b)$. 

