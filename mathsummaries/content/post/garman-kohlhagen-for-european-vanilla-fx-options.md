---
title: "Garman Kohlhagen for European Vanilla FX Options"
date: 2023-11-19T08:47:10+01:00
math: katex
tags: ["vanilla-option","european-option","fx-option"]
categories: ["FX Derivatives"]
---

## FX Options.

Let $R(t)$ be an exchange-rate such as EURUSD. Suppose it has the dynamics:

$$dR(t)=\mu R(t) dt + \sigma R(t) dW^{\mathbb{P}}(t)\tag{1}$$

Suppose we have a foreign money market account $M^{f}(t)$. The value of the foreign money market account in domestic currency is $M^{f}(t)R(t)$, where $R(t)$ is the exchange rate. 

Consider the discounted value of the foreign money market account (in domestic currency). We have:

$$
\begin{align*}
d(M^{f}(t)R(t)D(t)) &= d(M^f(t))R(t)D(t) + M^{f}(t) d(R(t)D(t))  \\\\
&= r_{FOR}M^{f}(t)R(t)D(t)dt + M^{f}(t)(dR(t)D(t) + R(t)dD(t))\\\\
&= r_{FOR}M^{f}(t)R(t)D(t)dt +  M^{f}(t)R(t)D(t)((\mu dt + \sigma dW_t^{\mathbb{P}}) - r_{DOM}(t)dt)\\\\
&= M^{f}(t)R(t)D(t)(\mu + r_{FOR}- r_{DOM})dt + \sigma dW^{\mathbb{P}}(t)) \tag{2}
\end{align*}
$$

We know that the discounted price of any asset is a martingale under the domestic money market account measure $\mathbb{Q}^d$. Thus, let $\theta = \frac{\mu + r_{FOR}- r_{DOM}}{\sigma}$.

We are interested to write:

$$
\begin{align*}
d(M^{f}(t)R(t)D(t)) &= M^{f}(t)R(t)D(t)(\sigma dW^{\mathbb{Q}^d}(t)) \tag{3}
\end{align*}
$$

Thus, we define the radon-nikodym derivative as:

$$Z := \frac{d\mathbb{Q}^d}{d\mathbb{P}} = \exp\left[-\theta W^{\mathbb{P}}(T) - \frac{\theta^2}{2}T\right]\tag{4}$$

$$dW^{\mathbb{Q}^d}(t) = \theta dt + dW^{\mathbb{P}^d}(t)\tag{5}$$

Then, by the Girsanov theorem, $W^{\mathbb{Q}^d}(t)$ is a standard brownian motion and $M^{f}(t)R(t)D(t)$ is a martingale.

### Drift of the exchange rate process $R(t)$ under $\mathbb{Q}^d$.


By Ito's formula, it follows that:

$$
\begin{align*}
d(M^{f}(t)R(t)) &= d(M^f(t)R(t)D(t))M(t) + M^{f}(t)R(t)D(t)dM(t)  \\\\
&= M^{f}(t)R(t)D(t)(\sigma dW^{\mathbb{Q}^d}(t)) M(t) + M^{f}(t)R(t)D(t)r_{DOM}M(t)dt \\\\
&= M^{f}(t)R(t)(r_{DOM}dt + dW^{\mathbb{Q}^d}(t))
\end{align*}
$$

Intuitively, this is what we'd expect, the mean rate of growth of every asset (which is denominated in the same currency as $M(t)$ is the domestic risk-free rate. However, the drift of the exchange rate process is:

$$
\begin{align*}
d(R(t)) &= d(M^f(t)R(t))D^{f}(t) + M^{f}(t)R(t)dD^{f}(t)  \\\\
&= M^{f}(t)R(t)(r_{DOM}dt + \sigma dW^{\mathbb{Q}^d}(t))D^{f}(t) - M^{f}(t)R(t)r_{FOR}(t)D^{f}(t)dt\\\\
&= M^{f}(t)R(t)D^{f}(t)((r_{DOM} - r_{FOR})dt + \sigma dW^{\mathbb{Q}^d}(t))\\\\
&= R(t)((r_{DOM} - r_{FOR})dt + \sigma dW^{\mathbb{Q}^d}(t))
\end{align*}
$$

The solution to the above SDE is:

$$R(t) = R(0)\exp\left[\left(r_{DOM} - r_{FOR}-\frac{\sigma^2}{2}\right)t + \sigma W^{\mathbb{Q}^d}(t)\right] \tag{6}$$

### Drift of the exchange rate process $1/R(t)$ under $\mathbb{Q}^f$.

From a foreign perspective, the exchange rate is USDEUR or $1/R(t)$. Intuitively, we expect the mean rate of growth of $1/R(t)$ under the foreign risk-neutral measure to be $r_{FOR} - r_{DOM}$. This indeed turns out to be the case.

Consider the domestic money market account $M(t)$. Its value in the foreign currency expressed in terms of shares of the foreign money market account $M^f(t)$ is $\frac{M(t)}{R(t)}D^{f}(t)$. This must be a martingale under the foreign-risk neutral measure $\mathbb{Q}^f$. We have:

$$
\begin{align*}
d\left(\frac{1}{R(t)}\right) &= -\frac{1}{R^2(t)}dR(t) + \frac{1}{2}\cdot \frac{2}{R^3(t)}dR(t)\cdot dR(t)\\\\
&= -\frac{1}{R(t)}\left[\mu dt + \sigma dW^{\mathbb{P}}(t)\right] + \frac{1}{R(t)}\sigma^2 dt\\\\
&= \frac{1}{R(t)}((\sigma^2 - \mu) dt - \sigma dW^{\mathbb{P}}(t)) 
\end{align*}
$$

So, we may write:

$$
\begin{align*}
d\left(\frac{M(t)}{R(t)}\right) &= M(t)d\left(\frac{1}{R(t)}\right) + dM(t)\frac{1}{R(t)}\\\\
&= \frac{M(t)}{R(t)}((\sigma^2 - \mu) dt - \sigma dW^{\mathbb{P}}(t)) + \frac{M(t)}{R(t)}r_{DOM}dt\\\\
&= \frac{M(t)}{R(t)}((r_{DOM} - \mu + \sigma^2) dt - \sigma dW^{\mathbb{P}}(t))
\end{align*}
$$

And

$$
\begin{align*}
d\left(\frac{M(t)D^{f}(t)}{R(t)}\right) &= d\left(\frac{M(t)}{R(t)}\right)D^{f}(t) + dD^{f}(t)\frac{M(t)}{R(t)}\\\\
&=\frac{M(t)}{R(t)}D^{f}(t)((r_{DOM} - \mu + \sigma^2) dt - \sigma dW^{\mathbb{P}}(t))-r_{FOR} D^{f}(t)\frac{M(t)}{R(t)}dt\\\\
&=\frac{M(t)}{R(t)}D^{f}(t)((r_{DOM} -r_{FOR} - \mu + \sigma^2)dt - \sigma dW^{\mathbb{P}}(t))
\end{align*}
$$

Let $\nu = -\frac{(r_{DOM} -r_{FOR} - \mu + \sigma^2)}{\sigma}$ and define the Radon-Nikodym derivative as:

$$
\begin{align*}
dW^{\mathbb{Q}^f}(t) &= \nu dt +  dW^{\mathbb{P}}(t)\\\\
Y_T &:= \frac{d\mathbb{Q}^f}{d\mathbb{P}} = \exp\left[-\nu W^{\mathbb{P}}(T) - \frac{1}{2}\nu^2 T\right] \tag{7}
\end{align*}
$$

By the Girsanov theorem, $W^{\mathbb{Q}^f}(t)$ is a standard brownian motion under the foreign risk-neutral measure $\mathbb{Q}^f$. We may write:

$$d\left(\frac{M(t)D^{f}(t)}{R(t)}\right) = -\frac{M(t)D^{f}(t)}{R(t)}\sigma dW^{\mathbb{Q}^f}(t)$$

Using Ito Calculus, we have:

$$
\begin{align*}
d\left(\frac{M(t)}{R(t)}\right) &= d\left(\frac{M(t)D^{f}(t)}{R(t)}\right) M^{f}(t) + \frac{M(t)D^{f}(t)}{R(t)}dM^{f}(t) \\\\
&= -\frac{M(t)}{R(t)}\sigma dW^{\mathbb{Q}^f}(t) + \frac{M(t)}{R(t)}r_{FOR}dt
\end{align*}
$$

and

$$
\begin{align*}
d\left(\frac{1}{R(t)}\right) &= \frac{1}{R(t)}((r_{FOR}-r_{DOM})dt - \sigma dW^{\mathbb{Q}^f}(t))
\end{align*}
$$

The solution to this SDE is:

$$\frac{1}{R(t)} = \frac{1}{R(0)}\exp \left[(r_{FOR}-r_{DOM} - \frac{\sigma^2}{2})t - \sigma W^{\mathbb{Q}^f}(t)\right]$$

The flipped rate is:

$$R(t) = R(0) \exp \left[(r_{DOM}-r_{FOR} + \frac{\sigma^2}{2})t + \sigma W^{\mathbb{Q}^f}(t)\right] \tag{8}$$

which satisfies 

$$dR(t) = (r_{DOM} - r_{FOR} + \sigma^2)dt + \sigma dW^{\mathbb{Q}^f}(t)\tag{9}$$

## Valuation of European Options

Consider a European call option with the payout function $v_T = \max{R_T - K,0}=(R_T - K)^{+}$. By the risk-neutral pricing formula, we have:

$$
\begin{align*}
V_0 &= e^{-r_{DOM}T}\mathbb{E}^{\mathbb{Q}^d}[(R_T - K)^{+}]\\\\
&= e^{-r_{DOM}T}\mathbb{E}^{\mathbb{Q}^d}[(R_T - K)1_{R_T > K}]\\\\
&= e^{-r_{DOM}T} \mathbb{E}^{\mathbb{Q}^d}[R_T 1_{R_T > K}] - e^{-r_{DOM}T}\mathbb{E}^{\mathbb{Q}^d}[K \cdot 1_{R_T > K}]\\\\
&= e^{-r_{DOM}T} \mathbb{E}^{\mathbb{Q}^d}[R_T 1_{R_T > K}] - Ke^{-r_{DOM}T}\mathbb{E}^{\mathbb{Q}^d}[1_{R_T > K}]\\\\
&= e^{-r_{DOM}T} \mathbb{E}^{\mathbb{Q}^d}[R_T 1_{R_T > K}] - Ke^{-r_{DOM}T}{\mathbb{Q}^d}[{R_T > K}] \tag{10}
\end{align*}
$$

Computation of $\mathbb{Q}^d[R_T \geq K]$, that is the domestic risk-neutral probability that $R_T \geq K$ is relatively trivial as we know the distributution of $R_T$. The other component requires a Radon-Nikodym change of measure argument, which in FX has a nice symmetry to it.

$$
\frac{d\mathbb{Q}^f}{d\mathbb{Q}^d} = \exp\left[-(\nu - \theta)W^{\mathbb{Q}^d}(T) - \frac{1}{2}(\nu - \theta)^2 T\right]\tag{11}
$$

$$
\begin{align*}
W^{\mathbb{Q}^f} &= (\nu-\theta)T + W^{\mathbb{Q}^d} \tag{12}
\end{align*}
$$

But, the drift $\nu - \theta = -\sigma$, so the above expressions become:

$$
\frac{d\mathbb{Q}^f}{d\mathbb{Q}^d} = \exp\left[\sigma W^{\mathbb{Q}^d}(T) - \frac{1}{2}\sigma^2 T\right]\tag{13}
$$

$$
W^{\mathbb{Q}^f} = -\sigma T + W^{\mathbb{Q}^d} \tag{14}
$$

We can now use (13) or (14) to complete (10). Consider $\mathbb{E}^{\mathbb{Q}^d}[R_T 1_{R_T \geq K}]$. We have:

$$
\begin{align*}
\mathbb{E}^{\mathbb{Q}^d}[R_T \cdot 1_{R_T \geq K}] &= \mathbb{E}^{\mathbb{Q}^d}\left[R(0)\exp\left\\{\left(r_{DOM} - r_{FOR}-\frac{\sigma^2}{2}\right)T + \sigma W^{\mathbb{Q}^d}(T)\right\\}\cdot 1_{R_T \geq K}\right]\\\\
&=  R(0)e^{(r_{DOM} - r_{FOR})T}\mathbb{E}^{\mathbb{Q}^d}\left[\exp\left\\{-\frac{\sigma^2}{2}T + \sigma W^{\mathbb{Q}^d}(T)\right\\}\cdot 1_{R_T \geq K}\right]\\\\
&=  R(0)e^{(r_{DOM} - r_{FOR})T}\mathbb{E}^{\mathbb{Q}^d}\left[\frac{d\mathbb{Q}^f}{d\mathbb{Q}^d}\cdot 1_{R_T \geq K}\right]\\\\
&=  R(0)e^{(r_{DOM} - r_{FOR})T}\mathbb{E}^{\mathbb{Q}^f}[1_{R_T \geq K}]\\\\
&=  R(0)e^{(r_{DOM} - r_{FOR})T}{\mathbb{Q}^f}[{R_T \geq K}] \tag{15}
\end{align*}
$$

We therefore have:

$$
V_0 = R(0)e^{-r_{FOR}T} \mathbb{Q}^f[R_T \geq K] - Ke^{-r_{DOM}T}\mathbb{Q}^d[R_T \geq K] \tag{16}
$$

### Calculating the two risk-neutral probabilities $\mathbb{Q}^f[R_T \geq K]$ and $\mathbb{Q}^d[R_T \geq K]$

We now need to calculate the two risk-neutral probabilities (in $\mathbb{Q}^d$ and $\mathbb{Q}^f$) that $S_T \geq K$. We have: 

$$R(t) = R(0)\exp\left[\left(r_{DOM} - r_{FOR}-\frac{\sigma^2}{2}\right)t + \sigma W^{\mathbb{Q}^d}(t)\right] \tag{17a}$$

$$R(t) = R(0) \exp \left[(r_{DOM}-r_{FOR} + \frac{\sigma^2}{2})t + \sigma W^{\mathbb{Q}^f}(t)\right] \tag{17b}$$

We can unify the notation by introducing the index $i$ which takes the values in $\{1,2\}$ and $X(\cdot)$ defined such that $X(1) \equiv f$ and $X(2) \equiv d$. We write:

$$R_T = R_0 \exp \left (\sigma W_T^{\mathbb{Q}^{X(i)}} + \left(r_{DOM} - r_{FOR} - \left[\frac{1}{2}-(i-1)\right]\sigma^2 \right) T\right ) \tag{18}$$

We can easily compute $\mathbb{Q}^{X_i}[R_T \geq K]$ now for the foreign and domestic risk-neutral measures. We have:

$$
\begin{align*}
&\mathbb{Q}^{X(i)}\left[R_0\exp \left(\sigma W_T^{\mathbb{Q}^{X(i)}}+\left(r_{DOM} - r_{FOR} + \left[\frac{1}{2}-(i-1)\right]\sigma^2\right)T\right) \geq K\right] \\\\
=& \mathbb{Q}^{X(i)}\left[\exp \left(\sigma W_T^{\mathbb{Q}^{X(i)}}+\left(r_{DOM} - r_{FOR} + \left[\frac{1}{2}-(i-1)\right]\sigma^2\right)T\right) \geq \frac{K}{R_0}\right] \\\\
=& \mathbb{Q}^{X(i)}\left[\left(\sigma W_T^{\mathbb{Q}^{X(i)}}+\left(r_{DOM} - r_{FOR} + \left[\frac{1}{2}-(i-1)\right]\sigma^2\right)T\right) \geq \log \frac{K}{R_0}\right] \\\\
=& \mathbb{Q}^{X(i)}\left[\left(\sigma W_T^{\mathbb{Q}^{X(i)}}\right) \geq \log \frac{K}{R_0}-\left(r_{DOM} - r_{FOR} + \left[\frac{1}{2}-(i-1)\right]\sigma^2\right)T\right] \\\\
=& \mathbb{Q}^{X(i)}\left[\left(-\sigma W_T^{\mathbb{Q}^{X(i)}}\right) \leq \log \frac{R_0}{K}+\left(r_{DOM} - r_{FOR} + \left[\frac{1}{2}-(i-1)\right]\sigma^2\right)T\right] \\\\
=& \mathbb{Q}^{X(i)}\left[\left(\sigma \sqrt{T} Z\right) \leq \log \frac{R_0}{K}+\left(r_{DOM} - r_{FOR} + \left[\frac{1}{2}-(i-1)\right]\sigma^2\right)T\right] \\\\
=& \mathbb{Q}^{X(i)}\left[Z \leq \frac{\log \frac{R_0}{K}+\left(r_{DOM} - r_{FOR} + \left[\frac{1}{2}-(i-1)\right]\sigma^2\right)T}{\sigma \sqrt{T} }\right] 
\end{align*}
$$

where $Z\sim\mathcal N^{\mathbb{Q}^{X(i)}}(0,1)$ normal distribution, noting that $W^{\mathbb{Q}^{X(i)}}$, $-W^{\mathbb{Q}^{X(i)}}$, $\sqrt{T}Z$ and $-\sqrt{T}Z$ all have the same distribution by symmetry.

We therefore put,

$$d_{\pm}(t,x) = \frac{\log \frac{x}{K} + \left(r \pm \frac{\sigma^2}{2}\right)T}{\sigma \sqrt{T}}$$

and we get:

$$V_0^C = R_0 e^{-r_{FOR}T} \Phi(d_{+}(T,R_0)) - Ke^{-r_{DOM}T} \Phi(d_{-}(T,R_0))$$

The same argument applies for the European put option, with the payout function $V_T = \max(K - R_T,0)$ at time $T$, for which we obtain:

$$V_0^P = Ke^{-r_{DOM}T} \Phi(-d_{-}(T,R_0)) - R_0 e^{-r_{FOR}T} \Phi(-d_{+}(T,R_0))$$

For clarity, we use a more unified notation - introduce the variable $\omega$ which is $+1$ for a call and a $-1$ for a put. We obtain:

$$V^{C/P} = \omega R_0 e^{-r_{FOR}T} \Phi(\omega d_{+}(T,R_0)) - Ke^{-r_{DOM}T} \Phi(\omega d_{-}(T,R_0))$$


