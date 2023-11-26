---
title: "Implementing Vanna Volga"
date: 2023-11-26T14:46:22+01:00
math: katex
tags: ["vanna-volga"]
categories: ["Volatility Surface"]
---

## Background.

It is possible to calculate analytically the values of vanillas or barrier options using the Black-Scholes model, however, they are far from quoted prices. This is because the BS-model is based on the assumption that the volatility $\sigma$ of the stock price process remains constant throughout the lifetime of the option.

The *vanna-volga* method also known as the *trader's rule of thumb* is based on adding an analytical correction to the Black-Scholes price of the instrument. In this note, I derive and implement the original paper *[The vanna-volga method for implied volatilities](http://quantlabs.net/academy/download/free_quant_instituitional_books_/[Risk%20Magazine,%20Castagna]%20The%20Vanna-Volga%20Method%20for%20Implied%20Volatilities.pdf)*, by Castagna and Mercurio.

## Replicating Portfolio.

Consider a Black-Scholes world with two assets : a locally risk free domestic bank account $B(t)$ and a stock $S(t)$. We assume that the volatility of the stock is stochastic, but strike-independent(flat). We have the asset dynamics:

$$
\begin{align*}
dB_t &= r_{DOM}B_t dt \\\\
dS_t &= \mu S_t dt + \sigma_t S_t dW_t
\end{align*}
$$

Our aim is to value an arbitrary option contract $O=f(t,S_t,\sigma_t;K)$ with a strike $K$. We price $O$ using a standard hedging argument. We build a hedge aka replicating portfolio such that it zeroes out the greeks of our net position upto the second order. 

Consider a self-financing portfolio $\Pi_t$ consisting of:

- A long position in $1$ unit of the option $O(t;K)$.
- A short position in $\Delta_t$ units of the stock $S_t$.
- Short positions in three European vanilla pivot options $C_i$, $i \in \{1,2,3\}$. We short $x_i$ units of $C_i$. It is standard practice, to take $C_1,C_2,C_3$ as a 25-delta put, an ATM call and a 25-delta call option respectively.  

The pivot options have strikes $K_1 = K_{25P}$, $K_2 = K_{ATM}$ and $K_3 = K_{25C}$ and implied volatility quotes (market prices) $\sigma_1$, $\sigma_2$ and $\sigma_3$ which are known to us.

The value of the portfolio at time $t$ is:

$$\Pi_t = O_t - \Delta_t S_t - \sum_{i=1}^{3} x_i C_t^i \tag{1}$$

By self-financing, I mean, there is no exogenous infusion or withdrawal of cash, once the portfolio has been setup at time zero. Therefore, the changes in the portfolio are solely due to gains/losses on the constituents. The self-financing condition is:

$$d\Pi_t = dO_t - \Delta_t dS_t - \sum_{i=1}^{3} x_i dC_t^i \tag{2}$$

By Ito's lemma, the differential of the option price $O_t$ can be written as:

$$
\begin{align*}
dO_t &= \frac{\partial O}{\partial t} dt + \frac{\partial O}{\partial S_t} dS_t + \frac{\partial O}{\partial \sigma_t} d\sigma_t \\\\
&+ \frac{1}{2}\frac{\partial^2 O}{\partial t^2} (dt)^2 \\\\
&+ \frac{1}{2}\frac{\partial^2 O}{\partial S_t^2} (dS_t)^2 \\\\
&+ \frac{1}{2}\frac{\partial^2 O}{\partial \sigma_t^2} (d\sigma_t)^2 \\\\
&+ \frac{\partial^2 O}{\partial t \partial S_t} dt \cdot dS_t \\\\
&+ \frac{\partial^2 O}{\partial S_t \partial \sigma_t} dS_t \cdot d\sigma_t \\\\
&+ \frac{\partial^2 O}{\partial t \partial \sigma_t} dt \cdot d\sigma_t \tag{3}
\end{align*}
$$

Since $(dt)^2$, $dt \cdot dS_t$, $dt \cdot d\sigma_t$ are equal to zero, we can write:

$$
\begin{align*}
dO_t &= \frac{\partial O}{\partial t} dt + \frac{\partial O}{\partial S_t} dS_t + \frac{\partial O}{\partial \sigma_t} d\sigma_t \\\\
&+ \frac{1}{2}\frac{\partial^2 O}{\partial S_t^2} (dS_t)^2 \\\\
&+ \frac{1}{2}\frac{\partial^2 O}{\partial \sigma_t^2} (d\sigma_t)^2 \\\\
&+ \frac{\partial^2 O}{\partial S_t \partial \sigma_t} dS_t \cdot d\sigma_t  \tag{4}
\end{align*}
$$

Similarly, we can apply Ito's lemma to the European vanilla pivot options to find the differential $dC^i_t$. Putting it together we have:

$$
\begin{align*}
d\Pi_t &= \left(\frac{\partial O(t;K)}{\partial t} - \sum_{i=1}^{3}x_i\frac{\partial C^i(t;K_i)}{\partial t} \right) dt  \\\\
&+ \left(\frac{\partial O(t;K)}{\partial S_t}  - \Delta_t - \sum_{i=1}^{3}x_i\frac{\partial C^i(t;K_i)}{\partial S_t}\right) dS_t \\\\
&+ \left(\frac{\partial O(t;K)}{\partial \sigma_t} - \sum_{i=1}^{3}x_i\frac{\partial C^i(t;K_i)}{\partial \sigma_t} \right)d\sigma_t\\\\
&+ \frac{1}{2}\left(\frac{\partial^2 O(t;K)}{\partial S_t^2} - \sum_{i=1}^{3}x_i\frac{\partial^2 C^i(t;K_i)}{\partial S_t^2}\right)(dS_t)^2 \\\\
&+ \frac{1}{2}\left(\frac{\partial^2 O(t;K)}{\partial \sigma_t^2}  - \sum_{i=1}^{3}x_i\frac{\partial^2 C^i(t;K_i)}{\partial \sigma_t^2} \right)(d\sigma_t)^2 \\\\
&+ \left(\frac{\partial^2 O(t;K)}{\partial S_t \partial \sigma_t} - \sum_{i=1}^{3}x_i\frac{\partial^2 C^i(t;K_i)}{\partial S_t \partial \sigma_t}\right)  dS_t \cdot d\sigma_t  \tag{5}
\end{align*}
$$

We claim that we can choose the weights $\Delta_t$ and $\mathbf{x}=(x_1,x_2,x_3)$ of the replicating portfolio, such that the coefficient of the terms $dS_t$, $d\sigma_t$, $(d\sigma_t)^2$ and $dS_t \cdot d\sigma_t$ are zeroed out.

We are therefore left with:

$$
\begin{align*}
d\Pi_t &= \left(\frac{\partial O}{\partial t} - \sum_{i=1}^{3}x_i\frac{\partial C^i_t}{\partial t} \right) dt \\\\
&+ \frac{1}{2}\left(\frac{\partial^2 O}{\partial S_t^2} - \sum_{i=1}^{3}x_i\frac{\partial^2 C^i_t}{\partial S_t^2}\right)\sigma_t^2 S_t^2 dt \tag{6}
\end{align*}
$$

The portfolio value process has no driving Brownian motion $dW_t$ term, and hence the source of randomness has been eliminated. Therefore, $\Pi_t$ must be a locally risk-free portfolio. That is, it satisfies:

$$d\Pi_t = r_{DOM}\Pi_t dt$$

## Calculating the VV weights.

We assume $t=0$, so we can drop the argument $t$ in the call prices $C_i(t;K)$ in equation (5). The weights $\mathbf{x}=(x_1,x_2,x_3)$ are determined by solving the system of equations $A\mathbf{x}=\mathbf{b}$ where:

$$
A = \begin{bmatrix}
\frac{\partial C_1(K_1)}{\partial \sigma_t} & \frac{\partial C_1(K_2)}{\partial \sigma_t} &  \frac{\partial C_3(K_3)}{\partial \sigma_t} \\\\
\frac{\partial^2 C_1(K_1)}{\partial S_t \partial \sigma_t} & \frac{\partial^2 C_2(K_2)}{\partial S_t \partial \sigma_t} & \frac{\partial^2 C_3(K_3)}{\partial S_t \partial \sigma_t}\\\\
\frac{\partial^2 C_1(K_1)}{\partial \sigma_t^2} & \frac{\partial^2 C_2(K_2)}{\partial \sigma_t^2} & \frac{\partial^2 C_3(K_3)}{\partial \sigma_t^2}
\end{bmatrix}, \quad
\mathbf{b} = \begin{bmatrix}
\frac{\partial O(K)}{\partial \sigma_t} \\\\
\frac{\partial^2 O(K)}{\partial S_t \partial \sigma_t} \\\\
\frac{\partial^2 O(K)}{\partial \sigma_t^2} 
\end{bmatrix}
$$




The entries in the first, second and third rows of $A$ and $\mathbf{b}$ are the option vega, the option vanna and the option volga. 

I derived the expressions for option vega, vanna and volga [here](https://quantophile.github.io/mathsummaries/post/2023/11/19/exploring-option-greeks/). They are:

$$
\begin{align*}
\text{Vega} &= S_0 e^{-r_{FOR}T} \phi(d_{+}) \sqrt{T} \\\\
\text{Vanna} &= -e^{-r_{FOR}T} \phi(d_{+})\frac{d_{-}}{\sigma}\\\\
\text{Volga} &= S_0 e^{-r_{FOR}T}\sqrt{T}\phi(d_{+}) \frac{d_{+}d_{-}}{\sigma} 
\end{align*}
$$

We can re-phrase the other greeks in terms of vega $\mathcal{V}$. Recall, that $d_{+}$ varies with the option strike $K$, so all other things equal, we can write $\mathcal{V} = \mathcal{V}(K)$. Also, $\sigma$ is the volatility of the stock-price process in the Black-Scholes framework, and by assumption it is strike-independent, so $\sigma(t;K) = \sigma$. 

$$
\begin{align*}
\text{Vanna} &= -\frac{d_{-}}{\sigma S_0 \sqrt{T}} \mathcal{V}(K)\\\\
\text{Volga} &= \frac{d_{+}d_{-}}{\sigma} \mathcal{V}(K)
\end{align*}
$$

The augmented matrix $[A | b]$, therefore is:

$$
\begin{bmatrix}
\mathcal{V}(K_1) & \mathcal{V}(K_2) &  \mathcal{V}(K_3) & | & \mathcal{V}(K)\\\\
-\frac{d_{-}(K_1)}{\sigma S_0 \sqrt{T}}\mathcal{V}(K_1) & -\frac{d_{-}(K_2)}{\sigma S_0 \sqrt{T}}\mathcal{V}(K_2) & -\frac{d_{-}(K_3)}{\sigma S_0 \sqrt{T}}\mathcal{V}(K_3) & | &\frac{d_{-}(K)}{\sigma S_0 \sqrt{T}}\mathcal{V}(K)\\\\
\frac{d_{+}(K_1) d_{-}(K_1)}{\sigma}\mathcal{V}(K_1) & \frac{d_{+}(K_2) d_{-}(K_2)}{\sigma}\mathcal{V}(K_2) & \frac{d_{+}(K_3) d_{-}(K_3)}{\sigma}\mathcal{V}(K_3) & | & \frac{d_{+}(K) d_{-}(K)}{\sigma}\mathcal{V}(K)
\end{bmatrix}
$$

Cancelling out the constant terms, we get:

$$
\begin{bmatrix}
\mathcal{V}(K_1) & \mathcal{V}(K_2) &  \mathcal{V}(K_3) & | & \mathcal{V}(K)\\\\
d_{-}(K_1)\mathcal{V}(K_1) & d_{-}(K_2)\mathcal{V}(K_2) & d_{-}(K_3)\mathcal{V}(K_3) & | & d_{-}(K)\mathcal{V}(K)\\\\
d_{+}(K_1) d_{-}(K_1)\mathcal{V}(K_1) & d_{+}(K_2) d_{-}(K_2)\mathcal{V}(K_2) & d_{+}(K_3) d_{-}(K_3)\mathcal{V}(K_3) & | & d_{+}(K) d_{-}(K)\mathcal{V}(K)
\end{bmatrix}
$$

Performing the elementary row operation $R_3 \leftarrow R_3 - d_{+}(K_1) R_2$, we get:

$$
\begin{bmatrix}
\mathcal{V}(K_1) & \mathcal{V}(K_2) &  \mathcal{V}(K_3) & | & \mathcal{V}(K)\\\\
d_{-}(K_1)\mathcal{V}(K_1) & d_{-}(K_2)\mathcal{V}(K_2) & d_{-}(K_3)\mathcal{V}(K_3) & | & d_{-}(K)\mathcal{V}(K)\\\\
0 & \log\frac{K_2}{K_1} d_{-}(K_2)\mathcal{V}(K_2) & \log \frac{K_3}{K_1} d_{-}(K_3)\mathcal{V}(K_3) & | & \log \frac{K}{K_1} d_{-}(K)\mathcal{V}(K)
\end{bmatrix}
$$

Performing the elementary row operation $R_2 \leftarrow R_2 - d_{-}(K_1)R_1$, we get:

$$
\begin{bmatrix}
\mathcal{V}(K_1) & \mathcal{V}(K_2) &  \mathcal{V}(K_3) & | & \mathcal{V}(K)\\\\
0 & \log\frac{K_2}{K_1}\mathcal{V}(K_2) & \log \frac{K_3}{K_1}\mathcal{V}(K_3) & | & \log \frac{K}{K_1}\mathcal{V}(K)\\\\
0 & \log\frac{K_2}{K_1} d_{-}(K_2)\mathcal{V}(K_2) & \log \frac{K_3}{K_1} d_{-}(K_3)\mathcal{V}(K_3) & | & \log \frac{K}{K_1} d_{-}(K)\mathcal{V}(K)
\end{bmatrix}
$$

Performing the elementary row operation $R_3 \leftarrow R_3 - d_{-}(K_2) R_2$, we get:

$$
\begin{bmatrix}
\mathcal{V}(K_1) & \mathcal{V}(K_2) &  \mathcal{V}(K_3) & | & \mathcal{V}(K)\\\\
0 & \log\frac{K_2}{K_1}\mathcal{V}(K_2) & \log \frac{K_3}{K_1}\mathcal{V}(K_3) & | & \log \frac{K}{K_1}\mathcal{V}(K)\\\\
0 & 0 & \log \frac{K_3}{K_1} \frac{K_3}{K_2}\mathcal{V}(K_3) & | & \log \frac{K}{K_1} \log \frac{K}{K_2}\mathcal{V}(K)
\end{bmatrix}
$$

Performing the elementary row operation $R_1 \leftarrow \log(K_2/K_1) R_1 - R_2$, we get:

$$
\begin{bmatrix}
\log \frac{K_2}{K_1}\mathcal{V}(K_1) & 0 & - \log \frac{K_3}{K_2}\mathcal{V}(K_3) & | & -\log \frac{K}{K_2}\mathcal{V}(K)\\\\
0 & \log\frac{K_2}{K_1}\mathcal{V}(K_2) & \log \frac{K_3}{K_1}\mathcal{V}(K_3) & | & \log \frac{K}{K_1}\mathcal{V}(K)\\\\
0 & 0 & \log \frac{K_3}{K_1} \log \frac{K_3}{K_2}\mathcal{V}(K_3) & | & \log \frac{K}{K_1} \log \frac{K}{K_2}\mathcal{V}(K)
\end{bmatrix}
$$

Performing the elementary row operation $R_1 \leftarrow \log(K_3/K_1)R_1 + R_3$, we get:

$$
\begin{bmatrix}
\log \frac{K_3}{K_1}\log \frac{K_2}{K_1}\mathcal{V}(K_1) & 0 & 0 & | & \log \frac{K}{K_3}\log \frac{K}{K_2}\mathcal{V}(K)\\\\
0 & \log\frac{K_2}{K_1}\mathcal{V}(K_2) & \log \frac{K_3}{K_1}\mathcal{V}(K_3) & | & \log \frac{K}{K_1}\mathcal{V}(K)\\\\
0 & 0 & \log \frac{K_3}{K_1} \log \frac{K_3}{K_2}\mathcal{V}(K_3) & | & \log \frac{K}{K_1} \log \frac{K}{K_2}\mathcal{V}(K)
\end{bmatrix}
$$

Performing the elementary row operation $R_2 \leftarrow \log(K_3/K_2) R_2 - R_3$, we get:

$$
\begin{bmatrix}
\log \frac{K_3}{K_1}\log \frac{K_2}{K_1}\mathcal{V}(K_1) & 0 & 0 & | & \log \frac{K}{K_3}\log \frac{K}{K_2}\mathcal{V}(K)\\\\
0 & \log\frac{K_2}{K_1} \log \frac{K_3}{K_2}\mathcal{V}(K_2) & 0 & | & \log \frac{K}{K_1} \log \frac{K_3}{K}\mathcal{V}(K)\\\\
0 & 0 & \log \frac{K_3}{K_1} \log \frac{K_3}{K_2}\mathcal{V}(K_3) & | & \log \frac{K}{K_1} \log \frac{K}{K_2}\mathcal{V}(K)
\end{bmatrix}
$$

Thus, the solution vector $\mathbf{x}$ is:

$$
\begin{align*}
x_1 &= \frac{\log \frac{K_3}{K}\log \frac{K_2}{K}\mathcal{V}(K)}{\log \frac{K_3}{K_1}\log \frac{K_2}{K_1}\mathcal{V}(K_1)}\\\\
x_2 &= \frac{\log \frac{K}{K_1} \log \frac{K_3}{K}\mathcal{V}(K)}{\log\frac{K_2}{K_1} \log \frac{K_3}{K_2}\mathcal{V}(K_2)}\\\\
x_3 &= \frac{\log \frac{K}{K_1} \log \frac{K}{K_2}\mathcal{V}(K)}{\log \frac{K_3}{K_1} \log \frac{K_3}{K_2}\mathcal{V}(K_3)}
\end{align*}
$$


