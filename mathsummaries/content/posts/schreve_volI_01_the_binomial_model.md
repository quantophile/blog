---
title: The Binomial Model
math: true
tags: ["binomial-model", "no-arbitrage", "martingale"]
categories: ["Stochastic Calculus"]
date: 2022-01-19T13:01:03+01:00
---


## Model Description.

Running time is denoted by the letter $t$, and by definition we have two points in time, $t=0$ and $t=1$. In the model, we have two assets: a **bond** and a **stock**. At time $t$, the bond is denoted by $B_t$ and the price of one share of stock is denoted by $S_t$. Thus, we have two price processes $B$ and $S$.

The bond price process is deterministic and given by,

$$
\begin{align\*}
    B_0 &= 1\\\\
    B_1 &= B_0(1+r)
\end{align\*}
$$

The constant $r$ is the spot rate for the period, we can also interpret the existence of the bond as the existence of a bank with $r$ as its rate of interest. The stock price process is a stochastic process, and its dynamical behavior can be described as follows:

$$
\begin{align\*}
    S_0 &= s \\\\
    S_1 &= \begin{cases}
    s \cdot u, \quad \text{ with probability } p_u \\\\
    s \cdot d, \quad \text{ with probability } p_d
    \end{cases}
\end{align\*}
$$

It is often convenient to write this as,

$$
\begin{align\*}
    \begin{cases}
    S_0 &= s \\\\
    S_1 &= s \cdot Z
    \end{cases}
\end{align\*}
$$

where $Z$ is a stochastic variable defined as

$$
\begin{align\*}
    Z &= \begin{cases}
    u, \text{ with probability } p_u\\\\
    d, \text{ with probability } p_d
    \end{cases}
\end{align\*}
$$

![one_period_binomial.png](attachment:one_period_binomial.png)

We assume that today's stock price $s$ is known, as are the positive constants, $u$, $d$, $p_u$ and $p_d$. We assume that $d < u$ and we have of course $p_u + p_d = 1$. We can illustrate the price dynamics using the tree structure in the above figure.

## Portfolios and arbitrage.

We will study the behavior of various portfolios on the $(B,S)$ market and to this end we define a portfolio as a vector $\mathbf{h} = (x,y)$ in $\mathbf{R}^2$. The interpretation is that $x$ is the number of bonds we hold in our portfolio, whereas $y$ in the number of units of the stock held by us. Note that, it is quite acceptable for $x$ and $y$ to be positive as well as negative. If, for example, $x=3$, this means that we have bought three bonds at time $t=0$. If on the other hand $y=-2$, this means that we have sold two share of the stock at time $t=0$. In financial jargon, we have a \textbf{long} position in the bond and a \textbf{short} position in the stock. It is an important assumption of the model, that \textbf{short} positions are allowed.

---
**Assumptions**. We assume the following institutional facts:

- Short positions as well as fractional holdings are allowed. In mathematical terms, this means that every $\mathbf{h}\in\mathbf{R}^2$ is an allowed portfolio.
- There is no bid-ask spread. That is, the selling price is equal to the buying price.
- There are no transactions costs of trading.
- The market is completely liquid i.e. it is always possible to buy and/or sell unlimited quantities on the market. In particular, it is possible to borrow unlimited amounts from the bank (by selling bonds short).


---

Consider now a fixed portfolio $\mathbf{h} =(x,y)$. This portfolio has a deterministic market value at $t=0$ and a stochastic value at $t=1$.

---

**Definition (Value process $V_t^h$)**. The **value process** of the portfolio $h$ is defined by

$$
\begin{align\*}
    V_t^h = xB_t + yS_t, \quad t=0,1
\end{align\*}
$$

or in more detail,

$$
\begin{align\*}
    V_0^h &= x + ys \\\\
    V_1^h &= x(1+r) + ysZ
\end{align\*}
$$

---

Everyone wants to make a profit by trading on the market, and in this context a so-called arbitrage-portfolio is a dream come true, this is one of the central concepts of the theory.

---
Arbitrage Portfolio.
An arbitrage portfolio is a portfolio $h$ with the properties,

$$
\begin{align\*}
    V_0^h &= 0,\\\\
    V_1^h &> 0, \text{ with probability }1
\end{align\*}
$$

---

An arbitrage portfolio is a deterministic money-making machine, and we interpret the existence of an arbitrage portfolio as equivalent to a serious case of mispricing on the market. It is now natural to investigate when a given market model is arbitrage free i.e. when there are no arbitrage opportunities.

---
**Proposition**. The model above is arbitrage-free if and only if the following conditions hold:
$$
 \begin{align\*}
     d \leq (1 + r) \leq u \tag{1}
 \end{align\*}
$$

---

*Proof*. The above condition has an easy economic interpretation. It simply says that the return on the stock is not allowed to dominate the bond and vice versa. To show that, absence of arbitrage implies equation (\ref{eq:arb_free}), we assume that (\ref{eq:arb_free}) does in fact not hold, and then we show that this implies an arbitrage opportunity. Let us assume that the inequalities in (\ref{eq:arb_free}) does not hold, so that we have the inequality $s(1+r)>su$. Then, we also have $s(1+r)>sd$, so it always more profitable to invest in the bond than in the stock. An arbitrage strategy can now be formed by the portfolio $h=(s,-1)$. For this portfolio, we therefore have, $V_0^h = s + (-1)(s) = 0$, and as for $t=1$, we have :

$$
\begin{align\*}
    V_1^h = s(1+r) - sZ
\end{align\*}
$$

which by the assumption is positive. 

Now assume that (\ref{eq:arb_free}) is satisfied. To show that this implies absence of arbitrage, let us consider an arbitrary portfolio such that $V_0^h = 0$. We thus have $x + ys = 0$ i.e. $x = -ys$. Using this relation, we can write the value of the portfolio at $t=1$ as 

$$
\begin{align\*}
    V_1^h &= \begin{cases}
    -ys(1+r) + ysu & \text{ if } Z=u\\\\
    -ys(1+r) + ysd & \text{ if } Z=d\\\\
    \end{cases} 
\end{align\*}
$$

That is,
$$
\begin{align\*}
    V_1^h &= \begin{cases}
    ys(u-(1+r)) & \text{ if } Z=u\\\\
    ys(d-(1+r)) & \text{ if } Z=d\\\\
    \end{cases} 
\end{align\*}
$$

Assume now that $y>0$. Then, $h$ is an arbitrage strategy, if and only, if we have the inequalities:

$$
\begin{align\*}
    u &> (1+r)\\\\
    d &> (1+r)
\end{align\*}
$$

but this is impossible because of condition (\ref{eq:arb_free}). The case $y < 0$ is treated similarly. This closes the proof.

At first glance, this result is perhaps only moderately exciting, but we may write it in a more suggestive form. To say that \eqref{eq:arb_free} holds is equivalent to saying that, geometrically, the point $(1+r)$ lies between the points $u$ and $d$ on the real line, and therefore it is a convex combination of $u$ and $d$. By the section formula,

$$
\begin{align\*}
    1+r = q_u \cdot u + q_d \cdot d
\end{align\*}
$$

where $q_u,q_d \geq 0$ are some fractions and $q_u + q_d = 1$. The point $(1+r)$ divides the line joining $(u,0)$ and $(d,0)$, into the ratio $q_d:q_u$. In particular, we see that these weights $q_u$ and $q_d$ can be interpreted as probabilities for a new probability measure $Q$ with the probability with the property $Q(Z=u)=q_u$ and $Q(Z=d) = q_d$. Denoting the expectation w.r.t this measure by $E^Q$, we have the following easy calculation:

$$
\begin{align\*}
    \frac{1}{1+r}E^Q[S_1] = \frac{1}{1+r}[q_u su + q_d sd] = \frac{1}{1+r} \cdot s(1+r) = s
\end{align\*}
$$

We thus have the relation
$$
\begin{align\*}
    s = \frac{1}{1+r}E^Q[S_1]
\end{align\*}
$$

This is called the **risk-neutral pricing formula**, in the sense that, it gives today's stock price as the discounted expected value of tomorrow's stock price. Of course, we do not assume that the agents in our market are risk-neutral - what we have shown is only that if we use $Q$-probabilities then we in fact have a risk-neutral valuation of the stock(given absence of arbitrage). A probability measure is called a **risk-neutral measure**, or alternatively a **risk adjusted measure** or a **martingale measure**.

---
**Definition (Martingale Measure)**. A probability measure $Q$ is called a martingale measure if the following condition holds:
$$
\begin{align\*}
    S_0 = \frac{1}{1+r}E^Q[S_1]
\end{align\*}
$$

---

---
**Proposition (Equivalence of No-arbitrage and existence of Martingale measure).** The market model is arbitrage free if and only if there exists a martingale measure $Q$.

---

*Proof*.

The binomial model is arbitrage free, if 
$$
\begin{align\*}
    d \leq (1+r) \leq u
\end{align\*}
$$

Let $(1+r) = q_u u + q_d d$. Then, by the section formula, 
$$
\begin{align\*}
    q_u &= \frac{(1+r)-d}{u-d}\\\\
    q_d &= \frac{u - (1+r)}{u-d}
\end{align\*}
$$

Clearly, $0 < q_u < 1$, $0 < q_d < 1$ and $q_u + q_d = 1$. Moreover, they satisfy the equation $q_u \cdot u + q_d \cdot d = (1+r)$. So, the discounted expectation of tomorrow's stock price under the $Q$-measure is today's stock price. Thus, there exists a martingale measure $Q$. This closes the proof.

---
**Proposition (Martingale probabilities in the Binomial Model).**
 For the binomial model above, the martingale probabilities are:
 
 $$
 \begin{align\*}
 q_u &= \frac{(1+r)-d}{u - d}\\\\
 q_d &= \frac{u-(1+r)}{u - d}
 \end{align\*}
 $$
 
---

---
**Defintion (Contingent claim).** A contingent claim(financial derivative) is any stochastic variable $X$ of the form $X = \Phi(Z)$, where $Z$ is the stochastic variable driving the stock price process above.

---

The function $\Phi$ is called the **contract function**. A typical example would be a European call option on the stock with strike price $K$. For this option to be interesting we assume that $sd < K < su$. If $S_1 > K$, then we use the option, pay $K$ to get the stock and then sell the stock on the market for $su$, thus making a net profit of $su - K$. If $S_1 < K$, then the option is obviously worthless. In this example, we thus have:

$$
\begin{align\*}
    X = \begin{cases}
    su - K, \quad &\text{ if } Z=u,\\\\
    0, \quad & \text{ if } Z = d
    \end{cases}
\end{align\*}
$$

and the contract function is given by 

$$
\begin{align\*}
    \Phi(u) &= su - K,\\\\
    \Phi(d) &= 0
\end{align\*}
$$

Our main problem is now to determine the fair price of this financial derivative at time $0$, if such an object exists at all, for a given contingent claim $X$.


![contingent_claim.png](attachment:contingent_claim.png)


If we denote the price of $X$ at time $t$ by $\Pi_t[X]$, then it can be seen that at time $t=1$, the problem is easy to solve. In order to avoid arbitrage, we must have 

$$
\begin{align\*}
    \Pi_1[X] = X
\end{align\*}
$$

If $\Pi_1[X] > X$, everyone would borrow the asset worth $X$ at time $1$ and sell it for a price $\Pi_1[x]$ to make a risk-less profit of $\Pi_X - X$, forcing the price downwards. If $\Pi_1[X] < X$, then everyone would buy the asset worth $X$ at time $1$ for a cheaper price $\Pi_1[X]$ and make a risk-less profit of $X - \Pi_1[X]$, thus pushing the price upwards. Thus, $X = \Pi_1[X]$, if there is to be no arbitrage opportunities.

The hard part of the problem is to now determine $\Pi_0[X]$. To attack this problem, we make a slight detour.

Since, we have assumed the absence of arbitrage we know that we cannot make money out of nothing, but it is interesting to study what we can achieve on the market. 

---
**Definition (Replication portfolio).** A given contingent claim $X$ can be \textbf{replicated}, or is said to be reachable if there if there exists a portfolio $h$ such that 
$$
\begin{align\*}
    V_1^h &= X
\end{align\*}
$$
with probability $1$. In that case, we say that the portfolio $h$ is a \textbf{hedging} portfolio or a \textbf{replicating} portfolio. If all claims can be replicated we say that the market is \textbf{complete}. 

---

If a certain claim $X$ is reachable with the replicating portfolio $h$, then from a financial point of view, there is no difference between holding the claim and holding the portfolio. No matter what happens on the stock market, the value of the claim at time $1$ will be exactly equal to the value of the portfolio at $t=1$. Thus, the price of the claim should equal the market value of the portfolio, and we have the following basic principle.

**Pricing principle 1.** If the claim $X$ is reachable with the replicating portfolio $h$, then the only reasonable price process for $X$ is given by 
$$
\begin{align\*}
    \Pi_t[X] = V_t^h, \quad t=0,1
\end{align\*}
$$

The word "reasonable" above can be given a more precise meaning as in the following proposition. We leave the proof to the reader.

---
**Proposition. Price of a contingent claim $X$** Suppose that the claim $X$ is reachable with the replicating portfolio $h$. Then any price at $t=0$ of the claim $X$, other than $V_0^h$ will lead to an arbitrage possibility.

---

*Proof.*
Case I. $\Pi_0[X] > V_0^h$. Then at time $t=0$, short sell the claim $X$ for $\Pi_0[X]$, invest $V_0^h$ dollars to buy the replicating portfolio and the remaining difference $\Pi_0[X] - V_0^h$ in a risk-free money-market account. At time $t=1$, we can sell the replicating portfolio for $V_1^h = \Pi_1[X]$ dollars and return the claim. We will be left with a risk-less profit of $(\Pi_0[X] - V_0^h)(1+r)$. 

Case II. $\Pi_0[X] < V_0^h$. Then, at time $t=0$, short sell the replicating portfolio for $V_0^h$ dollars, buy the claim $X$ for $\Pi_0[X]$ and invest the remaining sum of money in a risk-free bank account. At time $t=1$, the claim $X$ is worth $\Pi_1[X]$ which is enough to square off our short position on the hedging portfolio worth $V_1^h$, and we are left with a risk-less profit of $(V_0^h - \Pi_0[X])(1+r)$.

We see that in a complete market, we can in fact price all contingent claims, so it is of great interest to investigate when a given market is complete. For the binomial model, we have the following result.

---
**Proposition (Binomial model is complete)**. Assume that the general binomial model is free of arbitrage. Then, it is also complete.

---

*Proof.*

We fix an arbitrary claim $X$ with the contract function $\Phi$, and we want to show that there exists a portfolio $h=(x,y)$ such that

$$
\begin{align\*}
    V_1^h &= \Phi(u), \text{ if } Z=u\\\\
    V_1^h &= \Phi(d), \text{ if } Z=d
\end{align\*}
$$

If we write this out in detail, we want to find a solution $(x,y)$ such that:

$$
\begin{align\*}
    (1+r)x + suy &= \Phi(u)\\\\
    (1+r)x + sdy &= \Phi(d)
\end{align\*}
$$

Solving for $x$ and $y$, we get:

$$
\begin{align\*}
    x &= -\frac{1}{1+r}\cdot\frac{\Phi(u)\cdot d - \Phi(d) \cdot u}{u - d}\\\\
    y &= \frac{\Phi(u) - \Phi(d)}{s(u - d)}
\end{align\*}
$$

## Risk-neutral Valuation

Since the binomial model is shown to be complete we can now price any contingent claim. According to the pricing principle of the preceding section, the time-zero price $\Pi_0[X]$ of the claim $X$ is given by,

$$
\begin{align\*}
    \Pi_0[X] &=  V_0^h
\end{align\*}
$$

and using the explicit formulas \eqref{eq:bonds}-\eqref{eq:stocks}, we obtain:

$$
\begin{align\*}
    \Pi_0[X] &= x + ys \\\\
    &= -\frac{1}{1+r}\cdot \frac{\Phi(u)\cdot d - \Phi(d) \cdot u}{u - d} +  \frac{\Phi(u) - \Phi(d)}{s(u-d)} \cdot s\\\\
    &= -\frac{1}{1+r}\cdot \frac{\Phi(u)\cdot d - \Phi(d) \cdot u}{u - d} +  \frac{1}{1+r}\cdot\frac{(1+r)\Phi(u) - (1+r)\Phi(d)}{(u-d)}\\\\
    &= \frac{1}{1+r}\left[\Phi(u) \left(\frac{(1+r) - d}{u - d}\right) + \Phi(d) \left(\frac{u - (1+r)}{u - d}\right)\right]
\end{align\*}
$$

Here we recognize the martingale probabilities $q_u$ and $q_d$. If we assume that the model is free of arbitrage, these are the true probabilities, so we can write the pricing formula above as

$$
\begin{align\*}
    \Pi_0[X] = \frac{1}{1+r}\{\Phi(u)\cdot q_u + \Phi(d)\cdot q_d\}
\end{align\*}
$$
The right hand side can now be interpreted as an expected value under the martingale probability measure $Q$, so we have proved the following basic pricing result, where we also add our old results about hedging.

---
**Proposition (Arbitrage free price of a contingent claim).** If the binomial model is free of arbitrage, then the arbitrage free price of a contingent claim $X$ is given by,
 $$
 \begin{align\*}
     \Pi_0[X] &= \frac{1}{1+r}E^Q[X]
 \end{align\*}
 $$
 
 Here the martingale measure $Q$ is uniquely determined by the relation
 $$
 \begin{align\*}
     S_0 = \frac{1}{1+r}E^Q[S_1]
 \end{align\*}
 $$
 and the explicit expressions for $q_u$ and $q_d$ are given in the proposition \ref{prop:binomial_probabilities}. Furthermore the claim can be replicated using the portfolio
 
 $$
 \begin{align\*}
     x &= -\frac{1}{1+r}\cdot \frac{d\Phi(u) - u\Phi(d)}{u - d}\\\\
     y &= \frac{\Phi(u) - \Phi(d)}{s(u-d)}
 \end{align\*}
$$

---

We see that the formula \eqref{eq:risk_neutral_valuation_formula} is a "risk-neutral" valuation formula, and that the probabilities which are used are just those for which the stock itself admits a risk-neutral valuation.

---
**Moral:**

- The only role played by the objective probabilities is that they determine which events are possible and which are impossible. In more abstract probabilistic terminology they thus determine the class of equivalent probability measures. 
- When we compute the arbitrage free price of a financial derivative we carry out the computations **as if** we live in a risk neutral world. 
- This does **not** mean that we de facto live (or believe that we live) in a risk-neutral world.
- The formula above holds for all investors, regardless of their attitude towards risk, as long as they prefer more deterministic money to less.
    
---



