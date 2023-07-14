---
title: Applied Mathematics and Noise
date: 2023-06-18 21:10:55
tags:
- random process
- noise
categories:
- dsp
mathjax: true
---

*This is a summary and overview, not original work. Most derivations etc. are based on those in the references; any mistakes are my own.*



## a long way to go

&#128162; random process

&#128162; sde

---


In applying frequency-domain techniques to the analysis of random signals the natural approach is to Fourier transform the signals.

Unfortunately the Fourier transform of a stochastic process does not, strictly speaking, exist because it has infinite signal energy.


## Phase Noise Model

Consider a stable periodic oscillator subjected to random fluctuations, so that is satisfies a vector Ito stochastic differential equation of the form

$$
dX = \mathbf{f(X)}dt + G(X)dW
$$


### General Model
Two assumptions:

- random trajectory perturbations in directions tangent to the isochron surface passing through $X(t)$ will never accumulate

- random fluctuations in the direction of the tangent to the stable orbit accumulate

This suggests therefore the approximation

$$
X(t) \simeq \mathbf{x}_c(t+\alpha(t)) + \mathbf{\Delta}(t)
$$

where $\mathbf{\Delta}(t)$ represents  a small perturbation belonging to the tangent space to the isochron surface pass through $\mathbf{x}_c(t+\alpha(t))$

If $\phi(X(t))$ is the asymptotic phase corresponding to trajectory point $X(t)$, the **phase noise**

$$
\alpha(t) = \phi(X(t)) - t
$$

After rigorous Ito's process, it can be proven that the phase noise $\alpha(t)$ satisfies the scalar Ito stochastic differential equation

$$
d\alpha(t) = \mathbf{q}_1^T(t+\alpha(t))G(\mathbf{x}_c(t+\alpha(t)))dW(t)
$$

The equation models the *unwrapped* phase noise $\alpha(t)$, which takes values in $\mathbb{R}$



> $d\alpha(t) = \mathbf{q}_1^T(t+\alpha(t))G(\mathbf{x}_c(t+\alpha(t)))dW(t)$ can be seen as the perturbation $G(\mathbf{x}_c(t+\alpha(t)))dW(t)$ projected onto phase gradient $\mathbf{q}_1$



## mathematical background

### Linear systems of ODEs

#### Exact equations

Suppose $F(x; y)$ is a function of two variables, which we call the **potential function**, which suggest potential energy, or electric potential ($F(x; y) = C$).

We take the *total derivative* of $F$:
$$
dF = \frac{\partial F}{\partial x}dx +\frac{\partial F}{\partial y}dy
$$
We apply the total derivative to $F(x; y) = C$, to find the differential equation $dF=0$

An equation of the form
$$
M(x,y)+N(x,y)\frac{dy}{dx}=0
$$
is called **exact** if it was obtained as $dF = 0$ for some *potential function* $F$



#### integrating factor

Given a linear first order equation:
$$
y'+p(x)y = f(x)
$$
The **integrating factor** is defined as
$$
r(x) = e^{\int p(x)dx}
$$
We multiply the above linear first order equation with $r(x)$
$$\begin{align}
y'+p(x)y &= f(x) \\
e^{\int p(x)dx}y'+e^{\int p(x)dx}p(x)y &=e^{\int p(x)dx}f(x) \\
\frac{d}{dx}\left[e^{\int p(x)dx}y\right] &=e^{\int p(x)dx}f(x) \\
e^{\int p(x)dx}y &= \int e^{\int p(x)dx}f(x)dx + C \\
y &= e^{-\int p(x)dx}\left(  \int e^{\int p(x)dx}f(x)dx + C \right)
\end{align}$$

> Of course, to get a closed form formula for $y$, we need to be able to find a closed form formula for the integrals appearing above




### Nonlinear Autonomous Systems of ODEs

We restrict our attention to a two-dimensional autonomous system
$$\begin{align}
x' &= f(x,y) \\
y' &= g(x,y)
\end{align}$$

where $f(x,y)$ and $g(x,y)$ are functions of two variables, and the derivatives are taken with respect to time $t$

#### critical points

**critical points** are the points where both $f(x; y) = 0$ and $g(x; y) = 0$



#### Linearization

we want to linearize the two functions $f(x; y)$ and $g(x; y)$ that define this system. To do so, we will replace $f$ and $g$ by the *tangent plane* approximation to the functions.

Since $(x_0; y_0)$ is a critical point, we know that $f(x_0; y_0) = 0$, so the tangent plane is given by
$$
L_f(x; y) = f_x(x_0; y_0)(x − x_0) + f_y(x_0; y_0)(y − y_0)
$$
Similarly, the tangent plane for $g(x; y)$ near the critical point $(x_0; y_0)$ is given by
$$
L_g(x; y) = g_x(x_0; y_0)(x − x_0) + g_y(x_0; y_0)(y − y_0)
$$
That means that we can *approximate* the solution to $x' = f(x,y);\quad y' = g(x,y)$ near the critical point $(x_0, y_0)$ *by* the solution to the system
$$\begin{align}
\frac{dx}{dt} &= f_x(x_0, y_0)(x − x_0) + f_y(x_0, y_0)(y − y_0) \\
\frac{dy}{dt} &= g_x(x_0, y_0)(x − x_0) + g_y(x_0, y_0)(y − y_0) 
\end{align}$$

Next, change variables to $(u,v)$. That is $u=x-x_0; \quad v=y-y_0$, so that $(u,v)=(0,0)$ corresponds to $(x_0, y_0)$

> Notice changing variables is not going to affect our differential equations because $x_0$ and $y_0$ are constant.
> $$\begin{align}
> \frac{dx}{dt} &= \frac{du}{dt} \\
> \frac{dy}{dt} &= \frac{dv}{dt}
> \end{align}$$



The *linearization* as the linear system
$$
\begin{bmatrix}
u \\
v
\end{bmatrix}'
=
\begin{bmatrix}
\frac{\partial f}{\partial x}(x_0,y_0) & \frac{\partial f}{\partial y}(x_0,y_0) \\
\frac{\partial g}{\partial x}(x_0,y_0) & \frac{\partial g}{\partial y}(x_0,y_0)
\end{bmatrix}
\begin{bmatrix}
u \\
v
\end{bmatrix}
$$

> **Jacobian matrix**:  derivative matrix



#### Conservative equations

An equation of the form
$$
x^{''} + f(x)=0
$$
for an arbitrary function $f(x)$ is called a **conservative equation**

> The equations are conservative as there is no friction in the system so the energy in the system is "conserved".



Let us write this equation as a system of nonlinear ODE
$$
x' = y, \quad y' = -f(x)
$$



Assume that we have an *autonomous system* of differential equations defining $x$ and $y$,
$$
x' = f(x,y), \quad y' = g(x,y)
$$
A **trajectory** for this system is a curve in the $xy$-plane that the solution curve $(x(t); y(t))$ will *stay on* for **all** $t$.

> This curve will generally be given with 
>
> - $y$ as a function of $x$, 
> - or the level curve of some function $F(x; y)$.



#### Hamiltonian Systems

A generalization of *conservative equations* to systems is a **Hamiltonian system**.

For these systems, the point is that the equation has a *conserved quantity* called a **Hamiltonian**, which *does not change as the system evolves in time*, which generally represents the *energy of the system*. Calling this function $H(x; y)$, this means that
$$
\frac{d}{dt}H(x,y) = 0
$$
Below give the definition of  **Hamiltonian system**:

> The system 
> $$\begin{align}
> \frac{dx}{dt} &= f(x,y) \\
> \frac{dy}{dt} &= g(x, y)
> \end{align}$$
>
> is **Hamiltonian** if there is a function $H(x,y)$ so that
> $$\begin{align}
> f(x,y) &=-\frac{\partial H}{\partial y} \\
> g(x,y) &= \frac{\partial H}{\partial x}
> \end{align}$$



#### Limit cycles

unforced nonlinear time-invariant differential systems of the form
$$
\frac{d\mathbf{x}}{dt}=\mathbf{f(x)}
$$


For nonlinear systems, trajectories do not simply need to approach or leave a single point. They may in fact approach a larger set, such as a *circle* or *another closed curve*.

##### Poincaré–Bendixson Theorem



#### Floquet Theory

When a small perturbation $\mathbf{\delta}(t)$ is applied to a periodic orbit $\mathbf{x}_c(t)$ so that the oscillator position is
$$
\mathbf{x}(t)=\mathbf{x}_c(t)+\mathbf{\delta}(t)
$$
by performing a Taylor series expansion in the vicinity of $\mathbf{x}_c(t)$, we obtain

$$\begin{align}
\frac{d}{dt}(\mathbf{x}_c(t)+\mathbf{\delta}(t)) &= \mathbf{f}(\mathbf{x}_c(t)+\mathbf{\delta}(t)) \\
&= \mathbf{f}(\mathbf{x}_c(t)) + \mathbf{A}(t)\mathbf{\delta}(t) + O(||\mathbf{\delta}(t)||^2)
\end{align}$$

where
$$
\mathbf{A}(t) = \mathbf{J}(\mathbf{x}_c(t))
$$
denotes the vector field Jacobian evaluted along the periodic orbit $\mathbf{x}_c(t)$

This indicates that small trajectory perturbations satisfy the linear differential equation
$$
\frac{d\mathbf{\delta}}{dt} = \mathbf{A}(t)\mathbf{\delta}(t)
$$

> where $\mathbf{A}(t)$ is periodic with period $T$ since $\mathbf{x}_c(t)$ is periodic with the same period

Since $\mathbf{x}_c(t)$ solves the differential equation, by differentiating
$$
\frac{d\mathbf{x}_c(t)}{dt} =\mathbf{f}(\mathbf{x}_c(t)
$$
we obtain
$$
\frac{d}{dt}\left(\frac{d\mathbf{x}_c(t)}{dt}\right) =\frac{d\mathbf{f}}{d\mathbf{x}_c}\frac{d\mathbf{x}_c(t)}{dt}
$$
and denoting $\mathbf{v}(t)=d\mathbf{x}_c/dt$, then
$$
\frac{d\mathbf{v}}{dt} = \mathbf{A}(t)\mathbf{v}(t)
$$
where the velocity vector $\mathbf{v}(t)$ is periodic with period $T$ and is tangent to orbit $C$ at point $\mathbf{x}_c(t)$

> **SPECIAL CASE:**
>
> If  the initial perturbation $\mathbf{\delta}(0)$ is colinear with vector $\mathbf{v}(0)$, i.e., $\mathbf{\delta}(0) = \alpha \mathbf{v}(0)$, then
> $$
> \mathbf{\delta}(t) = \alpha \mathbf{v}(t)
> $$
> for all $t$, so that in this case $\mathbf{\delta}(t)$ **remain** colinear with $\mathbf{v}(t)$ and is periodic with period $T$



Since the oscillator orbit we consider is stable, small perturbations in **directions other than the tangent to the trajectory** must **disappear** as $t$ becomes large.

i.e., if $\mathbf{\delta}(0)$ has no component along the $\mathbf{v}(0)$ direction, we must have
$$
\lim_{t\to \infty}\mathbf{\delta}(t) = 0
$$




#### Chaos

Achaotic system is extremely sensitive to initial conditions. 

A small change in the initial conditions yields a very different solution after a reasonably short time



### Riemann integral

*standard* (Riemann) integral
$$
\int_0^T f(t)dt = \lim_{N\to\infty}\sum_{k=0}^{N-1}f(\tilde{t_k})\Delta t_k,\quad\Delta t_k=t_{k+1}-t_k
$$
where the width of each interval is $T/N$, and for each interval $\Delta t_k$, we choose a value $\tilde{t_k}\in[t_k,t_{k+1}]$ at which we evaluate the function.

![The Riemann integral construction; divide the function up into rectangles. Here, I’ve evaluated the function at the left edge of each rectangle.](math-and-noise/riemann_int.png)

The Riemann integral construction; divide the function up into rectangles. Here, I’ve evaluated the function at the *left edge* of each rectangle.

> For *ordinary, smooth functions*, of course, this integral converges to the same value *no matter* where we choose our rectangle heights $\tilde{t_k}$ in the interval. 
>
> 
>
> However, Brownian motion is *less well behaved*.



### Lebesgue integral

[[What is the difference between a Riemann and a Lebesgue integral, and why is the latter needed?](https://qr.ae/py5x6K)]

Riemann integration:

![image-20230702004840807](math-and-noise/image-20230702004840807.png)

> The disadvantage of the Riemann integral is that it privileges the role of intervals. It is ineffective when applied to a highly discontinuous function 



Lebesgue integration:

![image-20230702005049938](math-and-noise/image-20230702005049938.png)


### Measure and Probabilities

> Probality is a measure of the size of a set

####  power set 

#### $\sigma$-Algebra

or $\sigma$-field, Sigma-field

#### measurable space

If $X$ is a set and $A$  is a $\sigma$-algebra on $X$, then the tuple $(X,A)$ is called the **measurable space** (also **Borel space**)

#### probability space

#### filtration and information flow

#### martingale

A stochastic process $M_t$ is a **martingale** if 

- its *mean* is bounded

- and *the conditional expectation given access to it’s history up to time* $t'$ is equal to the value at that time

that is
$$\begin{align}
\mathbb{E}[|M_t|] &\lt \infty \\
\mathbb{E}[M_t|{M_s,s\leq t'}] &= M_{t'}, \quad \text{for all } t'\leq t
\end{align}$$



> In less formal language, this means that the “best guess" for the future value of a martingale is always the most recent observed value; knowing $M_{t'}$ is just as good as knowing the entire history of $M_t$ up to $t'$
>
> If $W_t$ is your wealth at the $t^{th}$ round of a fair game, like betting on a coin flip, then $W_t$ is a martingale; on average you end up with the same amount of money you started with.






##### WSS process

 A random process $X(t)$ is **wide-sense stationary** if:

1. $\mu _x(t)=\text{constant}$, for all $t$, and
2. $R_X(t_1, t_2)=R_x(t_1-t_2)$ for all $t_1, t_2$



#### Wiener Process (or Brownian Motioan)

> $\text{SDE} = \text{ODE} + \text{GWN}$
>
> where $\text{GWN}$ is **Gaussian White Noise**



a Brownian Motion $\{W_t\}_{t:t\in[0,\infty]}$ is a stochastic process, whose conditional likelihood is Gaussian with a variance that increase linearly in the time interval that one considers and a zero mean

- $W_0 = 0$
- $W_t \sim \mathbb{N}(0, t)$ 
- $W_{t2} - W_{t1}$ is independent from $W_{t4} - W_{t3}$ for $0\leq t_1\leq t_2 \leq t_3 \leq t_4$



> Brownian motion $W_t$ is an example of a **Gaussian process**
>
> Wiener process can be thought of as the **integral** of white noise



The implications of these assumptions are:
$$
E[W_t] = 0
$$

$$
Var(W_t) = E[W_t^2] = t
$$



- A single trajectory $t \to W_t(\omega)$ is **continuous**, yet extremely spiky, that is $\frac{dW_t}{dt}$ **does not** exist.

- Yet, the Brownian Motion itself is well defined of course. that is $W_t = \int_0^tdW_u$ **does** exist

$$
W_t = \int_0^tdW_u
$$



What does it really mean?

- $dW_t \sim \mathbb{N}(0, dt)$
- $\frac{dW_t}{dt}\sim \mathbb{N}(0,1)$



![image-20230702094054155](math-and-noise/image-20230702094054155.png)



#### Ito SDE with Brownian Motion

$$
\frac{dX_t}{dt} = f(X_t) + g(X_t)\frac{dW_t}{dt}
$$

is not well defined and hence only a popular *'Symbolic Representation'*

For SDEs, the proper representation is the **'Pathwise Stochastic Integral Representation'**

![image-20230702155217093](math-and-noise/image-20230702155217093.png)

> **stochastic integral**:
>
> It doesn’t have the same geometrically intuitive nature as the Riemann integral, but there is an analogy here; 
>
> instead of a finite sum of simple functions which are rectangles, we are now dealing with **a finite sum of 'simple random variables' multiplied by increments of a Brownian walk**, which are Gaussian.





### stochastic differential equation (SDE)

#### Wiener Stochastic Integral

Let $L^2([0,T])$ denote the space of measurable functions $f:[0,T]\longrightarrow \mathbb{R}$ such that
$$
||f||_{L^2([0,T])}=\sqrt{\int_0^T|f(t|^2dt}\lt \infty
$$
In the above definition, $||f||_{L^2([0,T])}$ represents the norm of the function $f\in L^2([0,T])$, and known as *square-integrable functions*



$\int_0^Tf(t)dB_t$ has the centered Gaussian distribution
$$
\int_0^Tf(t)dB_t \simeq \mathbb{N}\left(0,\int_0^T|f(t)|^2dt\right)
$$
where $f\in L^2([0,T])$



The Wiener stochastic integral $\int_0^T f(t)dB_t$ is a Gaussian random variable that cannot be "computed" in the way standard integrals are computed via the use of primitives. However, when $f\in L^2([0,T])$ and is continuously differentiable on $[0,T]$, we have the integration by parts relation
$$
\int_0^Tf(t)dB_t = f(T)B_T -\int_0^TB_tf'(t)dt
$$

#### Ito Stochastic Integral

The biggest advantage of Ito formulation is that the evaluations of the function are totally uncorrelated with the increment, by contruction.

That is to say, that because we evaluate the function $f(x,B_t, t)$ at the **left** point of the midpoint, our limiting sum is
$$
\int f(x,B_t, t)dB_t = \lim_{N\to \infty}\sum f(x_{t_k},B_{t_k},t_k)(B_{t_{k+1}}-B_{t_k})
$$

> For a deterministic integral, the convergence of the integral does **NOT** depend on wheter the integrands is evaluated at the left, mid or end point.
>
> The Ito stochastic integral uses the left end point for the integrand.



But because the increment $(B_{t_{k+1}}-B_{t_k})$ is **uncorrelated** with $B_{t_k}$, it's also **uncorrelated with any function of $B_{t_k}$**, i.e.  $f(x_{t_k},B_{t_k},t_k)$. and the limiting sum always has **mean zero **

This leads to the nice property that an Ito integral
$$
\int _S ^ T f(x, t)dB_t
$$
always has mean zero, and is a martingale

> $f(x, t)$ omit $B_t$ due to uncorrelated property





##### quadratic variation



Step function approximation of Brownian motion



$$\begin{align}
E\left[\left( \int_0^Tu_t dB_t \right)^2\right] &= E\left[\int_0^T |u_t|^2 dt \right] \\
E\left[\int_0^T u_t dB_t\right] &= 0
\end{align}$$



##### Basic Ito formula

For $f$ is twice continuously differentiable on $[0, T]$, Taylor's formula written at the second order for Brownian motion reads
$$
df(B_t) = f'(B_t)dB_t + \frac{1}{2}f^{''}(B_t)dt
$$
for **infinitesimally small** $dt$.



Note that writing this formula as
$$
\frac{df(B_t)}{dt}=f'(B_t)\frac{dB_t}{dt}+\frac{1}{2}f^{''}(B_t)
$$
**does not** make sense because the pathwise derivative
$$
\frac{dB_t}{dt}\simeq \pm\frac{\sqrt{dt}}{dt}\simeq \pm\frac{1}{\sqrt{dt}}\simeq \pm\infty
$$
of $B_t$ with respect to $t$ does not exist.



With $f(B_t)-f(B_0)=\int_0^t df(B_s)$, we get the integral form of Ito formula for Brownian motion
$$
f(B_t) = f(B_0)+\int_0^tf'(B_s)dB_s+\frac{1}{2}\int_0^tf^{''}(B_s)ds
$$

##### Ito processes

A stochastic process $(X_t)_{t\in \mathbb{R}_+}$ that can be written as
$$
X_t = X_0 + \int_0^t v_sds + \int_0^t u_sdB_s,\quad t\geq0
$$
or differential notation
$$
dX_t = v_tdt + u_tdB_t
$$
where $(u_t)_{t\in\mathbb{R}_+}$ and $(v_t)_{t\in\mathbb{R}_+}$ are *square-integrable adapted process*



##### Ito formula for Ito processes

For any Ito process $(X_t)_{t\in\mathbb{R}_+}$ and any $f$ that is continuously differentiable on $t\in[0,T]$ and twice differentiable in $x\in\mathbb{R}$, with bounded derivatives
$$
f(t,X_t) = f(0,X_0)+\int_0^t\frac{\partial f}{\partial s}(s,X_s)ds + \int_0^t v_s\frac{\partial f}{\partial x}(s,X_s)ds + \int_0^t u_s\frac{\partial f}{\partial x}(s,X_s)dB_s+\frac{1}{2}\int_0^t|u_s|^2\frac{\partial ^2 f}{\partial x^2}(s,X_s)ds
$$
Due to $\int_0^t df(s,X_s)=f(t,X_t)-f(0,X_0)$
$$
\int_0^t df(s,X_s)=\int_0^t\frac{\partial f}{\partial s}(s,X_s)ds + \int_0^t v_s\frac{\partial f}{\partial x}(s,X_s)ds + \int_0^t u_s\frac{\partial f}{\partial x}(s,X_s)dB_s+\frac{1}{2}\int_0^t|u_s|^2\frac{\partial ^2 f}{\partial x^2}(s,X_s)ds
$$
which allow us to rewrite in differential notation, as
$$
df(t,X_t) = \frac{\partial f}{\partial t}(t,X_t)dt + v_t\frac{\partial f}{\partial x}(t, X_t)dt+u_t\frac{\partial f}{\partial x}(t,X_t)dB_t+\frac{1}{2}|u_t|^2\frac{\partial ^2 f}{\partial x^2}(t, X_t)dt
$$


- In case the function $x \to f(x)$ does **not depend on the time variable $t$**, we get
  $$
  df(X_t) = v_t\frac{\partial f}{\partial x}(X_t)dt+u_t\frac{\partial f}{\partial x}(X_t)dB_t+\frac{1}{2}|u_t|^2\frac{\partial ^2 f}{\partial x^2}(X_t)dt
  $$

- $X_t = B_t$ while taking $v_t=0$, $u_t=1$ and $X_0=0$ in Ito process, Ito formula reads
  $$
  f(t, B_t) = f(0, B_0)+\int_0^t\frac{\partial f}{\partial s}(s,B_s)ds + \int_0^t\frac{\partial f}{\partial x}(s,B_s)dB_s+\frac{1}{2}\int_0^t\frac{\partial ^2 f}{\partial x^2}(s,B_s)ds
  $$
  i.e. in differential notation:
  $$
  df(t, B_t) = \frac{\partial f}{\partial t}(t,B_t)dt + \frac{\partial f}{\partial x}(t,B_t)dB_t+\frac{1}{2}\frac{\partial ^2 f}{\partial x^2}(t,B_t)dt
  $$

---

**Ito Lemma**, it says that if the input to a function follows an Ito SDE, then the output to a sufficiently smooth function follows also an Ito SDE.

![image-20230702160220762](math-and-noise/image-20230702160220762.png)

---



##### Bivariate Ito formula

Consider two Ito processes $(X_t)_{t\in \mathbb{R} _+}$ and $(Y_t)_{t\in \mathbb{R} _+}$ written in *integral form* as

$$\begin{align}
X_t &= X_0 + \int_0^t v_sds + \int_0^t u_s dB_s, \quad t \geq 0 \\
Y_t &= Y_0 + \int_0^t b_sds + \int_0^t a_s dB_s, \quad t \geq 0
\end{align}$$

or in *differential notation* as

$$\begin{align}
dX_t &= v_t dt +u_tdB_t \\
dY_t &= b_tdt + a_tdB_t
\end{align}$$



The Ito  formula can also be written for functions $f$ of two state variables as

$$\begin{align}
df(t,X_t, Y_t) &= \frac{\partial f}{\partial t}(t,X_t,Y_t)dt + \frac{\partial f}{\partial x}(t, X_t, Y_t)dX_t + \frac{1}{2}|u_t|^2\frac{\partial ^2 f}{\partial x^2}(t, X_t, Y_t)dt \\
&+\frac{\partial f}{\partial y}(t, X_t, Y_t)d_t + \frac{1}{2}|a_t|^2\frac{\partial ^2 f}{\partial y^2}(t, X_t, Y_t)dt + u_ta_t\frac{\partial ^2 f}{\partial x \partial y}(t,X_t,Y_t)dt
\end{align}$$

##### Ito multiplication table

| $\cdot$ | $dt$ | $dB_t$ |
| ------- | ---- | ------ |
| $dt$    | $0$  | $0$    |
| $dB_t$  | $0$  | $dt$   |

That is

$$\begin{align}
dt\cdot dt &= 0 \\
dt\cdot dB_t &= 0 \\
dB_t \cdot dB_t &= dt
\end{align}$$

It follows from above Ito table that

$$\begin{align}
dX_t \cdot dY_t &= (v_tdt+u_tdB_t)\cdot (b_tdt + a_tdB_t) \\
&= b_tv_t(dt)^2+b_tu_tdtdB_t +a_tv_tdtdB_t +a_tu_t(dB_t)^2 \\
&= a_tu_t dt
\end{align}$$

and we also have
$$\begin{align}
(dX_t)^2 &= (v_tdt + u_tdB_t)^2 \\
&= (v_t)^2 (dt)^2 + (u_t)^2(dB_t)^2 + 2u_tv_t(dt\cdot dB_t) \\
&= (u_t)^2dt
\end{align}$$

> $dB_t = \sqrt{dt}$



##### Ito formula using Ito multiplication table

with $(u_t)^2dt=(dX_t)^2$ and $X_t = v_tdt + u_tdB_t$, Ito formula's differential notation can be rewritten as 
$$\begin{align}
df(t,X_t) &= \frac{\partial f}{\partial t}(t,X_t)dt + v_t\frac{\partial f}{\partial x}(t, X_t)dt+u_t\frac{\partial f}{\partial x}(t,X_t)dB_t+\frac{1}{2}|u_t|^2\frac{\partial ^2 f}{\partial x^2}(t, X_t)dt \\
&= \frac{\partial f}{\partial t}(t,X_t)dt + \frac{\partial f}{\partial x}(t,X_t)\cdot (v_tdt + u_tdB_t) + \frac{1}{2}\frac{\partial ^2 f}{\partial x^2}(t, X_t)\cdot |u_t|^2dt \\
&= \frac{\partial f}{\partial t}(t,X_t)dt + \frac{\partial f}{\partial x}(t,X_t)dX_t + \frac{1}{2}\frac{\partial ^2 f}{\partial x^2}(t, X_t)\cdot (dX_t)^2 \\
& = \frac{\partial f}{\partial t}(t,X_t)dt + \frac{\partial f}{\partial x}(t,X_t)dX_t + \frac{1}{2}\frac{\partial ^2 f}{\partial x^2}(t, X_t)dX_t\cdot dX_t
\end{align}$$



and the Ito formula for function $f$ of two state variables can be rewritten as

$$\begin{align}
df(t,X_t, Y_t) 
&= \frac{\partial f}{\partial t}(t,X_t,Y_t)dt + \frac{\partial f}{\partial x}(t, X_t, Y_t)dX_t + \frac{1}{2}\frac{\partial ^2 f}{\partial x^2}(t, X_t, Y_t)(dX_t))^2 \\
&+\frac{\partial f}{\partial y}(t, X_t, Y_t)d_t + \frac{1}{2}\frac{\partial ^2 f}{\partial y^2}(t, X_t, Y_t)(dY_t)^2 + \frac{\partial ^2 f}{\partial x \partial y}(t,X_t,Y_t)(dX_t\cdot dY_t) 
\end{align}$$

where $(dX_t)^2 = |u_t|^2dt$, $(dY_t)^2=|a_t|^2dt$ and $dX_t\cdot dY_t = u_ta_tdt$



### Solving a Geometric Brownian Motion

#### Geometric Brownian motion (GBM)

A **geometric Brownian motion (GBM)** (also known as **exponential Brownian motion**)

A stochastic process $S_t$ is said to follow a **GBM** if it satisfies the following (SDE) [[link](https://en.wikipedia.org/w/index.php?title=Geometric_Brownian_motion&oldid=1161374200)]:
$$
dS_t = \mu S_t dt + \sigma S_t dW_t
$$
where $W_t$ is a Wiener process or Brownian motion

and $\mu$ ('the percentage drift') and $\sigma$ ('the percentage volatility') are constants. 

> The former parameter is used to model deterministic trends, 
>
> while the latter parameter models unpredictable events occurring during the motion.



#### solving step by step

[[Quant Guild](https://youtu.be/y0s2GXREymI)]

Given the stochastic differential equation
$$
dS_t = \mu S_t dt + \sigma S_t dW_t, \quad t\in[t_0, T]
$$
that represents the dynamics of a stock process, it is desirable to recover the function for simulation.

First, recall **Ito lemma** where $y(t, X_t)$ represents a time-dependent function of  a stochastic process
$$
dy(t,X_t) = \frac{\partial y}{\partial t}dt + \frac{\partial y}{\partial X_t}dX_t + \frac{1}{2}\frac{\partial ^2 y}{\partial X_t^2}(dX_t)^2
$$
Now, consider the following log transformation of the stock process
$$
g(S_t) = \ln(S_t)
$$
We can apply Ito lemma to the log transformation function
$$
dg(S_t) = \frac{\partial g}{\partial t}dt + \frac{\partial g}{\partial S_t}dS_t +\frac{1}{2}\frac{\partial ^2 g}{\partial X_t^2}(dX_t)^2
$$
It follows from $g(S_t) = \ln(S_t)$ and $dS_t = \mu S_t dt + \sigma S_t dW_t$ with *Ito multiplication table*
$$\begin{align}
\frac{\partial g}{\partial t} &= 0 \\
\frac{\partial g}{\partial S_t} &= \frac{1}{S_t} \\
\frac{\partial ^2  g}{\partial S_t ^2} &= -\frac{1}{S_t^2} \\
(dX_t)^2 &= 0 + 0 + \sigma^2S_t^2(dW_t)^2 = \sigma^2S_t^2dt
\end{align}$$



By substitution of these results into $dg(S_t) = \frac{\partial g}{\partial t}dt + \frac{\partial g}{\partial S_t}dS_t +\frac{1}{2}\frac{\partial ^2 y}{\partial X_t^2}(dX_t)^2$, we obtain
$$\begin{align}
dg(S_t) &= 0 + \frac{1}{S_t}(\mu S_t dt + \sigma S_t dW_t) + \frac{1}{2}(-\frac{1}{S_t^2})\sigma^2S_t^2dt \\
&= \mu dt + \sigma dW_t - \frac{1}{2}\sigma^2 dt \\
&= \left(\mu - \frac{1}{2}\sigma^2\right) + \sigma dW_t
\end{align}$$

We can now integrate both sides
$$
\int_{t_0}^Tdg(S_t) = \int_{t_0}^T \left(\mu - \frac{1}{2}\sigma^2\right)dt + \int_{t_0}^T\sigma dW_t
$$

$$
g(S_t) - g(S_{t_0}) = \left(\mu - \frac{1}{2}\sigma^2\right)(T - {t_0}) + \sigma(W_T - W_{t_0})
$$

Let's substitute $g(S_t) = \ln(S_t)$ into above equation
$$
\ln(S_t) - \ln(S_{t_0}) = \left(\mu - \frac{1}{2}\sigma^2\right)(T - {t_0}) + \sigma(W_T - W_{t_0})
$$
after arranging, the closed form solution is
$$
S_T = S_{t_0}e^{(\mu-\frac{1}{2}\sigma^2)(T-t_0)+\sigma(W_T-W_{t_0})}
$$


## reference

### paper

A. Demir, A. Mehrotra and J. Roychowdhury, "Phase noise in oscillators: a unifying theory and numerical methods for characterization," in IEEE Transactions on Circuits and Systems I: Fundamental Theory and Applications, vol. 47, no. 5, pp. 655-674, May 2000, doi: 10.1109/81.847872. [[pdf](https://www.researchgate.net/profile/Jaijeet-Roychowdhury/publication/3774912_Phase_noise_in_oscillators_a_unifying_theory_and_numerical_methods_for_characterisation/links/56436c0308ae54697fb2e543/Phase-noise-in-oscillators-a-unifying-theory-and-numerical-methods-for-characterisation.pdf)]

demir, Alper. (2000). Floquet theory and non-linear perturbation analysis for oscillators with differential-algebraic equations. International Journal of Circuit Theory and Applications - INT J CIRCUIT THEOR APPL. 28. 163-185. 10.1002/(SICI)1097-007X(200003/04)28:23.0.CO;2-K. 



### book

&#11088; Levy, Bernard. (2020). **Random Processes with Applications to Circuits and Communications**. 10.1007/978-3-030-22297-0. 

Sundararajan, D.. (2023). **Signals and Systems: A Practical Approach**. 10.1007/978-3-031-19377-4. 

Øksendal, Bernt. (2000). **Stochastic Differential Equations: An Introduction with Applications**. 10.1007/978-3-662-03185-8. 

Chicone, Carmen Charles. **Ordinary Differential Equations with Applications. 2nd ed**. New York ; Berlin: Springer, 2006. 

&#11088; Stanley H. Chan (2021). **Introduction to Probability for Data Science**. Michigan Publishing, [[link](https://probability4datascience.com/index.html)]

Simo Särkkä and Arno Solin (2019). **Applied Stochastic Differential Equations**. Cambridge University Press. Cambridge, UK. [[link](https://github.com/AaltoML/SDE)]

Gerald Teschl, **Ordinary Differential Equations and Dynamical Systems** A.M.S., 2012

Kurt Bryan; Brian Winkel (2020), "2021-Bryan, Kurt - SIMIODE Online Digital Textbook - **Differential Equations: A Toolbox for Modeling the World**.," https://www.simiode.org/resources/8208.

Jordan, D.W. and Smith, P. (2007) **Nonlinear Ordinary Differential Equations: An Introduction for Scientists and Engineers. 4th Edition**, Oxford University Press, New York.

Strogatz, S.H. (2015). **Nonlinear Dynamics and Chaos: With Applications to Physics, Biology, Chemistry, and Engineering (2nd ed.)**. CRC Press. https://doi.org/10.1201/9780429492563

&#11088; Nicolas Privault. **Introduction to Stochastic Finance with Market Examples, Second Edition**, Chapman & Hall/CRC Financial Mathematics Series, 2022

&#11088; Nicolas Privault. **MH4514 Financial Mathematics** [[link](https://personal.ntu.edu.sg/nprivault/indext.html), [MH4514_notes](https://drive.google.com/file/d/1iCsMdtJctWK2fo65WP5iqNvQ73acObzU)]

Evans, Lawrence C.. **Stochastic differential equations version 1.2** [[pdf](https://www.cmor-faculty.rice.edu/~cox/stoch/SDE.course.pdf)]

Evans, Lawrence C.. **An Introduction to Stochastic Differential Equations.** (2014).

&#11088; Matt Charnley. **Differential Equations: An Introduction for Engineers** [[link](https://sites.rutgers.edu/matthew-charnley/course-materials/differential-equations-an-introduction-for-engineers/)]

&#11088; Jiří Lebl. **Notes on Diffy Qs: Differential Equations for Engineers** [[link](https://www.jirka.org/diffyqs/)]



### measure-theoretic probability theory

Jacod, J., & Protter, P. (2004). **Probability Essentials (Second edition.)**. Springer Berlin Heidelberg.

Sebastien Roch, UW-Madison. **Lecture Notes on Measure-theoretic Probability Theory** [[link](https://people.math.wisc.edu/~roch/grad-prob/index.html)]

Matthew N. Bernstein **Demystifying measure-theoretic probability theory** [[part1](https://mbernste.github.io/posts/self_info/), [part2](https://mbernste.github.io/posts/measure_theory_2/), [part3](https://mbernste.github.io/posts/measure_theory_3/)]

Edwin Chen. **Layman's Introduction to Measure Theory** [[link](https://blog.echen.me/2011/03/14/laymans-introduction-to-measure-theory/)]

Ales Cerný. **Mathematical Techniques in Finance: Tools for Incomplete Markets - Second Edition**



### blogs

&#11088; Prof. Dr. Maxim Ulrich, KIT. **Stochastic Calculus: Basics** [[link](https://youtube.com/playlist?list=PLyQSjcv8LwAEdNgdVnNH02-JTJfrwCt81)]

&#11088; Lewis Smith. **Itô and Stratonovich; a guide for the perplexed** [[link](https://www.robots.ox.ac.uk/~lsgs/posts/2018-09-30-ito-strat.html)]

布朗运动、伊藤引理、BS 公式（前篇） [[link](https://zhuanlan.zhihu.com/p/38293827)]


Wiener Process $dB^2=dt$ [[https://math.stackexchange.com/q/81865/1059887](https://math.stackexchange.com/q/81865/1059887)]

Professor Steve Lalley Statistics 385: Brownian Motion and Stochastic Calculus Fall 2016 [[link](https://galton.uchicago.edu/~lalley/Courses/385/)]

18.S096 | Fall 2013 | Undergraduate MIT. Topics In Mathematics With Applications In Finance [[link](https://ocw.mit.edu/courses/18-s096-topics-in-mathematics-with-applications-in-finance-fall-2013/pages/syllabus/)]

Mathuranathan, Power and Energy of a Signal : Demystified URL: [https://www.gaussianwaves.com/2013/12/power-and-energy-of-a-signal/](https://www.gaussianwaves.com/2013/12/power-and-energy-of-a-signal/)

White Noise : Simulation and Analysis using Matlab gaussianwaves.com [[link](https://www.gaussianwaves.com/2013/11/simulation-and-analysis-of-white-noise-in-matlab/)]

Prof. J. Nathan Kutz AMATH 568 Advanced Differential Equations: Asymptotics & Perturbations [[link](https://faculty.washington.edu/kutz/am568/am568.html)]

Asymptotics and perturbation methods - Prof. Steven Strogatz [[link](https://youtube.com/playlist?list=PL5EH0ZJ7V0jV7kMYvPcZ7F9oaf_YAlfbI)] via @YouTube 

Simo Särkkä and Arno Solin (2014). **Applied Stochastic Differential Equations**. *Lecture notes of the course Becs-114.4202 Special Course in Computational Engineering II held in Autumn 2014*. ([Booklet as PDF](https://users.aalto.fi/~ssarkka/course_s2014/sde_course_booklet.pdf), [Slides and exercises](https://users.aalto.fi/~ssarkka/course_s2014/)). (2012 material is [here](https://users.aalto.fi/~ssarkka/course_s2012/pdf/)).

Ben Chugg. Itô Integral: Construction and Basic Properties [[link](https://benchugg.com/research_notes/intro_ito/)]

Ben Chugg. Itô Processes and The Fundamental Theorem of Stochastic Calculus [[link](https://benchugg.com/research_notes/sde_ito_lemma/)]
