---
title: Review of basic real analysis
date: 2022-03-29T19:23:36+02:00
math: true
tags: ["fixed-point","iteration"]
categories: ["Numerical Analysis"]
---

## Review of basic Real Analysis.

---
**Definition.** (Compactness) A set $K \subseteq \mathbf{R}$ is *compact* if every sequence in $K$ has a subsequence that converges to a limit that is also in $K$.

---

---
**Theorem.** (Characterization of Compactness) A set $K \subseteq \mathbf{R}$ is compact if and only if it is closed and bounded.

---

***Proof.***

$\Longrightarrow$ direction.

We are given that $K$ is compact. We first prove the boundedness of $K$. We proceed by contradiction. Assume that $K$ is not bounded. Then, for all $n \in \mathbf{N}$, there exists $x \in K$, such that $|x|> n$. Pick $x_1 \in K$, such that $|x_1| > 1$. Pick $x_2 \in K$, such that $|x_2| > 2$. In general, we pick $|x_n| > n$ for all $n \in \mathbf{N}$. $(x_n)$ is unbounded. Every subsequence of $(x_n)$ increases without bounds.

By definition of compact sets, every sequence in $K$ has a subsequence that converges to a limit that is also in $K$. Consequently, $(x_n)$ has a subsequence $(x_{n_k})$ such that $\lim x_{n_k}$ exists. Convergent sequences are bounded. This is a contradiction. Hence, our initial assumption is false. $K$ is bounded.

Our claim is that $K$ is closed.

Let $x$ be an arbitrary limit point of $K$. We are intereted to prove that $x \in K$. 

Since, $x$ is a limit point of $K$, there exists an sequence $(x_n) \in K$, with $x_n \neq x$ for all $n \in\mathbf{N}$, such that $\lim x_n = x$.

Since $K$ is compact, every sequence in $K$, has atleast one subsequence that converges to a limit that is also in $K$. Consequently, $(x_n)$ has a subsequence $(x_{n_m})$ such that $\lim x_{n_m} \in K$. But, $\lim x_{n_m} = \lim x_n = x$. Consequently, $x \in K$. Since, $x$ was arbitrary, this is true for all limit points of $K$. Therefore, $K$ is closed.

$\Longleftarrow$ direction.

We are given that $K$ is closed and bounded. We are interested to prove that $K$ is compact.

Let $(x_n)$ be an arbitrary sequence in $K$. Since, $(x_n)$ is a bounded sequence, by the Bolzanno Weierstrass theorem, there exists atleast one convergent subsequence $(x_{n_m})$ of $(x_n)$. Since, $K$ is closed, $\lim x_{n_m} \in K$. As $(x_n)$ was arbitrary to begin with, this holds for all sequences in $K$. Every sequence has atleast one subsequence that converges to a limit also in $K$. Therefore, $K$ is compact.

---
**Theorem.** (Nested Compact Set property).

If 

$$K_1 \supseteq K_2 \supseteq K_3 \supseteq K_4 \ldots$$

is a nested sequence of non-empty compact sets, then the intersection 

$$\bigcap_{n=1}^{\infty}K_n$$

is non-empty.

---

***Proof.***

Since $K_1, K_2, \ldots, K_n$ are non-empty, there exists elements $x_1\in K_1$, $x_2 \in K_2$ and in general $x_n \in K_n$. Thus, the sequence $(x_n) \in K_1$. Since, $K_1$ is compact, there exists a subsequence of $K_1$, call it $(x_m)$ that converges to a limit $x$ in $K_1$. Since, $\\{x_m\\}$ belongs to $K_2$, there exists a subsequence of $(x_m)$ that converges to a limit in $K_2$. But subsequence of a convergent sequence approaches the same limit as the original sequence. So, $\lim_{m \to\infty} (x_m)_{m \geq 2} = x \in K_2$. In a similar fashion, we can prove that $x \in K_n$ for all $n \in \mathbf{N}$.

Thus, the set

$$\bigcap_{n=1}^{\infty}K_n \neq \emptyset$$

This closes the proof.

---
**Definition.** Let $A \subseteq \mathbf{R}$. An open cover for $A$ is a (possibly infinite) collection of open sets $\{O_\lambda: \lambda \in \Lambda\}$ whose union contains the set $A$; that is $A \subseteq \bigcup_{\lambda \in \Lambda}O_{\Lambda}$. Given an open cover for $A$, a *finite subcover* is a finite sub-collection of open sets from the original open cover whose union still manages to completely contain $A$.

---


**Example.** Consider the open interval $(0,1)$. For each point $x\in(0,1)$. let $O_x = (x/2,1)$. Taken together, the infinite collection $\{O_x : x \in (0,1)\}$ forms an open cover for the open interval $(0,1)$. Notice, however, that it is impossible to find a finite subcover. Given any proposed finite subcollection

$$\\{O_{x_1}, O_{x_2}, \ldots, O_{x_n}\\}$$

set $x' = \min \\{x_1,x_2,\ldots,x_n\\}$ and observe that any real number $y$ satisfying $0 < y < x'/2$ is not contained in the union $\bigcup_{i=1}^{n}O_{x_i}$.

Now, consider a similar cover for the closed interval $[0,1]$. For $x \in (0,1)$, the sets $O_x = (x/2,1)$ do a fine job of covering $(0,1)$, but in order to have an open cover of the closed interval $[0,1]$,we must also cover the endpoints. To remedy this, we could fix $\epsilon > 0$, and let $O_0 = (-\epsilon,+\epsilon)$ and $O_1=(1-\epsilon,1+\epsilon)$. Then the collection 

$$\\{O_0,O_1,O_x:x\in(0,1)\\}$$

is an open cover for $[0,1]$. But this time, notice that there is a finite subcover. Because of the addition of the set $O_0$, we can choose $x'$ so that $x'/2 < \epsilon$. It follows that $\\{O_0,O_{x'},O_1\\}$ is a finite subcover for the closed interval $[0,1]$.



---
**Theorem.** (Heine-Borel Theorem) Let $K$ be a subset of $\mathbf{R}$. All of the following statements are equivalent in the sense that any one of them implies the two others:

(i) $K$ is compact.

(ii) $K$ is closed and bounded.

(iii) Every open cover for $K$ has a finite subcover.

---

***Proof.***

The equivalence of (i) and (ii) is the content of theorem on the characterization of compactness. What remains is to show that (iii) is equivalent to (i) and (ii). Let's first assume (iii), and prove that it implies (ii) (and thus (i) as well).

$\Longleftarrow$ direction.

To show that $K$ is bounded, we construct an open cover for $K$ by defining $O_x = (x - 1, x + 1)$. Clearly, $\bigcup_{x \in K}O_x$ contains $K$. Every open cover for $K$ has a finite subcover. So, there exists a finite subcover $\\{O_{x_1},\ldots,O_{x_N}\\}$ that covers $K$. Then, we have the following bounds for $K$:

$$\min_{1 \leq n \leq N}\\{x_n\\} - 1 < x \leq \max_{1 < n \leq N}\\{x_n\\} + 1$$

for all $x \in K$.

To show that $K$ is closed, we proceed by contradiction. Let $y$ be an arbitrary limit point of $K$. There exists a sequence $(y_n) \subseteq K$, such that $\lim y_n = y$. To show that $K$ is closed, we must demonstrate that $y \in K$. We assume that $y \notin K$. 

Since $y \notin K$, every $x$ is some positive distance away from $K$. We construct an open cover by taking $O_x$ to be an interval of radius $|x-y|/2$ around each point $x \in K$. The resulting open cover must have a finite subcover, so there exists $\\{O_{x_1},\ldots,O_{x_N}\\}$ that covers $K$. 

The contradiction arises, when we realize that this finite subcover cannot contain all the elements of the sequence $(y_n)$. To make this explicit, set:

$$\epsilon_0 = \min \left\\{\frac{|x_i - y|}{2}:1 \leq i \leq N \right\\}$$

$\epsilon_0$ is the distance of the point $x_i$, $1\leq i \leq N$, that is closest to $y$. Because $(y_n) \to y$, we can certainly find a term $y_N$ satisfying $|y_N - y| < \epsilon_0$. But such a $y_N$ mus tbe necessarily excluded from $\bigcup_{i=1}^{N}O_{x_i}$. This contradicts the fact that $(y_n) \subseteq K$.

Hence, our initial assumption is false. $y \in K$, and hence $K$ is closed and bounded. This closes the proof.

**Connected Sets.** Although the two open sets $(1,2)$ and $(2,5)$ have the limit point $x=2$, in common, there is still some space between them in the sense that no limit point of one of these intervals is actually contained in the other. Said another way, the closure of $(1,2)$ is disjoint from $(2,5)$, and the closure of $(2,5)$ does not intersect $(1,2)$. Notice that this same observation cannot be made about $(1,2]$ and $(2,5)$, even though these latter sets are disjoint.

---

**Definition.** (Connected Sets). Two non-empty sets $A,B \subseteq \mathbf{R}$ are separated if $cl(A) \cap B$ and $A \cap cl(B)$ are both empty. A set $E$ is disconnected, if it can be partitioned into two disjoint sets $E = A \cup B$, where $A$ and $B$ are separated. A set that is not disconnected is called a connected set.

---

**Example.** 
(i) If we let $A = (1,2)$ and $B=(2,5)$, then it is not difficult to verify that $E = A \cup B$ is disconnected. Notice that the sets $C=(1,2]$ and $D=(2,5)$ are not separated, because $C \cap cl(D) = \\{2\\}$ is not empty. This should be comforting. The union $C \cup D$  is equal to the interval $(1,5)$ which better not qualify as a disconnected set. We will prove in a moment that every interval is a connected subset of $\mathbf{R}$ and vice versa.

(ii) Let's show that the set of rational numbers is disconnected. If we let 

$$A = \mathbf{Q} \cap (-\infty,\sqrt{2}), \quad B = \mathbf{Q} \cap (\sqrt{2},\infty)$$

then we certainly have $\mathbf{Q} = A \cup B$. $A$ and $B$ are non-empty disjoint sets, therefore they are a valid partition of $\mathbf{Q}$. Any limit point of $A$ must necessaily fall in $(-\infty,\sqrt{2}]$ by the order limit theorem. Because this is disjoint from $B$ , we get $cl(A) \cap B = \emptyset$. We can similarly show that $A \cap cl(B) = \emptyset$. Thus, $\mathbf{Q}$ is disconnected.

---
**Theorem.** A set $E \subseteq \mathbf{R}$ is connected if and only if, for all non-empty disjoint sets satisfying $E = A \cup B$, there always exists a convergent sequence $(x_n) \to x$, with $(x_n)$ contained in one of $A$ or $B$, and $x$ an element of the other.

---

***Proof.*** 

$\Longrightarrow$ direction.

Negating the definition of connected sets, we have - 

A set $E$ is connected, if for all non-empty disjoint sets $A$, $B$ satisfying $E = A\cup B$, atleast one of $cl(A) \cap B \neq \emptyset$ or $A \cap cl(B) \neq \emptyset$.

Consequently, there exists an element $x \in cl(A) \cap B$ or $x \in A \cap cl(B)$. 

Since, $A$ and $B$ are disjoint non-empty sets, $A \cap B = \emptyset$. So, $x \notin A \cap B$. Thus, we have the possibilities:

(i) $x \in A, x \notin B$.

(ii) $x \notin A, x \in B$.

(iii) $x \notin A, x \notin B$.

If $x \in A, x \notin B$, then $x \in A \cap cl(B)$ must be true (The other possibility cannot hold). So, $x$ is a limit point of $B$. $x \in cl(B) \setminus B$. There exists a convergent sequence $(x_n) \subseteq B$, such that $\lim x_n = x$.

If $x \notin A, x \in B$, then $x \in cl(A) \cap B$ must be true. So, $x$ is a limit point of $A$. $x \in cl(A) \setminus A$. There exists a convergent sequence $(x_n) \subseteq A$, such that $\lim x_n = x$.

The third possibility is rejected, because it would mean that $x$ is neither in $cl(A) \cap B$, nor in $A \cap cl(B)$, which is false.

In both cases (i) and (ii), there exists a convergent sequence $(x_n) \to x$, with $(x_n)$ contained in one of $A$ or $B$, and $x$ an element of the other.

$\Longleftarrow$ direction.

We proceed by contradiction. We are given that, for all non-empty disjoint sets $A$, $B$, satisfying $E = A \cup B$, there exists a convergent sequence $(x_n) \to x$, with $(x_n)$ contained in one of the sets, and $x$ in the other set.

Assume that $E$ is disconnected. By definition, there exists a partition $C|D$ of $E$, such that both $cl(C) \cap D = \emptyset$ and $C \cap cl(D) = \emptyset$. 

Since $C|D$ is a valid partition of $E$, there exists a convergent sequence $(x_n)\to x$, such that $(x_n)$ is contained in one of $C$, $D$, whilst $x$ is contained in the other.

Thus, atleast one of $cl(C) \cap D$ and $C \cap cl(D)$ is non-empty.

But, this is a contradiction. Our initial assumption must be false. $E$ is a connected set. 

The concept of connectedness is more relevant when working with subsets of the plane and other higher dimensional spaces. This is because in $\mathbf{R}$, the connected sets coincide precisely with the collection of intervals (with the understanding that unbounded intervals $(-\infty,3)$ and $(0,\infty)$ are inclded.

---
**Theorem.** (Characterization of connected sets) A set $E \subseteq \mathbf{R}$ is connected if and only if whenever $a < c < b$ with $a,b \in E$, it follows that $c \in E$.

---

***Proof.***

$\Longrightarrow$ direction.

We are given that $E$ is connected. We proceed by contradiction. Assume that, if whenever $a,b \in E$, with $a < c < b$, then $c \notin E$.

Let $A = E \cap (-\infty,c)$ and $B = E \cap (c,\infty)$. Clearly, $A,B$ are non-empty disjoint subsets of $E$ satisfying $E = A \cup B$, so $A | B$ is a partition of $E$.

Any limit point of $A$ lies in $(-\infty,c]$ by the order limit theorem, so $cl(A) \cap B = \emptyset$. By similar logic, $A \cap cl(B) = \emptyset$. Thus, we have found a partition $A|B$ of $E$, that is separate. By definition, $E$ is disconnected. This is a contradiction. Our initial assumption must be false.

If whenever $a,b \in E$, with $a < c < b$, then $c \in E$.

$\Longleftarrow$ direction.

We are interested to prove that $E$ is connected. We must show that, for all partitions $A|B$ of $E$, there exists a convergent sequence $(x_n) \to x$, such that $(x_n)$ belongs to one of $A$,$B$, with $x$ belonging to the other set.

Let's take an arbitrary partition of $E$. Let $A$, $B$ be non-empty disjoint sets satisfying $E = A \cup B$. $A|B$ is a partition of $E$. 

Since $A$, $B$ are non-empty, there exists elements $a \in A$ and $b \in B$.

Let $I_1 = [a_1,b_1] = [a,b]$. 

We compute the midpoint of the straight-line joining $a_1$ and $b_1$.

$$m = \frac{a_1 + b_1}{2}$$

Since $a_1 < \frac{a_1 + b_1}{2} < b_1$, with $a_1$, $b_1$ belonging to $E$, it follows that $(a_1+b_1)/2 \in E$. Thus, either $(a_1 + b_1)/2 \in A$ or $(a_1+b_1)/2 \in B$.

If $(a_1+b_1)/2 \in A$, we let $a_2 = (a_1 + b_1)/2$, $b_2 = b_1$, $I_2 = [a_2,b_2]$.

If $(a_1+b_1)/2 \in B$, we let $a_2 = a_1$, $b_2 = (a_1 + b_1)/2$, $I_2 = [a_2,b_2]$.

We can continue this construction indefinitely. Now,

$$I_1 \subseteq I_2 \subseteq I_3 \ldots \subseteq I_n \subseteq I_{n+1} \subseteq \ldots $$

By the nested interval property,

$$\bigcap_{n=1}^{\infty} I_n \neq \emptyset$$

and there exists 

$$x \in \bigcap_{n=1}^{\infty} I_n$$

with $\lim a_n = x$ and $\lim b_n = x$.

Since $a_n \leq x \leq b_n$ and $a_n$, $b_n$ belong to $E$ for all $n \in \mathbf{N}$, it follows that $x \in E$. But, it means, either $x \in A$ or $x \in B$. 

If $x \in A$, then from the fact that $\lim b_n = x$, we have a convergent sequence $(x_n)$ in $B$, and it's limit point $x$ in $A$.

If $x \in B$, then from the fact that $\lim a_n = x$, we have a convergent sequence $(x_n)$ in $A$, and it's limit point $x$ in $B$.

As $A|B$ was an arbitrary partition of $E$ to begin with, this holds true for all partitions of $E$. 

Consequently, $E$ is connected.

---
[Abbott 3.4.5] Let $A$ and $B$ be non-empty subsets of $\mathbf{R}$. Show that if there exist disjoint open sets $U$ and $V$ with $A \subseteq U$ and $B \subseteq V$, then $A$ and $B$ are separated.

---

***Proof.***

If $A$ and $B$ have no limit points, then $cl(A) = A$ and $cl(B) = B$. So, $cl(A) \cap B = \emptyset$ and $A \cap cl(B) = \emptyset$ and therefore $A$ and $B$ are separated. And we are done.

Let's assume that atleast one of $A$, $B$ has a limit point. 

Suppose $x$ is an arbitrary limit point of $A$. There exists a sequence $(x_n) \subseteq A$, with $x_n \neq x$ for all $n \in \mathbf{N}$, such that $(x_n) \to x$. Since, $A \subseteq U$, it follows that $(x_n) \subseteq U$. So, $x$ is a limit point of $U$.

We are interested to prove that $x \notin V$. For the sake of contradiction, assume that $x \in V$. Since $V$ is an open set, there exists an $\epsilon-$ball around $x$, $V_\epsilon(x)=(x-\epsilon,x+\epsilon)$ that is contained in $V$. Since, $U$ and $V$ are disjoint, $(x - \epsilon,x+\epsilon) \cap U = \emptyset$. Since, $x$ is a limit point of $U$, we must have that, $(x-\epsilon,x+\epsilon)$ intersects $U$ in atleast one point other than $x$. So, $(x - \epsilon,x+\epsilon) \cap U \neq \emptyset$. This is a contradiction. Our initial assumption is false. It follows that $x \notin V$. This implies, $x \notin B$. Since, $x$ was arbitrary, we conclude that $cl(A) \cap B = \emptyset$.

We can similarly argue that if $x$ is an arbitrary limit point of $B$, it does not belong to $A$. 

Consequently, $A$ and $B$ are separated.



