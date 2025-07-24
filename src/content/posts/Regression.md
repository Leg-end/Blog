---
title: Regression
published: 2023-03-19
description: "Learn to predict real value"
tags: ["Linear Hypothesis", "Bayesian Linear Regression"]
category: Regression
draft: false
---

***Introduction***  
*Idea of solving linear regression problem*
*Regression problem always require fitting on points, but in reality, fitting the exact point is unfeasible, since the turbulance of noise or random error when sampling.*
*So it's natural to switch to fitting a softer target, an area around the sample points. May yield a better and feasible solution.*
*You may already seen similar thoughts in SVM, which named slack variables. Or a threshold controling convergence on simple method of linear regression, or a probabilistic parameter called precison, i.e. inversion of variance.*
Note : the relationship between x and y may only involve numerical, the cause-and-result may not always true  
***Definition***  
Data $D:\left\{\left({\bm{x}}^{\left(\bm{i}\right)},{t}^{\left(i\right)}\right)\right\}.i.i.d\ from\ p\left(\bm{x},t\right)$
Estimate (Hypothesis Space) $\mathrm{y}\left(\bm{x}\right)$
Assumption
since in inference, given $x\Rightarrow p\left(\bm{x}\right)=1\Rightarrow we\ only\ care\ p\left(t|\bm{x}\right)$
so we need to find $p\left(t|\bm{x}\right)$ from data, assume

$$
\mathrm{p}\left(t|\bm{x}\right)=\left\{\begin{array}{c}\mathcal{B}\left(t|\mathit{\mu}\left(x\right),\mathit{\mu}\left(x\right)\left(1-\mathit{\mu}\left(x\right)\right)\right),logistic\ regression\\ \mathcal{N}\left(t|\mathit{\mu}\left(x\right),{\mathit{\sigma}}^{2}\left(x\right)\right),linear\ regression\end{array}\right.
$$

base on maxilikelihood assumption

$$
\mathrm{max}\left(\mathrm{p}\left(t|\bm{x}\right)\right)=\mathrm{p}\left(\mathit{\mu}\left(x\right)|\bm{x}\right)\Rightarrow \mathrm{define}\ \mathrm{ideal}\ y\left(\bm{x}\right)\equiv \mathit{\mu}\left(\bm{x}\right)=E\left[t|\bm{x}\right]
$$

Error(Loss) function: $L\left(t,\ y\left(\bm{x}\right)\right)$
Target:$\underset{y\left(\bm{x}\right)}{\mathrm{argmin}}{E}_{\left(\bm{x},t\right)~D}\left[L\right]$

$$
{E}_{\left(\bm{x},t\right)~D}\left[L\right]=\int \int L\left(t,\ y\left(\bm{x}\right)\right)p\left(\bm{x},t\right)d\bm{x}dt
$$

*Question: The idea behind the target form?*
*In classification, loss is a evaluation of decision, i.e a cost of specific behave*

$$
E\left[L\right]={\sum}_{k}{\sum}_{j}\underset{{R}_{j}}{\int}{L}_{kj}p\left(x,{C}_{k}\right)dx,{L}_{kk}=0,\ {R}_{j}=\left\{x|x\ belong\ to\ {C}_{j}\right\}
$$

*The cost when x belong to class k, while was distributed to class j*

$$
\Rightarrow \forall x\mathit{\epsilon}{R}_{j},\mathrm{min}{\sum}_{k}{L}_{kj}p\left(x,{C}_{k}\right)\propto \mathrm{min}{\sum}_{k}{L}_{kj}p\left({C}_{k}|x\right)
$$

*under L2 loss, choose *$y\left(x\right)$* so as to minimize *$E\left[L\right]$
*why L2 loss? It's a assumption of Gaussian Distribution*

$$
E\left[L\right]=\int \int {\left(y\left(\bm{x}\right)-t\right)}^{2}p\left(\bm{x},t\right)d\bm{x}dt
$$

$$
\Rightarrow \frac{\mathit{\partial}E\left[L\right]}{\mathit{\partial}y\left(x\right)}=0
$$

$$
\Rightarrow 2\int \int \left(y\left(\bm{x}\right)-t\right)p\left(\bm{x},t\right)d\bm{x}dt=0
$$

$$
\Rightarrow \int \left(y\left(\bm{x}\right)-t\right)p\left(\bm{x},t\right)dt=0
$$

$$
\Rightarrow y\left(\bm{x}\right)=\frac{\int tp\left(\bm{x},t\right)dt}{p\left(\bm{x}\right)}
$$

$$
\Rightarrow y\left(\bm{x}\right)\equiv \int tp\left(t|\bm{x}\right)dt=E\left[t|\bm{x}\right]
$$

*optimal *$y\left(\bm{x}\right)$* is the conditional average, since points at mean have maximal probability, so best function is conditional expectation, which is conditional mean.*
*Note: Optimal *$y\left(x\right)$ *is defined as conditional expection, which called regression function*
*we can see the component of error*

$$
E\left[L\right]=\int \int {\left(y\left(\bm{x}\right)-E\left[t|\bm{x}\right]+E\left[t|\bm{x}\right]-t\right)}^{2}p\left(\bm{x},t\right)d\bm{x}dt
$$

$$
=\int {\left(y\left(\bm{x}\right)-E\left[t|\bm{x}\right]\right)}^{2}p\left(\bm{x}\right)d\bm{x}+\int {\left(E\left[t|\bm{x}\right]-t\right)}^{2}p\left(\bm{x}\right)d\bm{x}
$$

*consider for a large number of data sets *$S=\left\{D\right\}$

$$
\int {\left(y\left(\bm{x};D\right)-{E}_{D}\left[t|\bm{x}\right]\right)}^{2}p\left(\bm{x}\right)d\bm{x}
$$

$$
=\int {\left(y\left(\bm{x};D\right)-{E}_{D}\left[y\left(\bm{x};D\right)\right]+{E}_{D}\left[y\left(\bm{x};D\right)\right]-{E}_{D}\left[t|\bm{x}\right]\right)}^{2}p\left(\bm{x}\right)d\bm{x}
$$

$$
=\int {\left({E}_{D}\left[y\left(\bm{x};D\right)\right]-{E}_{D}\left[t|\bm{x}\right]\right)}^{2}p\left(\bm{x}\right)d\bm{x}+\int {{E}_{D}[\left(y\left(\bm{x};D\right)-{E}_{D}\left[y\left(\bm{x};D\right)\right]\right)}^{2}]p\left(\bm{x}\right)d\bm{x}
$$

$$
={\left(bias\right)}^{2}+variance
$$

$$
\Rightarrow {E}_{\left(\bm{x},t\right)~D}\left[L\right]={\left(bias\right)}^{2}+variance+noise,\ bias\ {\propto}^{-1}\ variance
$$

*bias: the distance between predicted model and desired model*
||*model complexity*|*data storage*|
|-|------------------|--------------|
|*bias*|$\propto^{-1}$|$\propto$|
|*variance*|$\propto$|$\propto^{-1}$|
|*bias -variance*|$\propto$|$\propto^{-1}$|

*(1)control by number of basis functions*  
*(2)control by regularization multiplier*$\mathit{\lambda}$  
*lower *$\mathit{\lambda}$* tend to free weights so that model has richer representation capacity(low bias), but in the same time, numerous turbulance causes higher variance*
*higher *$\mathit{\lambda}$* tend to bound weights so that model has rigid representation capacity(high bias), but in the same time, numerous steady brings lower variance*  
***But a perfect model, always contains large number of basis function with matched regularization***  


***Linear function(Linear Hypothesis Space)***  

$$
y\left(\bm{x},\bm{w}\right)={w}_{0}{\mathit{\phi}}_{0}\left(\bm{x}\right)+{w}_{1}{\mathit{\phi}}_{1}\left(\bm{x}\right)+\dots +{w}_{M-1}{\mathit{\phi}}_{M-1}\left(\bm{x}\right)={\bm{w}}^{\bm{T}}\bm{\phi}\left(\bm{x}\right),\ {w}_{0}=b,{\mathit{\phi}}_{0}\left(\bm{x}\right)=1
$$

Assumption:genration of data

$$
y\left(\bm{x},\bm{w}\right)=t+\mathit{\epsilon},\mathit{\epsilon}~N\left(0,{\mathit{\beta}}^{-1}\right)
$$

Premise a conditional Gaussian distribution along the desired function ${y}^{\ast}\left(\bm{x},\bm{w}\right)$* with decaying confidence on the both sides of the function, so each sample will be treated as mean, which has maximal probability. (maximum likelihood estimation)*

$$
\Rightarrow p\left(t|\bm{x},\bm{w},\mathit{\beta}\right)=N\left(y\left(\bm{x},\bm{w}\right),{\mathit{\beta}}^{-1}\right)
$$

*That's why, we call *$\mathit{\beta}$* precision, a slack variable (like SVM) to avoid overfitting, or say,*
*a threshold controling convergence.*

$$
Target:\underset{\bm{w}}{\mathrm{argmin}}{E}_{\left(\bm{x},t\right)~D}\left[L\right]
$$

$$
optimal\ y\left(\bm{x}\right)=\int tp\left(t|\bm{x}\right)dt=E\left[t|\bm{x}\right]=y\left(\bm{x},\bm{w}\right)
$$

*under log-maxlikelihood*

$$
\underset{\bm{w}}{\mathrm{argmin}}{E}_{\left(\bm{x},t\right)~D}\left[L\right]=\underset{\bm{w}}{\mathrm{argmax}}{\sum}_{i=1}^{N}\mathrm{ln}p\left({t}^{\left(i\right)}|{\bm{x}}^{\left(\bm{i}\right)},\bm{w},\mathit{\beta}\right)
$$

$$
=\frac{N}{2}\mathrm{ln}\mathit{\beta}-\frac{N}{2}\mathrm{ln}\left(2\pi \right)-\frac{\mathit{\beta}}{2}{\sum}_{i=1}^{N}{\left({t}^{\left(i\right)}-y\left({\bm{x}}^{\left(\bm{i}\right)},\bm{w}\right)\right)}^{2}
$$

$$
\propto \underset{\bm{w}}{\mathrm{argmin}}\frac{1}{2}{\sum}_{i=1}^{N}{\left({t}^{\left(i\right)}-y\left({\bm{x}}^{\left(\bm{i}\right)},\bm{w}\right)\right)}^{2}
$$

*maximizing likelihood with regard to *$\bm{w}$ *is equivalent to minimizing L2 loss*

$$
{\nabla}_{\bm{w}}E={\sum}_{i=1}^{N}\left({t}^{\left(i\right)}-y\left({\bm{x}}^{\left(\bm{i}\right)},\bm{w}\right)\right){\bm{\phi}}^{\bm{T}}\left({\bm{x}}^{\left(\bm{i}\right)}\right)
$$

*(1) batch techniques : least square method*

$$
{\nabla}_{\bm{w}}E=0\Rightarrow {\mathbf{\Phi}}^{\bm{T}}\bm{t}={\mathbf{\Phi}}^{\bm{T}}\mathbf{\Phi}\bm{w}\Rightarrow {\bm{w}}_{ML}={\left({\mathbf{\Phi}}^{\bm{T}}\mathbf{\Phi}\right)}^{-1}{\mathbf{\Phi}}^{\bm{T}}\bm{t}
$$

$$
\mathbf{\Phi}=\left[\begin{array}{ccc}{\mathit{\phi}}_{0}\left({\bm{x}}^{\left(1\right)}\right)& \cdots & {\mathit{\phi}}_{M-1}\left({\bm{x}}^{\left(1\right)}\right)\\ \vdots & \ddots & \vdots \\ {\mathit{\phi}}_{0}\left({\bm{x}}^{\left(\bm{N}\right)}\right)& \cdots & {\mathit{\phi}}_{M-1}\left({\bm{x}}^{\left(\bm{N}\right)}\right)\end{array}\right]
$$

*By finding t's projection on space = *$span\left\{{\mathit{\phi}}_{k}\left(\bm{x}\right)\right\}$

$$
{\mathit{\beta}}_{ML}=\frac{1}{N}{\sum}_{i=1}^{N}{\left({t}^{\left(i\right)}-y\left({\bm{x}}^{\left(\bm{i}\right)},{\bm{w}}_{\bm{M}\bm{L}}\right)\right)}^{2}
$$

Note: when $\nexists \ {\left({\mathbf{\Phi}}^{\bm{T}}\mathbf{\Phi}\right)}^{-1},\ \bm{I}\ was\ introduced,\ so\ that\ \exists {\left({\mathbf{\Phi}}^{\bm{T}}\mathbf{\Phi}+\bm{I}\right)}^{-1}$

$$
{\bm{w}}_{ML}={\left({\mathbf{\Phi}}^{\bm{T}}\mathbf{\Phi}+\bm{I}\right)}^{-1}{\mathbf{\Phi}}^{\bm{T}}\bm{t}
$$

$$
corresponding\ to\ \ \frac{1}{2}{\sum}_{i=1}^{N}{\left({t}^{\left(i\right)}-y\left({\bm{x}}^{\left(\bm{i}\right)},\bm{w}\right)\right)}^{2}+\frac{\mathit{\lambda}}{2}{\bm{w}}^{\bm{T}}\bm{w},\mathit{\lambda}=\frac{\mathit{\alpha}}{\mathit{\beta}}
$$

*a *[*regularization*](onenote:#Regularization&section-id={206D0DBC-E353-4C40-ABB7-20922DEC5824}&page-id={74105814-BC3B-473C-908D-0AEB72711C85}&object-id={5DB304C5-ED6B-07BD-3264-4A7AC3D63882}&12&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/机器学习.one)* term was added*
*Note: In words co-occurence matrix, a assumption that each word at least appear once*
*was introduced, in case of dividing by zero*
*(2) sequential learning : gradient descent for each data point*

$$
{\bm{w}}^{\left(\bm{\tau}+1\right)}={\bm{w}}^{\left(\bm{\tau}\right)}-\mathit{\eta}{\nabla}_{{\bm{w}}^{\left(\bm{\tau}\right)}}{E}_{i}
$$

$$
={\bm{w}}^{\left(\bm{\tau}\right)}+\mathit{\eta}\left({t}^{\left(i\right)}-y\left({\bm{x}}^{\left(\bm{i}\right)},{\bm{w}}^{\left(\bm{\tau}\right)}\right)\right)\bm{\phi}\left({\bm{x}}^{\left(\bm{i}\right)}\right)
$$

*Support that promise sequential learning converge to *${\nabla}_{\bm{w}}E=0$

$$
\bm{X}=\left({\bm{x}}_{1},\dots ,{\bm{x}}_{\bm{N}}\right),p\left(\bm{X}\right)=\mathcal{N}\left(\bm{X}|\bm{\mu},\mathbf{\Sigma}\right)
$$

maximum likelihood estimation of ${\bm{\mu}}_{\bm{M}\bm{L}}$ *base on N observations*

$$
\frac{\mathit{\partial}}{\mathit{\partial}\bm{\mu}}\mathrm{ln}p\left(\bm{X}\right)=0\Rightarrow {\bm{\mu}}_{\bm{M}\bm{L}}^{\left(\bm{N}\right)}=\frac{1}{N}{\sum}_{n=1}^{N}{\bm{x}}_{\bm{n}}
$$

*convert to a sequential way*

$$
{\bm{\mu}}_{\bm{M}\bm{L}}^{\left(\bm{N}\right)}=\frac{1}{N}{\bm{x}}_{\bm{N}}+\frac{N-1}{N}{\bm{\mu}}_{\bm{M}\bm{L}}^{\left(\bm{N}-1\right)}
$$

$$
\ \ \ \ \ \ \ \ \ \ ={\bm{\mu}}_{\bm{M}\bm{L}}^{\left(\bm{N}-1\right)}+\frac{1}{N}\left({\bm{x}}_{\bm{N}}-{\bm{\mu}}_{\bm{M}\bm{L}}^{\left(\bm{N}-1\right)}\right)
$$

*Stochastic approximation*
*Robbins-Monro Algorithm (todo): a generalization of sequential way aforementioned*
*a sequential estimation to find root point for unknown function*

$$
{\mathit{\theta}}^{\left(N\right)}={\mathit{\theta}}^{\left(N-1\right)}+{a}_{N-1}z\left({\mathit{\theta}}^{\left(N-1\right)}\right)
$$

$$
subject\ to\ \left\{\begin{array}{c}E\left[{\left(z-f\right)}^{2}|\mathit{\theta}\right]<\infty \\ \underset{N\to \infty}{\mathrm{lim}}{a}_{N}=0\\ {\sum}_{N=1}^{\infty}{a}_{N}=\infty \\ {\sum}_{N=1}^{\infty}{a}_{N}^{2}<\infty \end{array}\right.
$$

$$
for\ f\left(\mathit{\theta}\right)\equiv E\left[z|\mathit{\theta}\right]=\int zp\left(z|\mathit{\theta}\right)dz
$$

and with goal to find$\ {\mathit{\theta}}^{\ast}\ that\ f\left({\mathit{\theta}}^{\ast}\right)=0$
In specific application is finding $\frac{\mathit{\partial}}{\mathit{\partial}\bm{\mu}}\mathrm{ln}p\left(\bm{X}\right)=0\ or\ {\nabla}_{\bm{w}}E=0$
*provide a support for convergence with probability one*  
***Bayesian Linear Regression***  
*To do what?: learning MAP on *$\bm{w}$

$$
p\left(\bm{w}|\bm{t}\right)\propto p\left(\bm{t}|\bm{w}\right)p\left(\bm{w}\right)
$$

Support idea: If two sets of variables are jointly Gaussian——[conjugate prior](https://towardsdatascience.com/conjugate-prior-explained-75957dc80bfb)
1. then the conditional distribution of one set conditioned on the other is again Gaussian, and **it's mean is a linear function of prior's mean**
2. the marginal distribution of either set is also Gaussian
Key-representation of proof:

$$
\bm{x}=\left(\begin{array}{c}{\bm{x}}_{\bm{a}}\\ {\bm{x}}_{\bm{b}}\end{array}\right),\bm{\mu}=\left(\begin{array}{c}{\bm{\mu}}_{\bm{a}}\\ {\bm{\mu}}_{\bm{b}}\end{array}\right),\mathbf{\Sigma}=\left(\begin{array}{c}{\mathbf{\Sigma}}_{\bm{a}\bm{a}}\ \ {\mathbf{\Sigma}}_{\bm{a}\bm{b}}\\ {\mathbf{\Sigma}}_{\bm{b}\bm{a}}\ \ {\mathbf{\Sigma}}_{\bm{b}\bm{b}}\end{array}\right),\mathbf{\Lambda}={\mathbf{\Sigma}}^{-1}=\left(\begin{array}{c}{\mathbf{\Lambda}}_{\bm{a}\bm{a}}\ \ {\mathbf{\Lambda}}_{\bm{a}\bm{b}}\\ {\mathbf{\Lambda}}_{\bm{b}\bm{a}}\ \ {\mathbf{\Lambda}}_{\bm{b}\bm{b}}\end{array}\right)
$$

*Property of determining the corresponding mean and covariance that any Gaussian distribution *$\mathcal{N}\left(\bm{x}|\bm{\mu},\mathbf{\Sigma}\right)$* can be written*

$$
-\frac{1}{2}{\left(\bm{x}-\bm{\mu}\right)}^{T}{\mathbf{\Sigma}}^{-1}\left(\bm{x}-\bm{\mu}\right)=-\frac{1}{2}{\bm{x}}^{\bm{T}}{\mathbf{\Sigma}}^{-1}\bm{x}+{\bm{x}}^{\bm{T}}{\mathbf{\Sigma}}^{-1}\bm{\mu}+const
$$

*Result:*
*Given a marginal Gaussian distribution and a conditional one*

$$
p\left(\bm{x}\right)=\mathcal{N}\left(\bm{x}|\bm{\mu},{\mathbf{\Lambda}}^{-1}\right)
$$

$$
p\left(\bm{y}|\bm{x}\right)=\mathcal{N}\left(\bm{y}|\bm{A}\bm{x}+\bm{b},{\bm{L}}^{-1}\right)
$$

*Yield the one switching on random variables*

$$
p\left(\bm{y}\right)=\mathcal{N}\left(\bm{y}|\bm{A}\bm{\mu}+\bm{b},{\bm{L}}^{-1}+\bm{A}{\mathbf{\Lambda}}^{-1}{\bm{A}}^{\bm{T}}\right)
$$

$$
p\left(\bm{x}|\bm{y}\right)=\mathcal{N}\left(\bm{x}|\mathbf{\Sigma}\left\{{\bm{A}}^{\bm{T}}\bm{L}\left(\bm{y}-\bm{b}\right)+\mathbf{\Lambda}\bm{\mu}\right\},\mathbf{\Sigma}\right)
$$

$$
\mathbf{\Sigma}={\left(\mathbf{\Lambda}+{\bm{A}}^{\bm{T}}\bm{L}\bm{A}\right)}^{-1}
$$


MAP estimation on $\bm{w}$  
Given

$$
prior:\ p\left(\bm{w}\right)=\mathcal{N}\left(\bm{w}|{\bm{m}}_0,{\bm{S}}_0\right)
$$

$$
likelihood:\ p\left(\bm{t}|\bm{w}\right)={\prod}_{n=1}^{N}\mathcal{N}\left({t}_{n}|{\bm{w}}^{\bm{T}}\bm{\phi}\left({\bm{x}}_{\bm{n}}\right),{\mathit{\beta}}^{-1}\right)
$$

*Yield*

$$
MAP:p\left(\bm{w}|\bm{t}\right)=\mathcal{N}\left(\bm{w}|{\bm{m}}_{\bm{N}},{\bm{S}}_{\bm{N}}\right)
$$

$$
{\bm{m}}_{\bm{N}}={\bm{S}}_{\bm{N}}\left({\bm{S}}_0^{-1}{\bm{m}}_0+\mathit{\beta}{\mathbf{\Phi}}^{\mathbf{T}}\bm{t}\right)
$$

$$
{\bm{S}}_{\bm{N}}^{-1}={\bm{S}}_0^{-1}+\mathit{\beta}{\mathbf{\Phi}}^{\bm{T}}\mathbf{\Phi}
$$

Relation to Maximum Likelihood estimation

$$
p\left(\bm{w}\right)=p\left(\bm{w}|\mathit{\alpha}\right)=\mathcal{N}\left(\bm{w}|0,{\mathit{\alpha}}^{-1}\bm{I}\right)
$$

$$
\mathit{\alpha}\to 0\Rightarrow {\bm{w}}_{\bm{M}\bm{A}\bm{P}}={\bm{m}}_{\bm{N}}\to {\bm{w}}_{\bm{M}\bm{L}}
$$

Predictive distribution: prediction of t for new values of $\bm{x}$

$$
p\left(t|\bm{x},\bm{t},\bm{X}\right)=\int p\left(t|\bm{w},\bm{x},\bm{X}\right)p\left(\bm{w}|\bm{t},\bm{x},\bm{X}\right)d\bm{w}=\mathcal{N}\left(t|{m}_{N}^{T}\bm{\phi}\left(\bm{x}\right),{\mathit{\sigma}}_{N}^{2}\left(\bm{x}\right)\right)
$$

  *proof: analogyous of*

$$
\left\{\begin{array}{c}p\left(t|\bm{w},\bm{x},\bm{X}\right)\to p\left(y|\bm{x}\right)\\ p\left(\bm{w}|\bm{t},\bm{x},\bm{X}\right)\to p\left(\bm{x}\right)\end{array}\right.
$$

$$
\Rightarrow p\left(t,\bm{w}|\bm{x},\bm{t},\bm{X}\right)\to p\left(\left(\bm{x},y\right)\right)
$$

$$
\Rightarrow p\left(t|\bm{x},\bm{t},\bm{X}\right)\to p\left(y\right)
$$

$$
{\mathit{\sigma}}_{N}^{2}\left(\bm{x}\right)=\frac{1}{\mathit{\beta}}+\bm{\phi}{\left(\bm{x}\right)}^{\bm{T}}{\bm{S}}_{\bm{N}}\bm{\phi}\left(\bm{x}\right),{\mathit{\sigma}}_{N}^{2}\left(\bm{x}\right)\to \frac{1}{\mathit{\beta}},N\to \infty 
$$

  *variance = noise + uncertainty of ****w***
  *which means, provided enough data, the prediction's variance will be*
  *converged as the variance of noise imposed on generation of data*
  *proof:*

$$
{\bm{S}}_{\bm{N}}^{-1}={\bm{S}}_{\bm{N}-1}^{-1}+\mathit{\beta}{\mathbf{\Phi}}^{\bm{T}}\mathbf{\Phi}={\bm{S}}_0^{-1}+\bm{N}\times \mathit{\beta}{\mathbf{\Phi}}^{\bm{T}}\mathbf{\Phi},\mathit{\beta}{\mathbf{\Phi}}^{\bm{T}}\mathbf{\Phi}>\left[0\right]
$$

$$
\Rightarrow \underset{N\to \infty}{\mathrm{lim}}{\bm{S}}_{\bm{N}}=\underset{N\to \infty}{\mathrm{lim}}{\left({\bm{S}}_0^{-1}+\bm{N}\times \mathit{\beta}{\mathbf{\Phi}}^{\bm{T}}\mathbf{\Phi}\right)}^{-1}=\left[0\right]
$$

  Note: when using Gaussian basis function, $\bm{\phi}{\left(\bm{x}\right)}^{\bm{T}}\bm{\phi}\left(\bm{x}\right)\to 0\ $ in region away from center, curve becomes randomly extrapolated, may cause overfitting problem.

*Training procedure*
1. Sample $\bm{w}$ from prior

$$
\bm{w}~\bm{p}\left(\bm{w}\right)=\mathcal{N}\left(\bm{w}|{\bm{m}}_0,{\bm{S}}_0\right)
$$

2. *Calculataion of likelihood, after observing a data point *$\left(\bm{x},t\right)$

$$
p\left(t|\bm{x},\bm{w}\right)=\mathcal{N}\left(t|{\bm{w}}^{\bm{T}}\bm{\phi}\left(\bm{x}\right),{\mathit{\beta}}^{-1}\right)
$$

*Note: it works in the same way with dozen data points*

$$
p\left(\bm{t}|\bm{x},\bm{w}\right)={\prod}_{n=1}^{M}\mathcal{N}\left({t}_{n}|{\bm{w}}^{\bm{T}}\bm{\phi}\left({\bm{x}}_{\bm{n}}\right),{\mathit{\beta}}^{-1}\right)
$$

3. *Calculation of MAP on *$\bm{w}$

$$
p\left(\bm{w}|t\right)=\frac{p\left(t|\bm{w}\right)p\left(\bm{w}\right)}{{\sum}_{{t}^{\prime}}p\left({t}^{\prime}|\bm{w}\right)p\left(\bm{w}\right)}
$$

*Note : Complex calculation can be eased by using conjugate prior*

$$
p\left(\bm{w}|t\right)=\mathcal{N}\left(\bm{w}|{\bm{m}}_{\bm{N}},{\bm{S}}_{\bm{N}}\right)
$$

$$
{\bm{m}}_{\bm{N}}={\bm{S}}_{\bm{N}}\left({\bm{S}}_{\bm{N}-1}^{-1}{\bm{m}}_{\bm{N}-1}+\mathit{\beta}{\mathbf{\Phi}}^{\mathbf{T}}\bm{t}\right)
$$

$$
{\bm{S}}_{\bm{N}}^{-1}={\bm{S}}_{\bm{N}-1}^{-1}+\mathit{\beta}{\mathbf{\Phi}}^{\bm{T}}\mathbf{\Phi}
$$

*And use it as prior on ****w ****on next iteration*

$$
\bm{p}\left(\bm{w}\right)\leftarrow p\left(\bm{w}|t\right)
$$

*go to step 1*
