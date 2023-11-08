---
title: "The Black-Scholes PDE"
date: 2023-10-29T09:38:36+01:00
math: katex
tags: ["financial-mathematics","black-scholes"]
categories: ["financial-mathematics"]
---

# Deriving the Black-Scholes PDE

## Risk-Free Asset

The price process $(B(t),t\geq 0)$ is the price of a risk-free asset, if it has the dynamics:

$$dB(t) = r(t)B(t)dt$$

The definining property of a risk-free asset is thus, that it has no driving $dW$-term. Using the separation of variables method, we can also write the $B$-dynamics as:

$$\frac{dB(t)}{B(t)} = r(t)dt$$

We can integrate this like an ordinary ODE. 

$$B(t) = B(0)e^{-\int_{0}^{t}r(s)ds}$$

and as notational convention, we put $B(0) = 1$.

The natural interpretation of a risk-free asset is that it corresponds to a bank account with (possibly stochastic) short interest rate $r$. Note that, the bank-account is **locally risk-free**, in the sense that, even if the short rate is a random process, the return $r(t)$ over an infinitesimal time-period $dt$ is risk-free (that is deterministic, given the information available at time $t$). However, the return of $B(t)$ over a **longer interval** such as $[t,T]$ is typically stochastic.



## Derivation of the PDE by a hedging argument

The Black-Scholes model consists of two assets with dynamics given by:

$$
\begin{align}
dB(t) &= r(t)B(t)dt\\
dS(t) &= \mu S(t)dt+ \sigma S(t)dW(t)
\end{align}
$$

We setup a self-financing portfolio $\Pi$ that is comprised of one option and an amount $\Delta(t)$ of the underlying stock. 

Hence, the value of the portfolio at time $t$ is:

$$\Pi(t) = V(t) + \Delta(t)S(t)$$

Since the portfolio is self-financing:

$$d\Pi(t) = dV(t) + \Delta(t)dS(t)$$

The price of the derivative contract at time $t$ is a function of the time $t$, and the position of the underlying $S(t)$. So, $V(t)=f(t,S(t))$. Applying Ito's lemma to $f(t,x)$, we have:

$$
\begin{align*}
df(t,x) &= \frac{\partial V}{\partial t}dt + \frac{\partial V}{\partial x}dS(t) + \frac{1}{2} \frac{\partial^2 V}{\partial x^2}d<S,S>_t \\
&=  \frac{\partial V}{\partial t}dt + \frac{\partial V}{\partial x}(\mu S(t) dt + \sigma S(t)dW(t)) + \frac{1}{2} \frac{\partial^2 V}{\partial x^2}\sigma^2 S_t^2 dt \\
&=  \left(\frac{\partial V}{\partial t} + \mu S(t)\frac{\partial V}{\partial x} + \frac{1}{2} \sigma^2 S_t^2 \frac{\partial^2 V}{\partial x^2}\right)dt + \sigma S(t) \frac{\partial V}{\partial x} dW(t)
\end{align*}
$$

Hence:

$$
\begin{align*}
d\Pi(t) &= \left(\frac{\partial V}{\partial t} + \mu S(t)\frac{\partial V}{\partial x} + \frac{1}{2} \sigma^2 S_t^2 \frac{\partial^2 V}{\partial x^2}\right)dt + \sigma S(t) \frac{\partial V}{\partial x} dW(t) + \Delta(t)(\mu S(t) dt + \sigma S(t) dW(t))\\
&=\left[\frac{\partial V}{\partial t} + \mu S(t)\left(\frac{\partial V}{\partial x} + \Delta(t)\right) + \frac{1}{2} \sigma^2 S_t^2 \frac{\partial^2 V}{\partial x^2}\right]dt + \sigma S(t) \left(\frac{\partial V}{\partial x} + \Delta(t)\right) dW(t) 
\end{align*}
$$

We set $\Delta(t) = \frac{\partial V}{\partial x}$, thereby eliminating the randomness, the $dW$-term. We are left with:

$$
\begin{align*}
d\Pi(t) 
&=\left[\frac{\partial V}{\partial t} + \frac{1}{2} \sigma^2 S_t^2 \frac{\partial^2 V}{\partial x^2}\right]dt  
\end{align*}
$$

Such a portfolio must earn the risk-free rate. Hence,

$$d\Pi = r(t)\Pi(t)dt$$

Putting it together, we have:

$$
\begin{align*}
r(t)\Pi(t)dt &= \left[\frac{\partial V}{\partial t} + \frac{1}{2} \sigma^2 S_t^2 \frac{\partial^2 V}{\partial x^2}\right]dt\\
r(t)( V(t) + \Delta(t)S(t)) &= \frac{\partial V}{\partial t} + \frac{1}{2} \sigma^2 S_t^2 \frac{\partial^2 V}{\partial x^2}\\
r(t)( V(t) + \frac{\partial V}{\partial x}S(t)) &= \frac{\partial V}{\partial t} + \frac{1}{2} \sigma^2 S_t^2 \frac{\partial^2 V}{\partial x^2}\\
rV(t) &= \frac{\partial V}{\partial t} -r(t)S(t) \frac {\partial V}{\partial x} + \frac{1}{2} \sigma^2 S_t^2 \frac{\partial^2 V}{\partial x^2} 
\end{align*}
$$


