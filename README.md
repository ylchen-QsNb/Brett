# Brett: Bidirectional recursive encoder from transformer time-dependent

## Introduction and motivation
If $T_1(\cdot), ..., T_L(\cdot)$ denote the maps from one layer of stacked transformer structure (encoders or decoders), we have
```math
T_l(x) = f_l(A_l(x)+x),
```
where the function $f_l(\cdot)$ denotes the normalization, e.g. layer normalization or RMS normalization, and $A_l(\cdot)$ is the function represents the combination of feed-forward layer and self-attention layer. This res-net-like structure of multi-layer transformer can be considered as a numerical solver of an ODE. For instance, in  simplest case where $f_l(x) = x$, if we think $A_l(x) = \Delta t~h_l(x)$, the entire network can be interpreted as a ODE solver using Gaussian method to solve the following dynamical system
```math
\frac{dy}{dt} = h(x, t).
```
The traditional solution to it, like Bert or GPT, is to set a fixed $\Delta t = t_{i+1}-t_i$ and to learn the time-dependent function on each time slice, i.e. $h(\cdot, t_1), ..., h(\cdot, t_L)$. This is way too much parameter waste and redundancy.

An clever solution is to use neural ODE to solve this. This is better than recursive neural network which is equavalent to use constant $\Delta t$ and way better that tranditional stacked transformer structure as discussed.

## Structure of Brett

![fig1](https://user-images.githubusercontent.com/127647390/236728158-88d38051-3f70-4eb0-be23-8e3f89dc50d2.png#center)
![fig2](https://user-images.githubusercontent.com/127647390/236730308-4f23ada2-e0f5-4852-a16f-03d1fcfa7a09.png)

```math
t_0 = 0,~~~ t_n = 1,~~~  t_1, ..., t_{n-1} \sim \mathcal{U}(0, 1)
```
