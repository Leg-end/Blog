---
title: Stochastic Calculus
published: 2024-03-08
description: "Introduction to Stochastic Calculus"
tags: ["Stochastic"]
category: Top-Design
draft: false
---

**Problem & Analysis**  
What is stochastic calculus ? And What problems it can apply ?
First let's start from our familiar standard calculus, i.e. [==Riemannian integral==](https://en.wikipedia.org/wiki/Riemann_integral), but do it more precisely
  $$I=\underset{0}{\overset{T}{\int}}tdt=\underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}{\sum}_{j=0}^{n-1}{s}_{j}\left({t}_{j+1}-{t}_{j}\right)=\underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}{\sum}_{j=0}^{n-1}{A}_{j},$$
  $$where\ \mathit{\Pi}=\left\{{t}_{0},{t}_{1},\dots ,{t}_{n}\right\},0\le {t}_{0}\le \dots \le {t}_{n}=T,\Vert \mathit{\Pi}\Vert =\underset{j=0,\dots ,n-1}{\mathrm{max}}\left({t}_{j+1}-{t}_{j}\right)$$
When ${s}_{j}={t}_{j}$
  $${A}_{j}={t}_{j}{t}_{j+1}-{t}_{j}^{2}+\frac{1}{2}{t}_{j+1}^{2}-\frac{1}{2}{t}_{j+1}^{2} \\ =\frac{1}{2}\left({t}_{j+1}^{2}-{t}_{j}^{2}\right)-\frac{1}{2}{\left({t}_{j+1}-{t}_{j}\right)}^{2}$$
$$\Rightarrow I=\frac{1}{2}\left({t}_{n}^{2}-{t}_{0}^{2}\right)-\frac{1}{2}{\sum}_{j=0}^{n-1}{\left({t}_{j+1}-{t}_{j}\right)}^{2} \\ =\frac{1}{2}{T}^{2}-\frac{1}{2}{\sum}_{j=0}^{n-1}{\left({t}_{j+1}-{t}_{j}\right)}^{2}$$
When ${s}_{j}=\frac{{t}_{j}+{t}_{j+1}}{2}$
  $${A}_{j}=\frac{{t}_{j+1}^{2}}{2}+\frac{{t}_{j+1}{t}_{j}}{2}-\frac{{t}_{j+1}{t}_{j}}{2}-\frac{{t}_{j}^{2}}{2}-\frac{{t}_{j+1}{t}_{j}}{2}+\frac{{t}_{j+1}{t}_{j}}{2}+\frac{{t}_{j}^{2}}{2}-\frac{{t}_{j}^{2}}{2} \\ ={t}_{j}{t}_{j+1}-{t}_{j}^{2}+\frac{1}{2}{\sum}_{j=0}^{n-1}{\left({t}_{j+1}-{t}_{j}\right)}^{2}$$
  We know that
    $${t}_{j}{t}_{j+1}-{t}_{j}^{2}=\frac{1}{2}{T}^{2}-\frac{1}{2}{\sum}_{j=0}^{n-1}{\left({t}_{j+1}-{t}_{j}\right)}^{2}$$
  $$\Rightarrow I=\frac{1}{2}{T}^{2}$$
And that's exactly matches the rules of Riemannian integral, except we need to prove that the **Quadratic variation** is 0
  $$\underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}{\sum}_{j=0}^{n-1}{\left({t}_{j+1}-{t}_{j}\right)}^{2}=0$$
Now that's extent it to a general case where integrant and integrator are all $f\left(t\right)$, a derivable function
  $$I=\underset{0}{\overset{T}{\int}}f\left(t\right)df\left(t\right)$$
And we can have same form of Quadratic variation
  $$\underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}{\sum}_{j=0}^{n-1}{\left(f\left({t}_{j+1}\right)-f\left({t}_{j}\right)\right)}^{2}$$
$$=\underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}{\sum}_{j=0}^{n-1}{\left({t}_{j+1}-{t}_{j}\right)}^{2}{\left[{f}^{\prime}\left({t}_{j}^{\ast}\right)\right]}^{2},\ \ mean\ value\ theorem$$
$$\le \underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}\Vert \mathrm{\Pi}\Vert \underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}{\sum}_{j=0}^{n-1}\left({t}_{j+1}-{t}_{j}\right){\left[{f}^{\prime}\left({t}_{j}^{\ast}\right)\right]}^{2}$$
$$=\underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}\Vert \mathrm{\Pi}\Vert \cdot \underset{0}{\overset{T}{\int}}{\left[{f}^{\prime}\left({t}_{j}^{\ast}\right)\right]}^{2}dt=0$$
So in case of derivable integrator, we can just use the standard rules of calculus that we all know and love. But what happen if the integrator is not derivable.
The rules of Riemannian integral will collide on different integrant, that is
  $${I}_{{s}_{j}={t}_{j}}\ne {I}_{{s}_{j}=\frac{{t}_{j+1}+{t}_{j}}{2}},\ \ \ \underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}{\sum}_{j=0}^{n-1}{\left(f\left({t}_{j+1}\right)-f\left({t}_{j}\right)\right)}^{2}\ne 0$$
That's when stochastic calculus come in handy to deal with function that continuous everywhere but derivable nowhere, e.g. [*Weierstrass function*](https://en.wikipedia.org/wiki/Weierstrass_function) or Wiener process $W\left(t\right)$
So informal way stochastic calculus can be seen as calculus over stochastic process, which is collection of random variables(a function over sample space) indexed by continuous time.
  $$G\left(t\right)=\underset{0}{\overset{t}{\int}}H\left(s\right)dX\left(s\right)$$
  Where $H\left(s\right),X\left(s\right)$ are two special types of stochastic process, so is $G\left(t\right)$
The slight differences to Riemannian integral is how to deal with integrator of stochastic process, which is indeterministic and so its underivable.
Why it's underivable w.r.t time ?
  For an derivable function $f\left(t\right)$ , we can describe its variation over infinitesimal time interval by
  $$df\left(t\right)=f^{'}\left(t\right)dt\ or\ f\left(t\right)=f\left({t}_{0}\right)+f^{'}\left(t\right)dt$$
  It means the increment, or path, between infinitesimal time interval is deterministic, but which is not true for a stochastic process, since the variation over infinitesimal time is randomly distributed
  So without existence of deterministic description for variation, nor stochastic process is derivable
  Further, such property, later we’ll see, is inherited from symmetric random walk
Underivable stochastic process leads to non-zero quadratic variation, which results in divergent integral limits due to different integrant. That’s why the standard rules of calculus fails over it.
Note that Riemannian integral works out only when we have convergent integral limits regardless of different integrant.
To figure out what stochastic calculus is doing, we can make an comparison between regular integral and stochastic integral
  $$R\left(t+\delta t\right)=\underset{0}{\overset{t+\delta t}{\int}}H\left(s\right)ds\approx R\left(t\right)+H\left(t\right)\delta t$$
  $$I\left(t+\delta t\right)=\underset{0}{\overset{t+\delta t}{\int}}H\left(s\right)dW\left(s\right)\approx I\left(t\right)+H\left(t\right)\left(W\left(t+\delta t\right)-W\left(t\right)\right)$$
We can find they share the description about increment over an infinitesimal time, which was scaled by $H\left(t\right)$*, *instead the former has deterministic step size, the later has random one.
So the output from stochastic calculus is accumulation of random increments, which is also a stochastic process.
That is a stochastic process can be a function of another one, and so is its statistics (mean, variance).
Provided statistics of its "x-stochastic-process" are known, so is its distribution, from which state at specific time can be determined.
Actually, there is **idea** works beneath the conversion from randomness to determinist or consistency between them.
Recall that stochastic process is underivable, but that is only established in deterministic space, can it be derivable in random space ?
First let's take a look at the definition of the regular derivative
  $$\underset{h\to 0}{\mathrm{lim}}\frac{f\left(t+h\right)-f\left(t\right)}{h}={f}^{\prime}\left(t\right)$$
But such limit does not exist for stochastic process, since it's also a random variable following some distribution
  $$\underset{h\to 0}{\mathrm{lim}}\frac{X\left(t+h\right)-X\left(t\right)}{h}~P$$
Note that a random variable converges to its mean almost surely if its variance converges to 0
So we can define $X\left(t\right)$*'s *derivative with ${X}^{\prime}\left(t\right)$ if the limit converges to it almost surely
  $$\left\{\begin{array}{c}\underset{h\to 0}{\mathrm{lim}}E\left[\frac{X\left(t+h\right)-X\left(t\right)}{h}\right]={X}^{\prime}\left(t\right)\\ \underset{h\to 0}{\mathrm{lim}}Var\left[\frac{X\left(t+h\right)-X\left(t\right)}{h}\right]=0\end{array}\right.$$
  Or equivalently
  $$\underset{h\to 0}{\mathrm{lim}}E\left[{\left(\frac{X\left(t+h\right)-X\left(t\right)}{h}-{X}^{\prime}\left(t\right)\right)}^{2}\right]=0$$
Under the support of probabilistic tools, the definition in deterministic space can also be established in stochastic space and so is the conversion from indeterminist to determinist  
**Stochastic Process**  
Let's start from a simple instance of **one dimensional symmetric random walk**, which is a discrete value, discrete time stochastic process.
Here is the deal:
An easy way to think of it is: starting at 0, at each time step, flip a fair coin and move up (+1) if heads, otherwise move down (-1).
  $${X}_{t}\left(\mathit{\omega}\right)=\left\{\begin{array}{c}1,\ \ {\mathit{\omega}}_{t}=H\\ -1,\ \ {\mathit{\omega}}_{t}=T\end{array}\right.,\mathit{\omega}={\mathit{\omega}}_{1}{\mathit{\omega}}_{2}{\mathit{\omega}}_{3}\dots \in \mathrm{\Omega}=\left\{{\left({a}_{n}\right)}_{1}^{\infty}:{a}_{n}\in \left\{H,T\right\}\right\}$$
But here we need to define a legal way to measure samples' probability, i.e. a [measurable sample space](onenote:#Preliminary&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={FC3FD93B-B8A9-4DAE-B196-0E6AE03017A3}&object-id={CBE548A0-8591-0545-2662-5ED383EF2157}&1C&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one) which is compatible when $t\to \infty $
Provided with well-defined Bernoulli process ${X}_{t}\left(\mathit{\omega}\right)$, the position at time t can be defined:
  $${S}_{t}\left(\mathit{\omega}\right)={\sum}_{i=1}^{t}{X}_{i}\left(\mathit{\omega}\right),{S}_{0}=0$$
Increment between any pairs of time step are independent, since any increment can be summation of independent Bernoulli random variable within.
  $$\left\{\begin{array}{c}E\left[{S}_{{k}_{i+1}}-{S}_{{k}_{i}}\right]=0\\ Var\left[{S}_{{k}_{i+1}}-{S}_{{k}_{i}}\right]={k}_{i+1}-{k}_{i}\end{array}\right.$$
So the state at any time step may have expectation stay at origin, but with deviation (variance) accumulating at a rate of one unit per time step.
The next is to consider a** scaled symmetric random walk** extended from its simple sibling
  $${W}^{\left(n\right)}\left(t\right)=\frac{1}{\sqrt{n}}{S}_{nt},\ \ {W}^{\left(n\right)}\left(0\right)=0$$
Here we can compress time step into ratio number set, or** further, into continuous time step** if $\mathrm{n}\to \infty $
And it follows the same properties as simple random walk
   $\left\{\begin{array}{c}E\left[{W}^{\left(n\right)}\left(t\right)-{W}^{\left(n\right)}\left(s\right)\right]=0\\ Var\left[{W}^{\left(n\right)}\left(t\right)-{W}^{\left(n\right)}\left(s\right)\right]=t-s\\ {\left[{W}^{\left(n\right)},{W}^{\left(n\right)}\right]}_{t}=t\end{array}\right.$ <equation>
  It has non-zero Quadratic variation
And by central limit theorem, ${W}^{\left(n\right)}\left(t\right)$ converges to some Gaussian distribution when $\mathrm{n}\to \infty $
  $$\underset{\mathrm{n}\to \infty}{\mathrm{lim}}{W}^{\left(n\right)}\left(t\right)=\underset{\mathrm{n}\to \infty}{\mathrm{lim}}\frac{1}{\sqrt{n}}{\sum}_{j=1}^{nt}{X}_{j}~\mathcal{N}\left(0,t\right),\ \ set\ s=0$$  
    
By taking the limit of scaled symmetric random walk, we can arrive at the definition of **Wiener process** , a continuous time real-valued stochastic process, which is inherited from the scaled symmetric random walk
  $$W\left(t\right)\u2254W\left(t,\mathit{\omega}\right),\ \ W\left(0\right)=0$$
All increments are identical independent distributed
  $$0={t}_{0}<{t}_{1}<\dots <{t}_{m},\ W\left({t}_{i+1}\right)-W\left({t}_{i}\right).i.i.d$$
  $$\left(W\left({t}_{i+1}\right)-W\left({t}_{i}\right)\right)~\mathcal{N}\left(0,{t}_{i+1}-{t}_{i}\right)$$
These are also properties that describes Brownian motion where path of a moving particle inside a box filled with other molecular is represented as $\mathit{\omega}$ and random movement at each infinitesimal point in time was droven by interaction with surrounding molecular is described as increment along the path.
Most importantly, quadratic variation follows consistently
  $$\underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}{\left[W,W\right]}_{t}=t$$
This is at the core of stochastic calculus so that we can describe stochastic integral with its statistics
  $$\left\{\begin{array}{c}dW\left(t\right)dW\left(t\right)=dt\\ dW\left(t\right)dt=0\\ dtdt=0\end{array}\right.,using\underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}\Vert \mathrm{\Pi}\Vert =0$$
  $$dW\left(t\right)=\underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}\left[W\left({t}_{j+1}\right)-W\left({t}_{j}\right)\right]$$

Due to some special properties(independent increment) of Weier process, any continuous time stochastic process can be written as function of it:
  $$X\left(t\right)=X\left(0\right)+bt+\mathit{\sigma}W\left(t\right)$$
Where $b\ \mathrm{and}\ \mathit{\sigma}$ are called drift term and diffusion term respectively, the drift term tells the bias of this stochastic process, forming its deterministic part, while the diffusion term stands random perturbation, forming its indeterministic part  
**Relationship between Gaussian white noise and Wiener process**  
Using the [definition of derivative in probabilistic space](onenote:#Stochastic%20Calculus&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={B902F5EC-F124-4DA3-A095-4D81332902CE}&object-id={AE9D6B8B-1D99-0A05-0AA7-DE6ECE92FC4B}&C8&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one), white noise is the derivative of Wiener process
  $$W\left(t\right)=\underset{0}{\overset{t}{\int}}\mathit{\eta}\left(s\right)ds$$
Note that Gaussian white noise(also a stochastic process) has zero mean and Dirac delta time correlation, it can be proved that derivative of Wiener process possesses same properties
  $$E\left[\frac{dW\left(t\right)}{dt}\right]=E\left[\underset{h\to 0}{\mathrm{lim}}\frac{W\left(t+h\right)-W\left(t\right)}{h}\right]=E\left[\mathit{\eta}\left(t\right)\right]=0$$
  $$E\left[\frac{dW\left({t}_{1}\right)}{d{t}_{1}}\frac{dW\left({t}_{2}\right)}{d{t}_{2}}\right]=E\left[\mathit{\eta}\left({t}_{1}\right)\mathit{\eta}\left({t}_{2}\right)\right]=\mathit{\delta}\left({t}_{2}-{t}_{1}\right)$$
So we have
  $$\frac{dW\left(t\right)}{dt}=\mathit{\eta}\left(t\right),\ \ almost\ surely$$  
    

**Solving Stochastic Calculus**  
It's quite a tangent from where we start, but with a depth diving into Wiener process, the building block for any continuous real-valued stochastic process, now we can move on.
Replace back into stochastic calculus
  $$G\left(t\right)=\underset{0}{\overset{t}{\int}}bH\left(s\right)ds+\underset{0}{\overset{t}{\int}}\mathit{\sigma}H\left(s\right)dW\left(s\right)$$
The first part in right of equation can be solved using regular integral(since $dt$ is determined), but not so for the second part, that's why we need stochastic calculus
  $$\underset{0}{\overset{t}{\int}}H\left(s\right)dW\left(s\right)=\underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}{\sum}_{j=0}^{n-1}H\left({s}_{j}\right)\left[W\left({t}_{j+1}\right)-W\left({t}_{j}\right)\right]$$
Same as the Riemannian Integral, take $H\left(t\right)=W\left(t\right)$
When ${s}_{j}={t}_{j}$
  $$\underset{0}{\overset{t}{\int}}W\left(s\right)dW\left(s\right)=\frac{1}{2}W{\left(t\right)}^{2}-\frac{1}{2}\underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}{\left[W,W\right]}_{t} \\ =\frac{1}{2}W{\left(t\right)}^{2}-\frac{1}{2}t$$
When ${s}_{j}=\frac{{t}_{j}+{t}_{j+1}}{2}$
  $$\underset{0}{\overset{t}{\int}}W\left(s\right)\circ dW\left(s\right)=\underset{0}{\overset{t}{\int}}W\left(s\right)dW\left(s\right)+\frac{1}{2}\underset{\Vert \mathrm{\Pi}\Vert \to 0}{\mathrm{lim}}{\left[W,W\right]}_{t} \\ =\frac{1}{2}W{\left(t\right)}^{2}$$
This is the subtle difference from regular integral that a biased integrant will result in biased stochastic process. So the solution for stochastic calculus dependents on the assumption on practical problems.
e.g. when modeling stock price at time, it will be inappropriate to pick integrant in the time interval, since the information from future is unreachable, so we can only use information at current time.
Note that $H\left(t\right)$ can also be written function of Weier process
  $$H\left(t\right)=H\left(0\right)+at+\mathit{\gamma}W\left(t\right)$$
Replace back into stochastic calculus
  $$G\left(t\right)=\underset{0}{\overset{t}{\int}}\left[bH\left(0\right)+abs+b\mathit{\gamma}W\left(s\right)\right]ds+\underset{0}{\overset{t}{\int}}\left[\mathit{\sigma}H\left(0\right)+\mathit{\sigma}as+\mathit{\sigma}\mathit{\gamma}W\left(s\right)\right]dW\left(s\right)$$
Which has same form as function of Wiener process
And $E\left[G\left(t\right)\right],Var\left[G\left(t\right)\right]$ is function of $E\left[W\left(t\right)\right],Var\left[W\left(t\right)\right]$  
[An instance of applicaiton](https://bjlkeng.io/posts/an-introduction-to-stochastic-calculus/#id20)  
**Stochastic Differential Equations**  
Differential form of stochastic calculus
  $$dX\left(t\right)=\mathit{\mu}\left(t,X\left(t\right)\right)dt+\mathit{\sigma}\left(t,X\left(t\right)\right)dW\left(t\right)$$
To solve the equation is to find $X\left(t\right)$ satisfies
  $$X\left(t\right)=X\left(0\right)+\underset{0}{\overset{t}{\int}}\mathit{\mu}\left(s,X\left(s\right)\right)ds+\underset{0}{\overset{t}{\int}}\mathit{\sigma}\left(s,X\left(s\right)\right)dW\left(s\right)$$
Note [LMC](onenote:#Sampling%20Method&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={4F341C3A-CF66-4855-B9B3-DA4571AC8699}&object-id={06EEE7F5-CE73-0748-1E1B-6D331EBE8217}&98&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one) is also a SDE, describing a biased stochastic process where drift term is gradient leading to large density region and diffusion term(including $dW\left(t\right)$) is injected random noise
  $$m\frac{d{\bm{v}}_{\bm{t}}}{dt}=-\mathit{\lambda}{\bm{v}}_{\bm{t}}+\mathit{\eta}\left(t\right)$$
Set $m=1$
  $$d{\bm{v}}_{\bm{t}}=-\mathit{\lambda}{\bm{v}}_{\bm{t}}dt+\mathit{\eta}\left(t\right)dt$$
Note that Gaussian white noise is derivative of Wiener process almost surely
  $$\frac{dW\left(t\right)}{dt}=\mathit{\eta}\left(t\right),\ \ almost\ surely$$
This will leads to its SDE
  $$d{\bm{v}}_{\bm{t}}=-\mathit{\lambda}{\bm{v}}_{\bm{t}}dt+dW\left(t\right)$$
In paper "SCORE-BASED GENERATIVE MODELING THROUGH STOCHASTIC DIFFERENTIAL EQUATIONS", SGLD and DDPM can be described by corresponding SDEs where the integral form all involving addition with Normal noise.
This is resulted from integral property of Dirac delta function
  $$\underset{0}{\overset{T}{\int}}dW\left(t\right)=\underset{0}{\overset{T}{\int}}\mathit{\eta}\left(t\right)dt\u2254\mathcal{N}\left(0,1\right),$$
$$\left\{\begin{array}{c}E\left[\mathit{\eta}\left(t\right)\right]=0\Rightarrow E\left[\underset{0}{\overset{T}{\int}}\mathit{\eta}\left(t\right)dt\right]=0\\ Var\left[\underset{0}{\overset{T}{\int}}\mathit{\eta}\left(t\right)dt\right]=\underset{T\to \infty}{\mathrm{lim}}\frac{1}{T}\underset{0}{\overset{T}{\int}}\underset{0}{\overset{T}{\int}}\mathit{\eta}\left(s\right)\mathit{\eta}\left(t\right)dtds=\underset{0}{\overset{T}{\int}}\mathit{\delta}\left(\mathit{\tau}\right)d\mathit{\tau}=1\end{array}\right.$$
  $$\mathrm{for}\underset{T\to \infty}{\mathrm{lim}}\frac{1}{T}\underset{0}{\overset{T}{\int}}\mathit{\eta}\left(t+\mathit{\tau}\right)\mathit{\eta}\left(t\right)dt=c\mathit{\delta}\left(\mathit{\tau}\right),\ s=t+\mathit{\tau}$$  
    

When analytical solution exists, stochastic calculus can work, otherwise, numerical method had to be used to solve them out
e.g. Monte Carlo Simulation and Partial Differential Equation
When stochastic process has form
  $$Y\left(t\right)=f\left(t,X\left(t\right)\right)$$
It can get back to similar form by using Taylor second-order expansion
  $$dY\left(t\right)=\frac{\mathit{\partial}f}{\mathit{\partial}t}dt+\frac{\mathit{\partial}f}{\mathit{\partial}X\left(t\right)}dX\left(t\right)+\frac{1}{2}\frac{{\mathit{\partial}}^{2}f}{\mathit{\partial}X{\left(t\right)}^{2}}dX\left(t\right)dX\left(t\right)$$
  $$dY\left(t\right)=\left(\frac{\mathit{\partial}f}{\mathit{\partial}t}+\mathit{\mu}\left(t\right)\frac{\mathit{\partial}f}{\mathit{\partial}X\left(t\right)}+{\mathit{\sigma}}^{2}\left(t\right)\frac{{\mathit{\partial}}^{2}f}{\mathit{\partial}X{\left(t\right)}^{2}}\right)dt+\frac{\mathit{\partial}f}{\mathit{\partial}X\left(t\right)}\mathit{\sigma}\left(t\right)dW\left(t\right)$$

**Dynamics, a stochastic process too**  
From a birds fly view, we can roughly split a stochastic process into deterministic and non-deterministic parts, similar to [HMC](onenote:#Sampling%20Method&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={4F341C3A-CF66-4855-B9B3-DA4571AC8699}&object-id={8918F406-FA6B-0184-0AFC-EF8E34924A96}&B&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one), which simulates a Hamiltonian Dynamics to make sampling process converge to target distribution.
More specifically, it samples points along directions toward high density region, which is indicated by gradients of energy-based function(containing $\mathrm{log}p\left(x\right)$ , that’s why we are heading to high density region). But deterministic guidence will only collapse at mode, instead of target distribution, simulation of interaction with heatbath was corporated as random perturbation to enable generated samples follow the target distribution around the mode.
