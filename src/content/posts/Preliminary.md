---
title: Preliminary
published: 2023-06-26
description: "Something you should know before starting."
tags: ["preliminary"]
category: Guides
draft: false
---

**Reflection-Ask more, Simbolic description, be more patient, be more fun**  
1. What is exactly we trying to solve and the ideal result ? or What is it look like, before solution and after solution ?
2. How does the solution do to solve it ? (the general process, not the parsed detail)
3. How does the solution come out ? (peel it out the simple core idea)
4. How does the idea behind adapt on this problem ? Are there any generalized way ?
It's indeed hard to remember all the complex detail of the solution, also it's boring to do so, so why not just to figure out the simple idea or theorim behind it and its adaption on real problem, and further, how to generalize it to more universal conditions.

[**Set VS Space**](https://math.stackexchange.com/questions/4362803/set-vs-space-in-definitions)  
In general, set is a concept with wider generalization than space, or we can say that space is equivalent to a set equipped with some operations.
e.g. vector space is set of vectors with closed addition and multiplication. More specifically, ${R}^{n}$ is a vector space, also a set made of n-dimension vectors, but any randomly picked subset of it may not satisfy a vector space, for the required closed operations are not met.  
[**Probability Space**](https://bjlkeng.io/posts/an-introduction-to-stochastic-calculus/)  
What support us to measure an event, a group of samples, with a quantity is the main story of measure theoretic definition of probability which can be extent to infinite sample space.
First, let's consider sample space $\mathrm{\Omega}$ with finite cardinality.
  So, all the possible events(event space) can be described as power set of sample space: ${2}^{\mathrm{\Omega}}$ which contains any possible trail that can be measured by frequency.
  Specifically, probability of any event $A$ can be measured by the following way

$$\displaystyle P\left(A\right)=\frac{\#\left(\mathrm{A}\right)}{\#\left(\mathit{\Omega}\right)},A\in {2}^{\mathrm{\Omega}},\ \ \#\left(\mathit{\Omega}\right)\ne +\infty ,P\left(\varnothing \right)=0$$

  And event space defines a closed set that:
 
$$\displaystyle \varnothing \in {2}^{\mathit{\Omega}}$$

$$A\in {2}^{\mathit{\Omega}},A^{C}\in {2}^{\mathit{\Omega}}$$

$${A}_{1},{A}_{2},\dots \in {2}^{\mathit{\Omega}},A_{1}\cup {A}_{2}\cup \dots \cup {A}_{n}\in {2}^{\mathit{\Omega}},same\ as\ intersection$$

But such measurement is undefined in sample space with infinite cardinality. For this, we need to define our own event space $\mathcal{F}\subseteq {2}^{\mathrm{\Omega}}$ more precisely while still follow the measurable rules by using a construction called $\sigma $\-algebra(still a closed set):

$$\varnothing \in \mathcal{F}$$

$$A\in \mathcal{F},A^{C}\in \mathcal{F}$$

$${A}_{1},{A}_{2},\dots \in {2}^{\mathit{\Omega}},A_{1}\cup {A}_{2}\cup \dots \cup {A}_{n}\in {2}^{\mathit{\Omega}},n\to +\infty ,same\ as\ intersection$$

Now all the measurable elements are confined in $\mathcal{F}$ and we can call them measurable sets, combined with sample space, a meaure space $\left(\mathit{\Omega},\mathcal{F}\right)$ can be defined.
It lists out the measurable events we can take as we do in finite sample space where measurable events are implicitly the power set of sample space.
Measurable space + measure rules
Inside the specific measurable space, the probability **measure** rules(function) $P$ can work as usual:

$$P:\mathcal{F}\to \left[0,1\right]$$

$$P\left(\varnothing \right)=0,P\left(\mathit{\Omega}\right)=1$$

$$\forall disjoint\ {A}_{1},\dots {A}_{n}\in \mathcal{F},P\left({U}_{i}{A}_{i}\right)={\sum}_{i}P\left({A}_{i}\right)$$

Combination of three yields probability space $\left(\mathit{\Omega},\mathcal{F},P\right)$ upon which a random variable(**measurable** function) can build

$$X:\mathit{\Omega}\to E\subseteq \mathbb{R}$$

1. It maps measurable space on sample space into that on real space  
For finite sample space

$$\left(\mathit{\Omega},{2}^{\mathrm{\Omega}}\right)\to \left(E,{2}^{E}\right)$$

For infinite sample space

$$\left(\mathit{\Omega},\mathcal{F}\right)\to \left(E,S\right),S\ is\ Borel\ set$$

2. It's a bijective mapping on $\mathcal{F}$

$$\forall s\in S,\left\{X\in s\right\}\in \mathcal{F},\left\{\mathit{\omega}\in \mathit{\Omega}|X\left(\mathit{\omega}\right)\in s\right\}\in \mathcal{F}$$

$$\sigma \left(X\right)=\left\{\left\{X\in s\right\}|s\in S\right\}$$

**Gradient&Derivative on Specific Direction**  
**Basic thoughts:**  
Multivariant
$$\bm{x}=\left({x}_{1},{x}_{2},\dots \right),f\left(\bm{x}\right)$$
We can get a slice figure of $f\left(x\right)$ by cutting it along a specifc direction **u** = ${\left[{u}_{1},\ {u}_{2},\ \dots \right]}^{T},\left|\left|\bm{u}\right|\right|=1$
Now we return to univariant case where the x-axis becomes s, and y-axis is function's value
$$start\ from\ {P}_{0}={\bm{x}}_{0},\ end\ at\ P=\bm{x},\left\{\begin{array}{c}\bm{P}{\bm{P}}_{0}=s\bm{u}\\ \left|\bm{P}{\bm{P}}_{0}\right|=s\end{array}\right.,u=\frac{\bm{x}-{\bm{x}}_{0}}{\left|\left|\bm{x}-{\bm{x}}_{0}\right|\right|}$$
Inner Product between Gradient and Direction, by chain rule
$${\left.\frac{df}{ds}\right|}_{\bm{u},{p}_{0}}=\underset{s\to 0}{\mathrm{lim}}\frac{f\left(\bm{x}\right)-f\left({\bm{x}}_{0}\right)}{s}={\left.\frac{df}{d\bm{x}}\right|}_{{P}_{0}}{\left.\frac{d\bm{x}}{ds}\right|}_{\bm{u}}=\ {\left({\left.{\mathbf{\nabla}}_{\bm{x}}\bm{f}\right|}_{{P}_{0}}\right)}^{T}\bm{u}$$  
**Confusion between Gradient and Normal of plane**  
We can make an analogy from derivative along $\mathbf{u}$ to tangent line in univariant function,
What's different is in multivariant case tangent line turns into tangent plane, and its normal is marked as
$$\bm{n}={\left[\frac{\mathit{\partial}f}{\mathit{\partial}{x}_{1}},\frac{\mathit{\partial}f}{\mathit{\partial}{x}_{2}},\dots ,-1\right]}^{T},\ i.e.\ {\left[{\mathbf{\nabla}}_{\bm{x}}\bm{f},-\frac{\mathit{\partial}f}{\mathit{\partial}f}\right]}^{T}$$
$$z=f\left(\bm{x}\right)\Rightarrow f\left(x\right)-z=0\Rightarrow \left[\bm{x}-{\bm{x}}_{0},z-{z}_{0}\right]\bm{n}=0$$
 $\left(\bm{x},z\right)$ is on the plane, note that $z\ne f\left(\bm{x}\right)$
This can be verified as an analog to a line in x-y coordinate system
$$\frac{z-{z}_{0}}{s}={\bm{u}}^{\bm{T}}{\mathbf{\nabla}}_{\bm{x}}\bm{f}$$
So the gradient has same dimensionality as its define field, it's the vector with components from partial derivative of each dimension at point ${x}_{0}$(each partial derivative indicates the changing rate along corresponding dimension, so gradient indicates the global steepest direction of changing)*, *and the directed derivative is exactly projection(inner product) on specific direction
[Why gradient indicates the direction of increasing](https://math.stackexchange.com/questions/223252/why-is-gradient-the-direction-of-steepest-ascent) ?
Similar to slope $\mathrm{k}={f}^{\prime}\left(x\right)$ in univariant case, when k > 0, we are heading the increase direction, vice versa. This is equivalent to make ${\mathrm{D}}_{\bm{u}}f>0$ where we increase function
${\mathrm{D}}_{\bm{u}}f={\mathbf{\nabla}}_{\bm{x}}{\bm{f}}^{\bm{T}}\bm{u}>0$, so when our choosen direction close to gradient, we are increasing function, that indicates gradient as the direction of ascent  
[**Calculus of Variations**](https://bjlkeng.io/posts/the-calculus-of-variations/)  
$$J\left[u\left(x\right)\right]=\underset{a}{\overset{b}{\int}}L\left(x,u\left(x\right),\ {u}^{\prime}\left(x\right)\right)dx:F\to R,\ u\left(a\right)=\mathit{\alpha},\ u\left(b\right)=\mathit{\beta}$$
F is infinite-dimensional function space
$$J\left[u\left(x\right)+\mathit{\epsilon}v\left(x\right)\right]=\underset{a}{\overset{b}{\int}}L\left(x,u\left(x\right)+\mathit{\epsilon}v\left(x\right),\ {u}^{\prime}\left(x\right)+\mathit{\epsilon}{v}^{\prime}\left(x\right)\right)dx,v\left(a\right)=v\left(b\right)=0$$
$$\frac{dJ}{d\mathit{\epsilon}}=\underset{\mathit{\epsilon}\to 0}{\mathrm{lim}}\frac{J\left[u\left(x\right)+\mathit{\epsilon}v\left(x\right)\right]-J\left[u\left(x\right)\right]}{\mathit{\epsilon}}$$
$$=\underset{\mathit{\epsilon}\to 0}{\mathrm{lim}}\underset{a}{\overset{b}{\int}}\left[\frac{\mathit{\partial}L}{\mathit{\partial}\left(u\left(x\right)+\mathit{\epsilon}v\left(x\right)\right)}v\left(x\right)+\frac{\mathit{\partial}L}{\mathit{\partial}\left(u\prime \left(x\right)+\mathit{\epsilon}{v}^{\prime}\left(x\right)\right)}{v}^{\prime}\left(x\right)\right]dx$$
$$=\underset{a}{\overset{b}{\int}}\left[\frac{\mathit{\partial}L}{\mathit{\partial}u\left(x\right)}v\left(x\right)+\frac{\mathit{\partial}L}{\mathit{\partial}{u}^{\prime}\left(x\right)}{v}^{\prime}\left(x\right)\right]dx=\underset{a}{\overset{b}{\int}}\mathbf{\nabla}{\bm{L}\left(x,u\left(x\right),{u}^{\prime}\left(x\right)\right)}^{\bm{T}}\left[\begin{array}{c}v\left(x\right)\\ {v}^{\prime}\left(x\right)\end{array}\right]dx=\mathbf{\nabla}\bm{J}{\left[\bm{u}\right]}^{\bm{T}}\bm{v}$$
$$=\underset{a}{\overset{b}{\int}}\frac{\mathit{\partial}L}{\mathit{\partial}u\left(x\right)}v\left(x\right)dx+\underset{a}{\overset{b}{\int}}\frac{\mathit{\partial}L}{\mathit{\partial}{u}^{\prime}\left(x\right)}dv\left(x\right)$$
$$=\underset{a}{\overset{b}{\int}}\left[\frac{\mathit{\partial}L}{\mathit{\partial}u\left(x\right)}-\frac{d}{dx}\left(\frac{\mathit{\partial}L}{\mathit{\partial}{u}^{\prime}\left(x\right)}\right)\right]v\left(x\right)dx$$
To find stationary, a functional must satisfy
$$\frac{\mathit{\partial}L}{\mathit{\partial}u\left(x\right)}-\frac{d}{dx}\left(\frac{\mathit{\partial}L}{\mathit{\partial}{u}^{\prime}\left(x\right)}\right)=0$$
Which is known as the Euler-Lagrange equations  
[**Calculate vector's derivative w.r.t vector**](https://zhuanlan.zhihu.com/p/36448789)  
$$\bm{A}\bm{x}=\bm{y},\bm{A}\in {R}^{m\times n},\bm{x}\in {R}^{n\times 1},\bm{y}\in {R}^{m\times 1}$$
The shape of derivative is same as $\bm{x}$
$$\frac{\mathit{\partial}\bm{y}}{\mathit{\partial}\bm{x}}=\left[\begin{array}{c}\frac{\mathit{\partial}\bm{y}}{\mathit{\partial}{x}_{1}}\\ \vdots \\ \frac{\mathit{\partial}\bm{y}}{\mathit{\partial}{x}_{n}}\end{array}\right],\frac{\mathit{\partial}\bm{y}}{\mathit{\partial}{x}_{i}}=\left[\begin{array}{ccc}\frac{\mathit{\partial}{y}_{1}}{\mathit{\partial}{x}_{i}}& \dots & \frac{\mathit{\partial}{y}_{m}}{\mathit{\partial}{x}_{i}}\end{array}\right]$$
$$\Rightarrow \frac{\mathit{\partial}\bm{y}}{\mathit{\partial}\bm{x}}=\left[\begin{array}{ccc}\frac{\mathit{\partial}{y}_{1}}{\mathit{\partial}{x}_{1}}& \dots & \frac{\mathit{\partial}{y}_{m}}{\mathit{\partial}{x}_{1}}\\ \vdots & \ddots & \vdots \\ \frac{\mathit{\partial}{y}_{1}}{\mathit{\partial}{x}_{n}}& \dots & \frac{\mathit{\partial}{y}_{m}}{\mathit{\partial}{x}_{n}}\end{array}\right]={A}^{T}\Rightarrow \left\{\begin{array}{c}\frac{\mathit{\partial}\bm{A}\bm{x}}{\mathit{\partial}\bm{x}}={A}^{T}\\ \frac{\mathit{\partial}A\bm{x}}{\mathit{\partial}{\bm{x}}^{\bm{T}}}=\bm{A}\end{array}\right.$$

**The Exponiential Family**  
$$p\left(\bm{x}|\bm{\eta}\right)=h\left(\bm{x}\right)g\left(\bm{\eta}\right)\mathrm{exp}\left\{\bm{\eta}^{\bm{T}}\bm{u}\left(\bm{x}\right)\right\},\ \ g\left(\bm{\eta}\right)\int h\left(\bm{x}\right)\mathrm{exp}\left\{\bm{\eta}^{\bm{T}}\bm{u}\left(\bm{x}\right)\right\}d\bm{x}=1$$
conjugate priors
$$p\left(\bm{\eta}|X,v\right)=f\left(X,v\right)g{\left(\bm{\eta}\right)}^{v}\mathrm{exp}\left\{v{\bm{\eta}}^{\bm{T}}X\right\}$$
  $\left(X,v\right)$:normalization coefficient  
  $v$: indicates number of states of $u\left(\bm{x}\right)$, or cardinality of $u\left(\bm{x}\right)$'s sample space  
   $X:$ indicates possible existence counts for each state of $\bm{u}\left(\bm{x}\right)$  
$$p\left(\bm{\eta}|\bm{x},X,v\right)\propto p\left(\bm{x}|\bm{\eta}\right)p\left(\bm{\eta}|X,v\right)=h\left(\bm{x}\right)f\left(X,v\right)g{\left(\bm{\eta}\right)}^{v+1}\mathrm{exp}\left\{\bm{\eta}^{\bm{T}}\left(\bm{u}\left(\bm{x}\right)+vX\right)\right\}$$
  *The posterior has same form as its conjugate prior*  
    
**Notes of Analysis [Tenrece Tao]**  
Lemma 5.3.14
Prove keypoint: for a non-zero real number, its corresponding Cauchy sequence must exists an element having arbitray distance away from 0
Proposition 5.4.14
Prove idea: Usage of Archimedes property (Deduction 5.4.13) and Proposition 5.4.12(bounding real number by ratio number)
Theorem 5.5.9
Prove idea: prove that E has at most one supreme and at least one supreme
By definition of supreme, we find supreme by keeping looking smaller upper bound until the smallest one, that will generate a sequence of upper bound, which can be proved as a Cauchy sequence, then its limit number is supreme.
Archimedes property (Deduction 5.4.13) can be used to construct the desired upper bound sequence
The uniqueness is based on Proposition 4.4.1
