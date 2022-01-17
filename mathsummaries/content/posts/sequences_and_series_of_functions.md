---
title: Sequences and Series of Functions
date: 2022-01-17T20:38:23+01:00
math: true
---

This is some content.

```julia

function fixedPoint(f::Function, x₀, ϵ=0.5E-6, max_iterations=500)
    x = Vector{Float64}()

    # Initial seed
    push!(x,x₀)
    x_old = x₀

    n = 1
    while(n < max_iterations)

        x_new = f(x_old)
        push!(x,x_new)

        if(abs(x_new - x_old) < ϵ)
            return true, x, n, x_new
        end

        x_old = x_new
        n = n + 1
    end;

    return false, x, n, x_old

end;

```

The function $f(x) = x^2$
