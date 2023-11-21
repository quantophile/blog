---
title: "Exploring Option Greeks"
date: 2023-11-19T22:55:20+01:00
math: katex
tags: ["vanilla-option","european-option","fx-option"]
categories: ["FX Derivatives"]
---

## Introduction.

I derived the Black-Scholes formula for European style vanilla FX options in a previous post [here](https://quantophile.github.io/mathsummaries/post/2023/11/19/garman-kohlhagen-for-european-vanilla-fx-options/). The Black-Scholes model $Bl(S_0,K,T,r_{DOM},r_{FOR},\sigma)$ equipped with a single flat volatility parameter $\sigma$ produces option prices which are **NOT consistent** with the observed market prices of FX options across different strikes and maturities. 

Although, the BS model suffers many flaws, it is still often used, at least for quoting purposes. Since all of the other inputs into the model - market data variables such as the stock price $S_0$, the domestic depo rate $r_{DOM}$, the foreign depo rate $r_{FOR}$, and the parameters such as option strike $K$, the time-to-maturity $T$, can be either seen in the market or are known constants, we can easily solve for the value $\sigma_{\text{imp}}$ of the parameter $\sigma$ such that:

$$Bl(S_0,K,T,r_{DOM},r_{FOR},\sigma_{\text{imp}}) = V_{\text{market}}$$

This value $\sigma_{\text{imp}}$ implied from the market price of the option is called the **implied volatility**. 

Thus, although the BS model suffers from flaws, it is mainly used as a quote converter. In the FX options market, option prices are quoted in terms of implied volatilities. The BS formula is used to convert implied vols $\sigma_{\text{imp}}$ to prices and vice versa. The delta hedge to be exchanged between counterparties is calculated according to the BS formula, and this is also true for the Vega hedge of various exotic options. In many cases, the model is also used to run trading books. 

Market conventions used in the FX markets are usually specified in terms of the price and vol attributes of options with various delta characteristics. So, it's nice to explore the intricacies of various types of FX delta and how they are used in the description of market volatility surfaces. The entire concept of the FX volatility smile is based on the parametrization with respect to delta. 

I walk-through the various market conventions used in practice.

## Quote style conversions.

In FX markets, options are quoted in one of 4 quote styles - domestic per foreign (d/f), percentage foreign (%f), percentage domestic (%d) and foreign per domestic (f/d). 

The standard Black-Scholes formula is:

$$
\begin{align*}
V_{d/f} &= \omega [S_0 e^{-r_{FOR} T} \Phi(d_{+}) - K e^{-r_{DOM}T} \Phi(d_{-})\\\\
&= \omega e^{-r_{DOM}T}[F \Phi(d_{+}) - K  \Phi(d_{-})]
\end{align*}
$$

Whether a call or a put, it is an option to exchange $K$ units of the domestic currency for $1$ unit of the foreign currency, valued in domestic currency - so it is the domestic/foreign price. 

If we want to express the above as a CCY1/CCY1 price, the conversion is easy : we just take the CCY2/CCY1 price above and convert the CCY2 value into CCY1 terms using today's spot rate $S_0$:

$$
V_{\text{\\% f}} = \frac{\omega}{S_0}e^{-r_{DOM}T}[F\Phi(\omega d_{+}) - K\Phi(\omega d_{-})] = \frac{V_{d/f}}{S_0}
$$

For the %CCY2 price, we start with the CCY2/CCY1 price, this being the price in CCY2 of an option with a unit notional in the foreign currency. Since the strike is predetermined, it is also the price in CCY2 of an option with a notional of $K$ in CCY2. So, the CCY1/CCY2 price divided by $K$, is the $%ccy2$ price i.e. the percentage domestic price:

$$V_{\\%d} = \frac{\omega}{K} e^{-r_{DOM}T}[F \Phi(d_{+}) - K e^{-r_{DOM}T} \Phi(d_{-})] = \frac{V_{d/f}}{K}$$

The ccy1/ccy2 price is the price you need to pay in foreign currency for an option on $1$ unit notional of the domestic currency.

$$V_{f/d} = \frac{V_{\\% d}}{S_0} = \frac{V_{d/f}}{S_0 K}$$

The four prices above are relative to the notionals of $K$ in the domestic currency and $1$ in the foreign currency. If the actual notionals are $N_d$ and $N_f$ in domestic and foreign currencies where $N_d = K \cdot N_f$, then we scale accordingly.

### Implementing the Bl Calculator and Option Greeks.


```python
# Author. Quasar C.
# Date. 19-11-2023

import numpy as np
from scipy.stats import norm

# An FX option is the right to exchange 1 unit notional of the 
# foreign currency for K units of the domestic currency at time T. 

class CallPut(Enum):
    CALL_OPTION = 1
    PUT_OPTION = -1
        
def atTheMoneyForward(S_t,K,t,T,r_DOM,r_FOR,sigma):
    foreignDF = np.exp(-r_FOR*(T-t))
    domesticDF = np.exp(-r_DOM*(T-t))
    fwdPoints = foreignDF / domesticDF
    F = fwdPoints * S_t
    return F
        
def dPlus(S_t,K,t,T,r_DOM,r_FOR,sigma):
    F = atTheMoneyForward(S_t,K,t,T,r_DOM,r_FOR,sigma)
    return (np.log(F/K) + (T-t)*(sigma**2)/2)/(sigma * np.sqrt(T - t))

def dMinus(S_t,K,t,T,r_DOM,r_FOR,sigma):
    F = atTheMoneyForward(S_t,K,t,T,r_DOM,r_FOR,sigma)
    return (np.log(F/K) - (T-t)*(sigma**2)/2)/(sigma * np.sqrt(T - t))

def PV(S_t,K,t,T,r_DOM,r_FOR,sigma, CCY1Notional,callPut):
    F = atTheMoneyForward(S_t,K,t,T,r_DOM,r_FOR,sigma)
    omega = callPut.value
    d_plus = dPlus(S_t,K,t,T,r_DOM,r_FOR,sigma)
    d_minus = dMinus(S_t,K,t,T,r_DOM,r_FOR,sigma)
    domesticDF = np.exp(-r_DOM*(T-t))
    
    undiscountedPrice = omega* (F * norm.cdf(omega * d_plus) - K * norm.cdf(omega * d_minus))
    pv = domesticDF * undiscountedPrice * CCY1Notional
    return pv
```

#### Computing the ATM-Forward and the option price


```python
S_t=1.0549 ; K=1.0710 ; t=0.0 ;T=1.0 ; r_DOM=0.041039868 ; r_FOR= 0.025860353; sigma=0.08971 ; CCY1Notional=100.00

ATMForward = atTheMoneyForward(S_t,K,t,T,r_DOM,r_FOR,sigma)

call_price = PV(S_t,K,t,T,r_DOM,r_FOR,sigma, CCY1Notional,callPut = CallPut.CALL_OPTION)
put_price = PV(S_t,K,t,T,r_DOM,r_FOR,sigma, CCY1Notional,callPut = CallPut.PUT_OPTION)
```


```python
print(f"At the money forward = {ATMForward} USD")
print(f"Call Price = {call_price} USD")
print(f"Put Price = {put_price} USD")
```

    At the money forward = 1.0710350214586397 USD
    Call Price = 3.679399488751329 USD
    Put Price = 3.676038161145839 USD
    

#### Plotting the option price against the CCY1CCY2 spot


```python
import matplotlib.pyplot as plt

plt.grid(True)
plt.title('Plot of EUR Call/USD Put Option price')
S_t = np.linspace(0.90,1.24,201)
CCY1Notional = 1.00

call_price_1y = PV(S_t,K,t,1.0,r_DOM,r_FOR,sigma, CCY1Notional,callPut = CallPut.CALL_OPTION)

plt.xlabel(r'EURUSD FX spot')
plt.xlabel(r'Option price (USD)')
plt.plot(S_t,call_price_1y)

plt.show()

```


    
![png](./../../../../exploring-option-greeks01.png)
    



```python
plt.close()

plt.grid(True)
plt.title('Plot of EUR Put/USD Call Option price')

put_price_1y = PV(S_t,K,t,1.0,r_DOM,r_FOR,sigma, CCY1Notional,callPut = CallPut.PUT_OPTION)


plt.xlabel(r'EURUSD FX spot')
plt.xlabel(r'Option price (USD)')

plt.plot(S_t,put_price_1y)

plt.show()
```


    
![png](./../../../../exploring-option-greeks02.png)
    


To derive the deltas, we use the following propositions, which are really easy to prove.

***Proposition.*** 

$$\frac{\partial d_{+}}{\partial S_0} = \frac{\partial d_{-}}{\partial S_0} = \frac{1}{\sigma S_0 \sqrt{T}}$$


***Proof***.

We have:

$$
\begin{align*}
d_{\pm} &= \frac{\log {S_0}}{\sigma \sqrt{T}} - \frac{\log {K} + (r \pm \sigma^2/2)T}{\sigma \sqrt{T}}\\\\
\frac{\partial d_{\pm}}{\partial S_0}&= \frac{1}{\sigma\sqrt{T}}\frac{1}{S_0}
\end{align*}
$$

***Proposition.***

$$\frac{\partial \Phi(\omega d_{\pm})}{\partial S_0} = \frac{\omega}{\sigma S_0 \sqrt{T}}\phi(\omega d_{\pm})$$

***Proof.***

By chain rule, we have:

$$
\begin{align*}
\frac{\partial\Phi(\omega d_{\pm})}{\partial S_0} &= \phi(\omega d_{\pm}) \frac{\partial (\omega d_{\pm})}{dS_0} \\\\
&= \phi(\omega d_{\pm}) \frac{\omega}{\sigma S_0 \sqrt{T}}
\end{align*}
$$

***Proposition***. The following general result holds:

$$\phi(\omega d_{+}) = \phi(\omega d_{-})\exp(\omega^2 [r_{FOR} - r_{DOM}]T)(K/S_0)^{\omega^2}$$

***Proof.***

We have:

$$
d_{+} + d_{-} = 2 \frac{\log (S_0/K) + (r_{FOR} - r_{DOM})T}{\sigma \sqrt{T}}
$$

$$
d_{+} - d_{-} = \sigma\sqrt{T}
$$

$$
\begin{align*}
\frac{\phi(\omega d_{+})}{\phi(\omega d_{-})} &= \exp\left[-\omega^2\left(\frac{d_{+}^2-d_{-}^2}{2}\right)\right]\\\\
&= \exp\left\[-\omega^2(\log (S_0/K) + (r_{DOM} - r_{FOR})T)\right\]\\\\
&= \exp\left\[\omega^2((r_{FOR} - r_{DOM})T)\right\](K/S_0)^{\omega^2}
\end{align*}
$$

### Pips Spot Delta

The pips spot delta is simply the derivative of the option price with respect to the spot rate - both expressed in ccy2/ccy1 terms.

$$\Delta_{S;\text{pips}} = \frac{\partial V_{d;\text{pips}}}{\partial S_0}$$

Thus,

$$
\begin{align*}
\frac{\partial V_{\text{d;pips}}}{\partial S_0} &= \omega\frac{\partial }{\partial S_0} \left[(S_0 e^{-r_{FOR}T} \Phi(\omega d_{+}) - K e^{-r_{DOM}T}\Phi(\omega d_{-})\right)]\\\\
&= \omega \left[e^{-r_{FOR}T} \Phi(\omega d_{+}) + S_0 e^{-r_{FOR}T} \phi (\omega d_{+})\frac{\omega}{\sigma S_0 \sqrt{T}} - K e^{-r_{DOM}T}\phi (\omega d_{-})\frac{\omega}{\sigma S_0 \sqrt{T}}\right]\\\\
&= \omega e^{-r_{FOR}T} \Phi(\omega d_{+}) + \frac{\omega^2}{\sigma S_0 \sqrt{T}}\left[S_0 e^{-r_{FOR}T} \phi(\omega d_{+}) - K e^{-r_{DOM}T}\phi(\omega d_{-})\right]\\\\
&= \omega e^{-r_{FOR}T} \Phi(\omega d_{+}) + \frac{\omega^2}{\sigma S_0 \sqrt{T}}\left[S_0 e^{-r_{FOR}T} e^{(r_{FOR} - r_{DOM})T}\frac{K}{S_0}\phi(\omega d_{-}) - K e^{-r_{DOM}T}\phi(\omega d_{-})\right]\\\\
&= \omega e^{-r_{FOR}T} \Phi(\omega d_{+}) + \frac{\omega^2}{\sigma S_0 \sqrt{T}}\left[K e^{-r_{DOM}T}\phi(\omega d_{-}) - K e^{-r_{DOM}T}\phi(\omega d_{-})\right]\\\\
&= \omega e^{-r_{FOR}T} \Phi(\omega d_{+})
\end{align*}
$$

If we think of a delta hedge, it is just the number of units of foreign currency we need to hold in order to hedge an option with a notional of 1 unit of foreign currency and an equivalent notional of $K$ units of domestic currency. So, the spot delta is expressed as a percentage of the foreign currency.

#### Implementing Analytic Delta.


```python
def analyticDelta(S_t,K,t,T,r_DOM,r_FOR,sigma,CCY1Notional, callPut = CallPut.CALL_OPTION):
    omega = callPut.value
    d_plus = dPlus(S_t,K,t,T,r_DOM,r_FOR,sigma)
    return omega * np.exp(-r_FOR * (T-t)) * norm.cdf(omega * d_plus) * CCY1Notional
```


```python
S_t=1.0549 ; CCY1Notional=100.00

pips_spot_delta = analyticDelta(S_t,K,t,T,r_DOM,r_FOR,sigma,CCY1Notional, callPut = CallPut.CALL_OPTION)
print(f"Spot Delta = {pips_spot_delta} EUR")
```

    Spot Delta = 50.48090225276146 EUR
    

#### Plotting the Analytic Delta of call options


```python
plt.close()

plt.grid(True)
plt.title('Plot of Analytic delta of the European call')
plt.xlabel('EURUSD spot price')
plt.ylabel(r'$\frac{\partial V}{\partial S}$')

S_t = np.linspace(0.90,1.24,201)
CCY1Notional = 1.00
delta = analyticDelta(S_t,K,t,1.0,r_DOM,r_FOR,sigma,CCY1Notional, callPut = CallPut.CALL_OPTION)
plt.plot(S_t,delta,label='T=1Y')
plt.legend(loc="upper left")
plt.show()
```


    
![png](./../../../../exploring-option-greeks03.png)
    


### Forward Delta

The interpretation of the foward delta is the number of units of FOR of forward contracts a trader needs to buy to delta hedge a short option position. According to Wystup, if we translate this hedge ratio in calculus, it means that we need to compute (for a call)

$$
\frac{\partial v_{\text{option}}}{\partial v_{\text{forward}}}
$$

The value of a forward contract $v_{\text{forward}}$ for an agreed forward exchange rate $K$ is:

$$
\begin{align*}
v_{\text{forward}} &= e^{-r_{DOM}T}\mathbb{E}^{\mathbb{Q}^d}[R_T - K]\\\\
&= e^{-r_{DOM}T}(R_0 \mathbb{E}^{\mathbb{Q}^d}[e^{(r_{DOM} - r_{FOR} - (\sigma^2/2))T + \sigma \sqrt{T} Z}] - K)\\\\
&= e^{-r_{DOM}T}(R_0 e^{(r_{DOM} - r_{FOR})T} - K)\\\\
&= R_0 e^{- r_{FOR}T} - K e^{-r_{DOM}T}
\end{align*}
$$

So, the derivative of the value of the forward contract with respect to the spot is:

$$\frac{\partial v_{\text{forward}}}{\partial R_0} = e^{-r_{FOR}T}$$

Using the chain rule and the derivative of the inverse function, we obtain the forward delta:

$$
\begin{align*}
\frac{\partial v_{\text{option}}}{\partial v_{\text{forward}}} &= \frac{\partial v_{\text{option}}}{\partial v_{R_0}} \times \frac{\partial v_{R_0}}{\partial v_{\text{forward}}}\\\\
&=\omega e^{-r_{FOR}T}\Phi(\omega d_{+}) \times e^{r_{FOR}T}\\\\
&= \omega \Phi(\omega d_{+})
\end{align*}
$$


```python
def forwardDelta(S_t,K,t,T,r_DOM,r_FOR,sigma,CCY1Notional, callPut = CallPut.CALL_OPTION):
    omega = callPut.value
    d_plus = dPlus(S_t,K,t,T,r_DOM,r_FOR,sigma)
    return omega  * norm.cdf(omega * d_plus) * CCY1Notional
```


```python
S_t=1.0549 ; CCY1Notional=100.00

forward_delta = forwardDelta(S_t,K,t,T,r_DOM,r_FOR,sigma,CCY1Notional, callPut = CallPut.CALL_OPTION)
print(f"Forward Delta = {forward_delta} EUR of forward contracts")
```

    Forward Delta = 51.803382405811725 EUR of forward contracts
    

## Gamma.

$$
\begin{align*}
\frac{\partial^2 V}{\partial S_0^2} &= \omega e^{-r_{FOR}T} \frac{\partial}{\partial S_0}\Phi(\omega d_{+}) \\\\
&= \omega e^{-r_{FOR}T} \phi(\omega d_{+}) \frac{\omega}{\sigma S_0 \sqrt{T}}\\\\
&= e^{-r_{FOR}T} \frac{\phi(\omega d_{+})}{\sigma S_0 \sqrt{T}}
\end{align*}
$$

The interpretation of the gamma is the change of the delta as the spot changes. A high gamma means that the delta hedge must be adapted very frequently and will cause transaction costs. Gamma is typically high when the spot is near a strike of a barrier, generally, whenever the payoff has a kink or dramatically a jump. Trading systems usually quote gamma as a *trader's gamma*, using a one percent relative change in the spot price. 


```python
def analyticGamma(S_t,K,t,T,r_DOM,r_FOR,sigma,CCY1Notional, callPut = CallPut.CALL_OPTION):
    omega = callPut.value
    d_plus = dPlus(S_t,K,t,T,r_DOM,r_FOR,sigma)
    return np.exp(-r_FOR * (T-t)) * norm.cdf(omega * d_plus) / (sigma * S_t * np.sqrt(T-t)) * CCY1Notional
```


```python
gamma = analyticGamma(S_t,K,t,T,r_DOM,r_FOR,sigma,CCY1Notional, callPut = CallPut.CALL_OPTION)
print(f"Analytic Gamma = {gamma} EUR")
```

    Analytic Gamma = 533.4269573839681 EUR
    

### Theta.

Let $\tau = T- t$, $\frac{\partial \tau}{\partial t} = -1$. 

We first observe that:

$$
\begin{align*}
d_{-} &= d_{+} - \sigma\sqrt{\tau}\\\\
\frac{\partial d_{-}}{\partial t} &= \frac{\partial d_{+}}{\partial t} + \frac{\sigma}{2\sqrt{\tau}}
\end{align*}
$$

$$
\begin{align*}
\phi (d_{-}) &= \exp\left[-\frac{1}{2}(d_{+} - \sigma \sqrt{\tau})^2\right]\\\\
&= \exp\left[-\frac{1}{2}(d_{+}^2 -2 d_{+}\sigma\sqrt{\tau} + \sigma^2 \tau)\right]\\\\
&= \exp\left(-\frac{1}{2}d_{+}^2\right) \exp(d_{+}\sigma\sqrt{\tau}) \exp(-\frac{1}{2} \sigma^2 \tau)\\\\
&= \phi(d_{+}) \exp\left(\log \frac{S_0}{K} + (r_{DOM} - r_{FOR} + \frac{\sigma^2}{2})\tau\right) \exp(-\frac{1}{2} \sigma^2 \tau)\\\\
&= \phi(d_{+}) \frac{S_0}{K} \exp((r_{DOM} - r_{FOR})\tau)\exp(\frac{\sigma^2 \tau}{2}) \exp(-\frac{1}{2} \sigma^2 \tau)\\\\
&= \frac{S_0}{K} \cdot \phi(d_{+}) e^{(r_{DOM} - r_{FOR})\tau}
\end{align*}
$$

And since $\phi(\omega d_{\pm}) = \phi(d_{\pm})$, we can write:

$$\phi(\omega d_{-})= \frac{S_0}{K} \phi(\omega d_{+}) e^{(r_{DOM} - r_{FOR})\tau}$$

The value function of a vanilla European option is:

$$v_{\text{option}} = \omega [S_0 e^{-r_{FOR}\tau} \Phi(\omega d_{+}) - K e^{-r_{DOM}\tau} \Phi(\omega d_{-})]$$


Differentiating with respect to $t$, we get:

$$\frac{\partial v_{\text{option}}}{\partial t} = \omega[S_0 \frac{\partial }{\partial t}e^{-r_{FOR}\tau}\Phi(\omega d_{+}) - K \frac{\partial }{\partial t} e^{-r_{DOM}\tau}\Phi(\omega d_{-})]$$

The first term can be expressed as:

$$
\begin{align*}
\frac{\partial }{\partial t} e^{-r_{FOR}\tau} \Phi(\omega d_{+}) &= r_{FOR}e^{-r_{FOR}\tau}\Phi(\omega d_{+}) + \omega e^{-r_{FOR}\tau} \phi(\omega d_{+}) \frac{\partial d_{+}}{\partial t}
\end{align*}
$$

The second term can be expressed as:

$$
\begin{align*}
\frac{\partial }{\partial t} e^{-r_{DOM}\tau}\Phi(\omega d_{-}) &= r_{DOM}e^{-r_{DOM}\tau}\Phi(\omega d_{-}) + \omega  e^{-r_{DOM}\tau}\phi(\omega d_{-}) \frac{\partial d_{-}}{\partial t}\\\\
&=r_{DOM}e^{-r_{DOM}\tau}\Phi(\omega d_{-}) + \omega \cdot \frac{S_0}{K}  e^{-r_{DOM}\tau}\phi(\omega d_{+}) e^{(r_{DOM} - r_{FOR})\tau}\left(\frac{\partial d_{+}}{\partial t} + \frac{\sigma}{2\sqrt{\tau}}\right)\\\\
&=r_{DOM}e^{-r_{DOM}\tau}\Phi(\omega d_{-}) + \omega \cdot \frac{S_0}{K}  e^{-r_{FOR}\tau}\phi(\omega d_{+}) \left(\frac{\partial d_{+}}{\partial t} + \frac{\sigma}{2\sqrt{\tau}}\right)\\\\
\end{align*}
$$

Collecting the two terms we have:

$$
\begin{align*}
&S_0 \frac{\partial }{\partial t} e^{-r_{FOR}\tau} \Phi(\omega d_{+}) - K \frac{\partial }{\partial t} e^{-r_{DOM}\tau}\Phi(\omega d_{-}) \\\\
=& S_0 r_{FOR}e^{-r_{FOR}\tau}\Phi(\omega d_{+}) + \omega S_0 e^{-r_{FOR}\tau} \phi(\omega d_{+}) \frac{\partial d_{+}}{\partial t}\\\\
-& K r_{DOM}e^{-r_{DOM}\tau}\Phi(\omega d_{-}) - \omega S_0  e^{-r_{FOR}\tau}\phi(\omega d_{+}) \left(\frac{\partial d_{+}}{\partial t} + \frac{\sigma}{2\sqrt{\tau}}\right)\\\\
=& S_0 r_{FOR}e^{-r_{FOR}\tau}\Phi(\omega d_{+}) - K r_{DOM}e^{-r_{DOM}\tau}\Phi(\omega d_{-}) - \omega S_0  e^{-r_{FOR}\tau}\phi(\omega d_{+}) \frac{\sigma}{2\sqrt{\tau}}
\end{align*}
$$

Therefore,

$$
\begin{align*}
\frac{\partial v_{\text{option}}}{\partial t} &= \omega [S_0 r_{FOR}e^{-r_{FOR}\tau}\Phi(\omega d_{+}) - K r_{DOM}e^{-r_{DOM}\tau}\Phi(\omega d_{-})] \\\\
&- S_0  e^{-r_{FOR}\tau}\phi(\omega d_{+}) \frac{\sigma}{2\sqrt{\tau}}
\end{align*}
$$


```python
def analyticTheta(S_t,K,t,T,r_DOM,r_FOR,sigma,CCY1Notional, callPut = CallPut.CALL_OPTION):    
    
    omega = callPut.value
    FOR_df = np.exp(-r_FOR*(T-t)); DOM_df =np.exp(-r_DOM*(T-t));
    dplus = dPlus(S_t,K,t,T,r_DOM,r_FOR,sigma); dminus = dMinus(S_t,K,t,T,r_DOM,r_FOR,sigma);
    Nd1 = norm.cdf(omega * dplus); Nd2 = norm.cdf(omega * dminus)
    
    theta = (omega * (S_t * r_FOR * FOR_df * Nd1 - K * r_DOM * DOM_df * Nd2) 
            - S_t * FOR_df * Nd1 * (sigma / (2 * np.sqrt(T-t)))) * CCY1Notional
    
    return theta
```


```python
S_t=1.0549 ; CCY1Notional=100.00

theta = analyticTheta(S_t,K,t,T,r_DOM,r_FOR,sigma,CCY1Notional, callPut = CallPut.CALL_OPTION)
print(f"Analytic Theta = {theta} USD")
```

    Analytic Theta = -3.04597416111385 USD
    

Theta reflects the change of the option value as the clock ticks. The *trader's theta* in a risk-management system refers to the change in the option value in one day, i.e. it can be approximated by $365 \frac{\partial v}{\partial t}$.

### Vega.

$$
\begin{align*}
\frac{\partial v}{\partial \sigma} &= \omega[S_0 e^{-r_{FOR}\tau} \frac{\partial}{\partial \sigma}\Phi(\omega d_{+}) - K e^{-r_{DOM}\tau} \frac{\partial}{\partial \sigma}\Phi(\omega d_{-})]\\\\
 &= \omega[S_0 e^{-r_{FOR}\tau} \phi(\omega d_{+})\frac{\partial d_{+}}{\partial \sigma} - K e^{-r_{DOM}\tau} \phi(\omega d_{-}) \frac{\partial d_{-}}{\partial \sigma}]
\end{align*}
$$

Note that, $d_{-} = d_{+} - \sigma\sqrt{\tau}$, so $\frac{\partial d_{-}}{\partial \sigma} = \frac{\partial d_{+}}{\partial \sigma} - \sqrt{\tau}$. 

Also, $\phi(\omega d_{-})=\frac{K}{S_0}e^{(r_{DOM} - r_{FOR})\tau}\phi(\omega d_{+})$.

Plugging these two facts in the expression for option vega, we get:

$$
\begin{align*}
\frac{\partial v}{\partial \sigma}  &= \omega[S_0 e^{-r_{FOR}\tau} \phi(\omega d_{+})\frac{\partial d_{+}}{\partial \sigma} \\\\
&- K e^{-r_{DOM}\tau} \frac{K}{S_0}e^{(r_{DOM} - r_{FOR})\tau}\phi(\omega d_{+}) \left(\frac{\partial d_{+}}{\partial \sigma} - \sqrt{\tau}\right)]\\\\
&= S_0 e^{-r_{FOR}\tau} \phi(\omega d_{+}) \sqrt{\tau}
\end{align*}
$$

### Vanna.

The vanna is *dvega/dspot*. It reflects the change in the vega as the spot moves.

$$
\begin{align*}
\frac{\partial^2 v}{\partial \sigma \partial S_0} &= \frac{\partial}{\partial S_0} \left(\frac{\partial v}{\partial \sigma}\right)\\\\
&= e^{-r_{FOR}\tau} \sqrt{\tau}\cdot \frac{\partial}{\partial S_0}(S_0\phi(\omega d_{+}))\\\\
&= e^{-r_{FOR}\tau} \sqrt{\tau}(\phi(\omega d_{+}) + S_0 \frac{\partial}{\partial S_0}\phi(\omega d_{+}))\\\\
&= e^{-r_{FOR}\tau} \sqrt{\tau}(\phi(\omega d_{+}) + \omega S_0 \frac{\partial}{\partial d_{+}}\phi(\omega d_{+})\cdot \frac{\partial d_{+}}{\partial S_0})\\\\
&= e^{-r_{FOR}\tau} \sqrt{\tau}(\phi(\omega d_{+}) + \omega S_0\frac{1}{\sqrt{2\pi}} \cdot\frac{\partial}{\partial d_{+}}\exp(-d_{+}^2/2)\cdot \frac{1}{\sigma S_0 \sqrt{\tau}})\\\\
&= e^{-r_{FOR}\tau} \sqrt{\tau}(\phi(\omega d_{+}) + \omega \frac{1}{\sqrt{2\pi}}e^{-d_{+}^2/2} (-d_{+})\cdot \frac{1}{\sigma \sqrt{\tau}})\\\\
&= e^{-r_{FOR}\tau} \sqrt{\tau}\phi(\omega d_{+})(1 -  \frac{d_{+}}{\sigma \sqrt{\tau}})\\\\
&= -e^{-r_{FOR}\tau} \phi(\omega d_{+})\frac{d_{-}}{\sigma}
\end{align*}
$$

### Volga.

The volga is *dvega/dvol*. It reflects the change in the vega as the vol moves.


