---
title: "Price of a Power Call Option"
date: 2024-01-21T16:33:58+01:00
math: katex
tags: ["vanilla-option","european-option","fx-option"]
categories: ["Radon-Nikodym"]
---
# Price of European option with payoff $V(T)=\max (S^2(T) - K,0)$

## Deriving the dynamics of $X(t) = S^2(t)$.

In the Black-Scholes world, the stock price $S(t)$ has $\mathbb{Q}$-dynamics:

$$
dS\_t = rS(t)dt + \sigma S(t) dW^{\mathbb{Q}}(t) \tag{1}
$$

Let $X(t) = S^2(t)$. The square of the stock price has the $\mathbb{Q}$-dyamics:

$$
\begin{align*}
dX\_t &= 2S(t)dS(t) + \frac{1}{2}\cdot 2 \cdot dS\_t \cdot dS\_t\\\\
&= 2S(t) ( rS(t)dt + \sigma S(t) dW^{\mathbb{Q}}(t)) + \sigma^2 S^2(t) dt \\\\
&= S^2(t)[(2r + \sigma^2)dt + 2\sigma dW^{\mathbb{Q}}(t)]\\\\
&= X(t)[(2r + \sigma^2)dt + 2\sigma dW^{\mathbb{Q}}(t)]
\end{align*}
$$

Let $f(x) = \log x$. By Ito's formula:

$$
\begin{align*}
d(\log X\_t) &= \frac{1}{X(t)}dX(t) + \frac{1}{2}\cdot \left(-\frac{1}{X^2(t)}\right)dX(t)\cdot dX(t)\\\\
 &= (2r + \sigma^2)dt + 2\sigma dW^{\mathbb{Q}}(t) - \frac{1}{2}\cdot 4\sigma^2 dt\\\\
 &= (2r - \sigma^2)dt + 2\sigma dW^{\mathbb{Q}}(t) \\\\
 X(t) &= X(0) \exp[(2r - \sigma^2)t + 2\sigma W^{\mathbb{Q}}(t)] \tag{2}
\end{align*}
$$

## Computing the expectations.

By the risk neutral pricing formula, the price of the claim $V(T) = \max(S^2(T) - K,0)$ at time $t$ is:

$$
\begin{align*}
V(t,T) &= \mathbb{E}^{\mathbb{Q}}[e^{-r(T-t)}(S^2(T) - K)\cdot 1\_{S^2(T) > K}|\mathcal{F}\_t] \\\\
&= e^{-r(T-t)}\mathbb{E}^{\mathbb{Q}}[S^2(T) 1\_{S^2(T) > K}|\mathcal{F}\_t] - Ke^{-r(T-t)}\mathbb{E}^{\mathbb{Q}}[1\_{S^2(T) > K}|\mathcal{F}\_t]
\end{align*}\tag{3}
$$

### Computing $\mathbb{E}^{\mathbb{Q}}[1\_{S(T) > K}|\mathcal{F}\_t]$.

Define :

$$
\begin{align*}
\tau &:= T - t\\\\
d\_{1}(\tau,x) &= \frac{\log\frac{x}{\sqrt{K}} + \left(r + \frac{3}{2}\sigma^2\right)\tau}{\sigma \sqrt{\tau}}\\\\
d\_{2}(\tau,x) &= \frac{\log\frac{x}{\sqrt{K}} + \left(r - \frac{\sigma^2}{2}\right)\tau}{\sigma \sqrt{\tau}}
\end{align*}
$$

The second expectation $\mathbb{E}^{\mathbb{Q}}[1\_{S(T) > K}|\mathcal{F}\_t]$ is computed in the standard way.

$$
\begin{align*}
\mathbb{E}^{\mathbb{Q}}[1\_{S^2(T) > K}|\mathcal{F}\_t] &= \mathbb{Q}(S^2(T) > K|\mathcal{F\_t})\\\\
&=\mathbb{Q}\left(\log S^2(T) > \log K|\mathcal{F\_t}\right)\\\\
&=\mathbb{Q}\left(\log S^2(t) + (2r - \sigma^2)\tau + 2\sigma \sqrt{\tau} Z > \log K|\mathcal{F\_t}\right)\\\\
&=\mathbb{Q}\left( 2\sigma \sqrt{\tau} Z > \log K - \log S^2(t) - 2(r - \sigma^2/2)\tau|\mathcal{F\_t}\right)\\\\
&=\mathbb{Q}\left(Z > \frac{\log K - \log S^2(t) - 2(r - \sigma^2/2)\tau}{2\sigma \sqrt{\tau}}|\mathcal{F\_t}\right)\\\\
&=\mathbb{Q}\left(Z < \frac{\log S^2(t) - \log K + 2(r - \sigma^2/2)\tau}{2\sigma \sqrt{\tau}}|\mathcal{F\_t}\right)\\\\
&=\mathbb{Q}\left(Z < \frac{\log \frac{S^2(t)}{K} + 2(r - \sigma^2/2)\tau}{2\sigma \sqrt{\tau}}|\mathcal{F\_t}\right)\\\\
&=\mathbb{Q}\left(Z < \frac{\log \frac{S(t)}{\sqrt{K}} + (r - \sigma^2/2)\tau}{\sigma \sqrt{\tau}}|\mathcal{F\_t}\right)\\\\
&=\Phi(d\_{2}(\tau,S(t)))
\end{align*} \tag{4}
$$

### Computing $\mathbb{E}^{\mathbb{Q}}[S^2(T) 1\_{S^2(T) > K}|\mathcal{F}\_t]$.

Let $\tilde{\mathbb{Q}}$ be another probability measure related to $\mathbb{Q}$ defined by the Radon-Nikodym derivative:

$$
\begin{align*}
\frac{d\tilde{\mathbb{Q}}}{d\mathbb{Q}} &= \frac{N(T)/B(T)}{N(0)/B(0)} \\\\
&= \frac{S^2(T)/e^{rT}}{S^2(0)/1}\\\\
&= \exp\left[(r-\sigma^2)T + 2\sigma W^{\mathbb{Q}(T)}\right]\\\\
&= \exp\left[2\sigma W^{\mathbb{Q}(T)}-\frac{1}{2}4\sigma^2 T\right]\exp\left[rT + \sigma^2 T\right]
\end{align*}
$$

Using Girsanov's theorem, we can express $W^{\tilde{\mathbb{Q}}}(t) = W^{\mathbb{Q}}(t) - 2\sigma t$ and the constant expression $\exp\left[rT + \sigma^2 T\right]$ is taken care of at the end, after we have found a suitable CDF.

By the change of measure theorem, the first expectation can be expressed as follows:

$$
\begin{align*}
\mathbb{E}^{\tilde{\mathbb{Q}}}[1\_{S^2(T)>K}|\mathcal{F}\_t] &= \mathbb{E}^{\mathbb{Q}}\left[\frac{(d\tilde{\mathbb{Q}}/d\mathbb{Q})\_T}
{(d\tilde{\mathbb{Q}}/d\mathbb{Q})\_t}1\_{S^2(T)>K}|\mathcal{F}\_t\right]\\\\
\mathbb{E}^{\tilde{\mathbb{Q}}}[1\_{S^2(T)>K}|\mathcal{F}\_t] &= \mathbb{E}^{\mathbb{Q}}\left[\frac{S^2(T)e^{-rT}}
{S^2(t)e^{-rt}}1\_{S^2(T)>K}|\mathcal{F}\_t\right]\\\\
S^2(t)\mathbb{E}^{\tilde{\mathbb{Q}}}[1\_{S^2(T)>K}|\mathcal{F}\_t] &= \mathbb{E}^{\mathbb{Q}}\left[S^2(T)e^{-r(T-t)}
1\_{S^2(T)>K}|\mathcal{F}\_t\right] \tag{5}
\end{align*}
$$

### Computing $\mathbb{E}^{\tilde{\mathbb{Q}}}[1\_{S^2(T)>K}|\mathcal{F}\_t]$.

We can now solve for $\tilde{\mathbb{Q}}(S^2(T) > K)$ as:

$$
\begin{align*}
\mathbb{E}^{\tilde{\mathbb{Q}}}[1\_{S^2(T)>K}|\mathcal{F}\_t] &= \tilde{\mathbb{Q}}\left(S^2(T) > K\right)\\\\
&=\tilde{\mathbb{Q}}\left(\log S^2(T) > \log K\right)\\\\
&=\tilde{\mathbb{Q}}\left(\log S^2(t) + (2r - \sigma^2)\tau + 2\sigma W^{\mathbb{Q}}(\tau) > \log K\right)\\\\
&=\tilde{\mathbb{Q}}\left(\log S^2(t) + (2r - \sigma^2)\tau + 2\sigma (W^{\tilde{\mathbb{Q}}}(\tau) + 2\sigma \tau) > \log K\right)\\\\
&=\tilde{\mathbb{Q}}\left(\log S^2(t) + (2r + 3\sigma^2)\tau + 2\sigma W^{\tilde{\mathbb{Q}}}(\tau) > \log K\right)\\\\
&=\tilde{\mathbb{Q}}\left(2\sigma W^{\tilde{\mathbb{Q}}}(\tau) > \log K - \log S^2(t) - (2r + 3\sigma^2)\tau \right)\\\\
&=\tilde{\mathbb{Q}}\left(W^{\tilde{\mathbb{Q}}}(1) > \frac{\log \sqrt{K} - \log S(t) - (r + \frac{3}{2}\sigma^2)\tau}{\sigma\sqrt{\tau}}\right)\\\\
&=\tilde{\mathbb{Q}}\left(W^{\tilde{\mathbb{Q}}}(1) < \frac{\log \frac{S(t)}{\sqrt{K}} + (r + \frac{3}{2}\sigma^2)\tau}{\sigma\sqrt{\tau}}\right)\\\\
&=\Phi(d\_1(\tau,S(t))
\end{align*}
$$

## Conclusion.

The price of the European power call option having payoff $V(T)=\max (S^\alpha(T) - K,0)$, where $\alpha = 2$ is:

$$
V(t,T) = S^2(t)\Phi(d\_1(\tau,S(t))) - Ke^{-r(T-t)}\Phi(d\_2(\tau,S(t)))
$$
