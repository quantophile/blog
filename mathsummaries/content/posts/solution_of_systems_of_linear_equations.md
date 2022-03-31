---
title: Solution of systems of linear equations
date: 2022-03-30T17:32:54+02:00
math: true
tags: ["Linear Equations"]
categories: ["Numerical Analysis"]
---

Previously, we consider the solution of a single equation of the form $f(x) = 0$, where $f$ is a real-valued function defined and continuous on a closed interval of the real line. The simplest example of this kind is the linear equation $ax = b$, where $a$ and $b$ are given real numbers, with $a \neq 0$, whose solution is

$$x = a^{-1}b$$

trivially. Of course, we could have expressd the solution as $x = b/a$ as in the previous post, but as we will see in a moment, writing $x = a^{-1}b$ is much more revealing in the present context. In this post, we shall consider a different generalization of this elementary problem:

Let $A$ be an $n \times n$ matrix with $a_{ij}$ as its entry in row $i$ and column $j$ and $\mathbf{b}$ be a given column vector of size $n$ with the $j$th entry $b_j$. We are interested to find a column vector $\mathbf{x}$ of size $n$ such that $A\mathbf{x} = \mathbf{b}$.

Denoting by $x_i$, the $i$th entry of the vector $\mathbf{x}$, wecan also write $A\mathbf{x} = \mathbf{b}$ in the following expanded form:

\begin{align\*}
a_{11}x_1 + a_{12}x_2 + \ldots + a_{1n}x_n &= b_1,\\\\
a_{21}x_1 + a_{22}x_2 + \ldots + a_{2n}x_n &= b_2,\\\\
\vdots\\\\
a_{n1}x_1 + a_{n2}x_2 + \ldots + a_{nn}x_n &= b_n
\end{align\*}

