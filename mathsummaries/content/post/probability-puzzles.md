---
title: "[Quant Interviews] probability puzzles"
date: 2023-09-14T13:17:07+02:00
math: true
tags: ["probability"]
categories: ["Quant Puzzles"]
---

# Probability puzzles. {#probability-puzzles. .unnumbered}

**Problem.** Two bullets are loaded into a gun's round barrel consecutively.
The barrel has a capacity of 6. The gun is fired once, but no bullet is
shot. Does rolling the barrel (shuffling) before next shot increase the
probability of firing a bullet?

<https://brainstellar.com/puzzles/easy/1>

*Solution.*

Let the holes in the barrel be $1,2,3,4,5,6$ labelled clockwise. WLOG,
suppose the firing pin was on hole $1$. Also, suppose the barrel rotates
clockwise. It's given that the gun is fired once, but no bullet was
shot. It implies that the bullets must have been loaded in $(2,3)$,
$(3,4),(4,5)$ or $(5,6)$. There's a $1/4=25$ percent chance of firing a
bullet, on the next shot; that is, if the bullets were loaded in
$(5,6)$.

On the other hand, if the barrel is shuffled, there are $6$ holes the
firing pin could point to; out of which $2$ are favorable. That's a
$2/6\approx 33$ percent chance of firing the bullet.

So, shuffling the barrel increases the chances of firing a bullet from
$25$ percent to $33$ percent.
