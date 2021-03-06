---
title: Joint Distributions
date: 2022-02-11T21:22:12+01:00
math: true
tags: ["probability", "joint-distributions", "multi-variate-gaussian"]
categories: ["Stochastic Calculus"]
---

The individual distributions of two random variables do not tell us anything about whether the random varaibles are independent or dependent. Although, the PMF of $X$ is a complete blueprint for the distribution of $X$ and the PMF of $Y$ is a complete blueprint for the distribution of $Y$, these individual PMFs are missing important information about the dependence structure of $X$ and $Y$.

Of course, in real life, we usually care about the relationship between multiple random variables in the same experiment. To give just a few examples:

- Medicine : To evaluate the effectiveness of a treatement, we may take multiple measurements per patient, an ensemble of blood pressure, heart rate, and cholesterol reading can be more informative than any of these measurements considered separately.
- Genetics : To study the relationships between various genetic markers and a particular disease, if we only looked separately at distributions for each genetic marker, we could fail to learn about whether an interaction between the markers is related to the disease. 
- Time-Series: To study how something evolves over time, we can often make a series of measurements over time, and then study the series jointly. There are many applications of such series, such as global temperatures, stock prices, or national unemployment rates. The series of measurements considered jointly can help us deduce trends for the purpose of forecasting future measurements.

This blog-post considers *joint-distributions*, also called *multi-variate distributions*, which capture the previously missing information about how multiple random variables interact. We introduce multivariate analogs of the CDF, PMF and the PDF in order to provide a complete specification of the relationship between multiple random variables. After this ground-work is in place, we'll study a couple of famous named multivariate distributions, generalizing the Binomial and Normal distributions to higher dimensions.

## Joint, Marginal and Conditional.

The three key concepts for this section are *joint, marginal* and *conditional* distributions. Recall that the distribution of a single random variable $X$ provides complete information about the probability of $X$ falling into any subset of the real line. Analogously, the joint distribution of two random variables $X$ and $Y$ provides complete information about the probability of the vector $(X,Y)$ falling into any subset of the plane. The *marginal* distribution of $X$ is the individual distribution of $X$, ignoring the value of $Y$ and the conditional distribution of $X$ given $Y=y$ is the updated distribution for $X$ after obsering $Y=y$. We'll look at these concepts in the discretecase first, then extend them to the continuous case. 

### Discrete.

The most general description of the joint distribution of two random variables is the joint CDF, which applies to discrete and continuous random variables alike.

---
**Definition.** (Joint CDF). The *joint* CDF of the random variables $X$ and $Y$ is the function $F_{X,Y}$ given by :

$$F_{X,Y}(x,y) = P(X \leq x, Y \leq y)$$

---

The joint CDF of a vector $n$ random variables $(X_1,X_2,\ldots,X_n)$ is described analogously.

Unfortunately, the joint CDF of discrete random variables is not a well-behaved function; as in the univariate case, it consists of jumps and flat regions. For this reason, with discrete random variables, we usually work with the joint PMF, which also determines the joint distribution and is much easier to visualize.

---
**Definition.** (Joint PMF). The *joint* PMF of discrete random variables $X$ and $Y$ is the function $f_{X,Y}$ given by,

$$f_{X,Y}(x,y) = P(X = x,Y=y)$$

---

The joint PMF of a vector of $n$ discrete random variables $(X_1,X_2,\ldots,X_n)$ is described analogously.

Just as univariate PMFs must be nonnegative and sum to $1$, we require valid joint PMFs to be non-negative and sum to $1$, where the sum is taken over all possible values of $X$ and $Y$:

$$\sum_{x} \sum_{y}P(X = x,Y = y) = 1$$

The joint PMF determines the distribution because we can use it to find the probability of the event $(X,Y) \in A$ for any set $A$ of points in the support of $(X,Y)$.  All we have to do is sum the joint PMF over $A$:

$$P((X,Y) \in A) = {\sum\sum}_{(x,y) \in A} P(X = x, Y = y)$$

From the joint distribution $(X,Y)$  we can easily get the distribution of $X$ alone by summing over the possible values of $Y$. This gives us the familiar PMF of $X$ that we have seen earlier. In the context of joint distributions, we will call it the *marginal* or unconditional distribution of $X$, to make it clear that we are referring to the distribution of $X$ alone, without regard for the value of $Y$.

---
**Definition.** (Marginal PMF). For discrete random variables $X$ and $Y$, the marginal PMF of $X$ is

\begin{align\*}
f_X(x) &= P(X = x) = \sum_{y} f_{X,Y}(x,y) = \sum_{y} P(X = x, Y = y) \\\\
f_Y(y) &= P(X = y) = \sum_{x} f_{X,Y}(x,y) = \sum_{x} P(X = x, Y = y) 
\end{align\*}

---

**Example.** Suppose a dice is rolled $N = 5$ times. Let $X$ be the number of ones and $Y$ be the number of twos. The pair $(X,Y)$ follows the $Multinomial(5,1/6,1/6)$ distribution. The joint PMF $f_{X,Y}(x,y)$ can be computed as follows.

```python
import numpy as np
from scipy.special import binom

class multinomial:
    def __init__(self, numTrials, successProbabilities):
        self.n = numTrials
        self.p = successProbabilities

    def pmf(self, x):
        size = len(x)

        probability = 1.0; k = 0; sumProbabilities = 0.0;

        for j in range(size):
            probability = probability * binom(self.n - k,x[j]) * (self.p[j]**x[j])
            k += x[j]
            sumProbabilities += self.p[j]

        if sumProbabilities < 1.0:
            probability = probability * (1 - sumProbabilities)**(self.n - k)

        return probability
```

We can now create a multinomial random variable and print it's joint PMF.

```python
if __name__ == "__main__":
    rv = multinomial(numTrials=5,successProbabilities=[1/6,1/6])

    x = np.array([0,1,2,3,4,5])
    y = np.array([0,1,2,3,4,5])

    jointPMF = np.zeros(shape=(6,6))
    for j in range(6):
        for k in range(6):
            jointPMF[j][k] = rv.pmf([x[j],y[k]])

    print(jointPMF)
```

Output:

```
[[ 1.317e-01  1.646e-01  8.230e-02  2.060e-02  2.600e-03  1.000e-04]
 [ 1.646e-01  1.646e-01  6.170e-02  1.030e-02  6.000e-04  0.000e+00]
 [ 8.230e-02  6.170e-02  1.540e-02  1.300e-03  0.000e+00  0.000e+00]
 [ 2.060e-02  1.030e-02  1.300e-03  0.000e+00  0.000e+00  0.000e+00]
 [ 2.600e-03  6.000e-04  0.000e+00  0.000e+00  0.000e+00  0.000e+00]
 [ 1.000e-04  0.000e+00 -0.000e+00  0.000e+00 -0.000e+00  0.000e+00]]
```

The probability of the event $\\{X = x_j, Y = y_k\\}$ is given by `jointPMF[j][k]`.

The marginal PMF of $X$ and $Y$ can be easily computed as:

```python
print("\nMarginal PMF of X")
print(np.sum(jointPMF, axis=0))

print("\nMarginal PMF of Y")
print(np.sum(jointPMF, axis=1))
```

Output:

```
Marginal PMF of X
[4.019e-01 4.018e-01 1.607e-01 3.220e-02 3.200e-03 1.000e-04]

Marginal PMF of Y
[4.019e-01 4.018e-01 1.607e-01 3.220e-02 3.200e-03 1.000e-04]
```

Clearly, if we only know the marginal PMFs, there is no way to recover the joint PMF without further assumptions.

Another way to go from joint to marginal distributions is via the joint CDF. In that case, we take a limit rather than a sum: the marginal CDF of $X$ is:

$$F_X(x) = P(X \leq x) = \lim_{y \to \infty} P(X \leq x, Y \leq y) = \lim_{y \to \infty} F_{X,Y}(x,y)$$

However as mentioned above it is usually easier to work with joint PMFs.

Now, suppose that we observe the value of $X$ and want to update our distribution of $Y$ to reflect this information. Instead of using the marginal PMF $P(Y = y)$, which does not take into account any information about $X$, we should use a PMF that conditions on the event $\{X = x\}$, where $x$ is the value we observed for $X$. This naturally leads us to consider conditional PMFs.

---
**Definition.** (Conditional PMF). 

For discrete random variables $X$ and $Y$, the conditional PMF of $X$ given $Y = k$ is,

$$
f_{X|Y=k}(x) = P(X = x|Y = k) = \frac{P(X = x, Y = k)}{P(Y = k)} = \frac{f_{X,Y}(x,k)}{f_Y(k)}
$$

The conditional PMF of $Y$ given $X = k$ is,

$$
f_{Y|X=k}(y) = P(Y = y|X = k) = \frac{P(Y = y, X = x)}{P(X = k)} = \frac{f_{X,Y}(k,y)}{f_X(k)}
$$

---

For instance, in the dice example, the conditional PMF of the number of ones, i.e. $X$, given that we observe two, $3$ times, i.e. $Y=3$ is given by:

```python
print("\nConditional PMF P(X=x|Y=3)")
conditionalPMF = jointPMF[:][3]/np.sum(jointPMF[:][3])
print(conditionalPMF)
```

Output:

```
Conditional PMF P(X=x|Y=3)
[0.6398 0.3199 0.0404 0.     0.     0.    ]
```

---
**Definition.** (Independence of discrete random variables). The random variables $X$ and $Y$ are said to be independent, if for all $x,y \in \mathbb{R}$, we have:

$$F_{X,Y}(x,y) = F_X(x) \cdot F_Y(y)$$

---

If $X$ and $Y$ are discrete, this is equivalent to the condition:

$$P(X = x, Y =y) = P(X = x)\cdot P(Y = y)$$

$\forall x,y \in \mathbb{R}$ and it is also equivalent to the condition:

$$P(Y = y|X = x) = P(Y = y)$$

$\forall x,y \in \mathbb{R}$ such that $P(X = x) > 0$.

Using the terminology from this post, the definition says that for independent random variables, the joint CDF factors into the product of the marginal CDFs, or that the joint PMF factors into the product o the marginal PMFs. Remember that in general, marginal distributions do not determine the joint distribution: this is the reason why we wanted to study joint distributions in the first place! But, in the special case of independence, the marginal distributions are all we need in order to specify the joint distribution; we can get the joint PMF by multiplying the marginal PMFs.

Another way of looking at independence is that all the conditional PMFs are the same as the marginal PMF. That is, starting with the marginal PMF of $Y$, no updating is necessary when we condition on the event $\\{X = x_j\\}$, regardless what $x_j$ is.

We'll do one more example of discrete joint distribution to round out this section. We've named it the chicken-egg story; in it, we use wishful thinking to find a joint PMF, and our efforts land us a surprising independence result.

**Story.** (Chicken-Egg). Suppose a chicken lays a random number of eggs, $N$, where $N \sim Poisson(\lambda)$. Each egg independently hatches with probability $p$ and fails to hatch with probability $q = 1 - p$. Let $X$ be the number of eggs that hatch and $Y$ the number that do not hatch, so $X + Y = N$. What is the joint PMF of $X$ and $Y$?

*Solution:*

We seek the joint PMF $P(X = x_j,Y = y_k)$ for non-negative integers $x_j$, $y_k$. Conditional on the total number of eggs $N$, the eggs are independent Bernoulli trials with probability of success $p$, so by the story of the binomial and further $X$ and $Y$ are conditionally dependent, because $Y = N - X$. Thus, we can write:

\begin{align\*}
f_{X,Y}(x_j,y_k) &= P(X = x_j, Y = y_k)\\\\
&= P(X = x_j, Y = y_k, N = x_j + y_k)\\\\
&= P(X = x_j, Y = y_k | N = x_j + y_k) \cdot P(N = x_j + y_k)\\\\
&= {x_j + y_k \choose x_j}p^{x_j}q^{y_k} \cdot e^{-\lambda} \frac{\lambda^{(x_j + y_k)}}{(x_j + y_k)!}\\\\
&= \frac{(x_j + y_k)!}{x_j! y_k!}p^{x_j}q^{y_k} \cdot e^{-\lambda(p+q)} \frac{\lambda^{(x_j + y_k)}}{(x_j + y_k)!}\\\\
&= e^{-\lambda p} \frac{(\lambda p)^{x_j}}{x_j!} \cdot e^{-\lambda q} \frac{(\lambda q)^{y_k}}{y_k!}
\end{align\*}

The joint PMF factors into the product of the $Poisson(\lambda p)$ PMF (as a function of $x$) and the $Poisson(\lambda q)$ PMF (as a function of $y$). This tells us two elegant facts: (1) $X$ and $Y$ are independent, since their joint PMF is the product of their marginal PMFs, and (2) $X \sim Poisson(\lambda p)$ and $Y \sim Poisson(\lambda q)$. 

At first it may seem deeply counterintuitive that $X$ is unconditionally independent of $Y$. Doesn't knowing that a lot of eggs hatched mean that there are probably not so many that didn't hatch? For a *fixed* number of eggs, this independence would be impossible: knowing the number of hatched eggs would perfectly determine the number of unhatched eggs. But, in this example, the number of eggs is random, following a Poisson distribution. Without any advanced knowledge of the total number of eggs, the number of eggs reveals no additional information about the number of unhatched ones.

The chicken-egg story supplements the following result:

---
**Theorem.** If $X \sim Poisson(\lambda p)$, $Y \sim Poisson(\lambda q)$, and $X$ and $Y$ are independent, then $N = X + Y \sim Poisson (\lambda)$ and $X|N = n \sim Binomial(n,p)$.

---

*Proof.* 

Let $X \sim Poisson(\lambda p)$ and $Y \sim Poisson(\lambda q)$ be independent random variables. Let $N = X + Y$. We have:

\begin{align\*}
P(N = n) &= P(X + Y = n) \\\\
&= \sum_{x} P(X + Y = n | X = x) P(X = x) \quad \\{ \text{Law of total probability}\\}\\\\
&= \sum_{x} P(Y = n - x | X = x) P(X = x) \\\\
&= \sum_{x} P(Y = n - x) \cdot P(X = x) \quad \\{ X \text{ is independent of } Y\\} \\\\
&= \sum_{x} e^{-\lambda q} \frac{(\lambda q)^{n-x}}{(n - x)!} \cdot e^{-\lambda p} \frac{(\lambda p)^x}{x!}\\\\
&= e^{-\lambda} \frac{\lambda^n}{n!} \sum_{x} \frac{n!}{(n-x)!x!} p^x q^{n - x} \\\\
&= e^{-\lambda} \frac{\lambda^n}{n!} \sum_{x} {n \choose x} p^x q^{n - x} \\\\
&= e^{-\lambda} \frac{\lambda^n}{n!} (p + q)^n \\\\
&= e^{-\lambda} \frac{\lambda^n}{n!}
\end{align\*}

Thus, $N \sim Poisson (\lambda)$.

Further, we wish to prove that the conditional on $N = n$, $X$ is a binomial random variable. We have:

\begin{align\*}
f_{X|N = n}(x) &= P(X = x|N = n) \\\\
&= \frac{P(X = x, N = n)}{P(N = n)}\\\\
&= \frac{P(N = n | X = x) \cdot P(X = x)}{P(N = n)} \\\\
&= \frac{P(Y = n - x|X = x)P(X = x)}{P(N = n)} \\\\
&= \frac{P(Y = n - x)P(X = x)}{P(N = n)} \quad \\{ X \text{ is independent of } Y\\} \\\\
&= \frac{e^{-\lambda p}\frac{(\lambda p)^x}{x!} \cdot e^{-\lambda q}\frac{(\lambda q)^{n - x}}{(n-x)!}}{e^{-\lambda}\frac{(\lambda)^n}{n!}} \\\\
&= {n \choose x} p^x q^{n - x}
\end{align\*}

Consequently, $X|N = x \sim Binomial(n,p)$.

By the Chicken-egg story, we now have the converse to this theorem. 

---
**Theorem.** If $N \sim Poisson(\lambda)$ and $X|N = n \sim Binomial(n,p)$, then $X \sim Poisson(\lambda p)$, $Y = N - X \sim Poisson(\lambda q)$, and $X$ and $Y$ are independent.

---

### Continuous.

Once we have a handle on discrete joint distributions, it isn't much harder to consider continuous joint distributions. We simply make the now-familiar substitutions of integrals for sums and PDFs for PMFs, remember that the probability of any individual point is now $0$. 

Formally, in order for $X$ and $Y$ to have a continuous joint distribution, we require that the joint CDF

$$F_{X,Y}(x,y) = P(X \leq x, Y \leq y)$$

be differentiable with respect to $x$ and $y$. The partial derivative with respect to $x$ and $y$ is called the joint PDF. The joint density function characterizes the joint distribution, as does the joint CDF.

---
**Definition.** (Joint PDF). If $X$ and $Y$ are continuous with joint CDF $F_{X,Y}(x,y)$, their joint PDF is the derivative of the joint CDF with respect to $x$ and $y$:

$$f_{X,Y}(x,y) = \frac{\partial^2}{\partial x \partial y}F_{X,Y}(x,y)$$

---

We require valid joint PDFs to be nonnegative and integrate to $1$:

$$
f_{X,Y}(x,y) \geq 0 \quad \text{and } \int_{\infty}^{\infty} \int_{-\infty}^{\infty} f_{X,Y}(x,y) dx dy = 1
$$

In the univariate case, the PDF was the function we integrated to get the probability of an interval. Similarly, the joint PDF of two random variables is the function we integrate to get the probability of a two dimensional region. For example,

$$
P(X < 3, 1 < Y < 4) = \int_{1}^{4} \int_{-\infty}^{3} f_{X,Y}(x,y) dx dy
$$

For a general region $A \subseteq \mathbb{R}^2$, 

$$
P((X,Y) \in A) = \int_A \int f_{X,Y}(x,y) dx dy
$$

When we integrate the joint PDF over a region $A$, we are calculating the volume under the surface of the joint PDF and above $A$. Thus, probability is represented by *volume under the joint* PDF. The total volume under a valid joint PDF is $1$.

In the discrete case, we get the marginal PMF of $X$ by summing over all possible values of $Y$ in the joint PMF. In the continuous case, we get the *marginal* PDF of $X$ by integrating over all possible values of $Y$ in the joint PDF.

---
**Definition.** (Marginal Density.) For continuous random variables $X$ and $Y$ with the joint density $f_{X,Y}$, the marginal density of $X$ is 

$$f_{X}(x) = \int_{-infty}^{\infty}f_{X,Y}(x,y) dy$$

---

This is the density of $X$, viewing $X$ individually rather than jointly with $Y$.

On similar lines, if we have the joint density of $X,Y,Z,YW$ but want the joint density of $X,W$, we just have to integrate over all possible values of $Y$ and $Z$:

$$
f_{X,W}(x,w) = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} f_{X,Y,Z,W}(x,y,z,w) dy dz
$$

Conceptually, this is easy - just integrate over the unwanted variables to get the joint PDF of the wanted variables - but computing it may or may not be easy.

Returning to the case of the joint distribution of two random variables $X$ and $Y$, let's consider how to update our distribution for $Y$ after observing the value of $X$, using the conditional density function.

---
**Definition.** For continuous random variables $X$ and $Y$ with the joint density function $f_{X,Y}$, the conditional density of $Y$ given $X = x$ is,

\begin{align\*}
f_{Y|X}(y|x) = \frac{f_{X,Y}(x,y)}{f_X(x)}
\end{align\*}

---

for all $x$ with $f_X(x) > 0$. This is considered as a function of $y$ for fixed $x$. As a convention, in order to make $f_{Y|X}(x)$ well-defined for all real $x$, let $f_{Y|X}(y) = 0$ for all $x$ with $f_X(x) = 0$.

Note that, we can recover the joint density function $f_{X,Y}$, if we have the conditional density $f_{Y|X}$ and the corresponding marginal $f_X$:

$$
f_{X,Y}(x,y) = f_{Y|X=x}(y|x) \cdot f_X(x)
$$

Similarly, we can recover the joint density if we have $f_{X|Y=y}$ and $f_Y$:

$$
f_{X,Y}(x,y) = f_{X|Y}(x|y) f_Y(y)
$$

This allows us to develop the continuous versions of the Bayes' rule and LOTP, The continuous versions are analogous to the discrete versions, with probability density functions in place of probabilities and integrals in place of sums.

---
**Theorem.** (Continuous form of Bayes' rule and LOTP). For continuous random variables $X$ and $Y$, we have the following continuous form of Bayes' rule:

$$
f_{Y|X}(y|x) = \frac{f_{X|Y}(x|y)f_Y(y)}{f_X(x)}, \quad \text{ for } f_X(x) > 0
$$

And we have the following continuous form of the law of total probability:

$$
f_X(x) = \int_{-\infty}^{\infty} f_{X|Y}(x|y) f_Y(y) dy
$$

---

*Proof*.

By the definition of conditional density functions, we have:

$$
f_{Y|X}(y|x) f_X(x) = f_{X,Y}(x,y) = f_{X|Y}(x|y) f_Y(y)
$$

The continuous version of Bayes' rule follows immediately from dividing by $f_X(x)$. The continuous version of LOTP follows immediately from integrating with respect to $y$: 

$$
f_X(x) = \int_{-\infty}^{\infty} f_{X,Y}(x,y)dy = \int_{\infty}^{\infty}f_{X|Y}(x|y)f_Y(y)dy
$$

We now have the versions of the Bayes' rule and LOTP for two discrete random variables and for two continuous random variables. Better yet, there are also versions when we have one discrete random variable and one continuous random variable. After understanding the discrete versions, it is easy to remember and use the other versions since they are analogous, replacing probabilities by density functions. 

---
**Definition.** (Independence of continuous random variables). Random variables $X$ and $Y$ are independent if for all $x$ and $y$,

$$
F_{X,Y}(x,y) = F_X(x) \cdot F_Y(y)
$$

