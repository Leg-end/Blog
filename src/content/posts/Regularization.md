---
title: Regularization
published: 2023-03-23
description: "How does regularization work and what is it used for?"
tags: ["L1 decay", "L2 decay"]
category: Optimization
draft: false
---

*Bayes MAP on weights*  
*with an regularized term over weights : an introducion of prior knowledge on weights*

$$
p\left(\bm{w}|\mathit{\alpha}\right)=N\left(0,{\mathit{\alpha}}^{-1}\bm{I}\right)
$$

$$
p\left(\bm{w}|\bm{X},\bm{t},\mathit{\alpha},\mathit{\beta}\right)\propto p\left(\bm{t}|\bm{X},\bm{w},\mathit{\beta}\right)p\left(\bm{w}|\mathit{\alpha}\right),\bm{X}=\left\{{\bm{x}}^{\left(i\right)}\right\}
$$

*Note: In Neural Network, regularization on bias is not considerd, otherwise may cause under-fitting*
*Recall that Bayes classification turn into a max-min estimation when considering prior distribution. Same as regularization, wrapping original optimization problem into a max-min one.*

$$
\stackrel{~}{E}\left[\bm{w}\right]=E\left[\bm{w}\right]+\mathit{\alpha}\mathrm{\Omega}\left(\bm{w}\right)
$$

$$
\Rightarrow {\bm{w}}^{\ast}=\underset{\bm{w}}{\mathrm{argmin}}\underset{\mathit{\alpha},\mathit{\alpha}\ge 0}{\mathrm{max}}\stackrel{~}{E}\left[\bm{w}\right]
$$

*we may solve this formual by iterative optimization (like *[*SVM*](onenote:#SVM&section-id={206D0DBC-E353-4C40-ABB7-20922DEC5824}&page-id={11A9696D-1BFF-4700-8B1D-CF78A9E2CCFA}&object-id={CE2703F7-A70F-0F36-1E79-A95AB13D5E0D}&12&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/机器学习.one)* or EM), but may converge to local minimum*
*by fix *$\mathit{\alpha}$* to *${\mathit{\alpha}}^{\ast}$*, turn into constrained optimization problem*

$$
{\bm{w}}^{\ast}=\underset{\bm{w}}{\mathrm{argmin}}\left[E\left[\bm{w}\right]+{\mathit{\alpha}}^{\ast}\mathrm{\Omega}\left(\bm{w}\right)\right]
$$

*Q: why do we need regularization ?*
*Regularization is aim at reducing generalization error, or a trade-off between bias and variance.*
1) *Reducing overfitting (generalization error)*
2) *It is providing a premise for model, so when premise is satisfied with desired model, then the predicted model will converge to desired model : A→B, A true → B true. Or we can say, we are introducing some prior knowledge into model.*
3) [*Unbias hypothesis is useless*](onenote:#Machine%20Learning%20and%20Nerual%20Network&section-id={206D0DBC-E353-4C40-ABB7-20922DEC5824}&page-id={0120613B-6AA7-47C0-ABEE-002AB1B2FB47}&object-id={BA99CE90-478A-4536-B77E-0585FA97E540}&2B&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/机器学习.one)
4) *Numeric steady, benifical to optimization*
*Q: How does it work? Or what exectlly is the process of regularization*
*regularization: Weights adjusted by sepcific rules*
*By analysing weights' gradient including**** L2 regularization term***

$$
{\bm{w}}^{\left(\bm{\tau}+1\right)}={\bm{w}}^{\left(\bm{\tau}\right)}-\mathit{\eta}\left(\mathit{\lambda}\bm{w}+{\nabla}_{{\bm{w}}^{\left(\bm{\tau}\right)}}{E}_{i}\right)
$$

*weight with big value will get more punishment*
*Further, analyze relation between gradient on desired weights *${\bm{w}}^{\ast}$*without regularization and gradient on desired weights *$\stackrel{~}{\bm{w}}$* with regularization*

$$
{\bm{w}}^{\ast}=\underset{\bm{w}}{\mathrm{argmin}}E,{\nabla}_{{\bm{w}}^{\ast}}E=0
$$

do taylor quadratic approximation on ${\bm{w}}^{\ast}$, without regularization term

$$
\widehat{E}\left[\bm{w}\right]=E\left[{\bm{w}}^{\ast}\right]+\frac{1}{2}{\left(\bm{w}-{\bm{w}}^{\ast}\right)}^{\bm{T}}\bm{H}\left(\bm{w}-{\bm{w}}^{\ast}\right),\bm{H}\ is\ positive\ semi-define
$$

$$
{\nabla}_{{\bm{w}}^{\ast}}\widehat{E}=\bm{H}\left(\bm{w}-{\bm{w}}^{\ast}\right)=0
$$

$$
\mathit{\alpha}\stackrel{~}{\bm{w}}+\bm{H}\left(\stackrel{~}{\bm{w}}-{\bm{w}}^{\ast}\right)=0
$$

$$
\Rightarrow \stackrel{~}{\bm{w}}={\left(\mathit{\alpha}\bm{I}+\bm{H}\right)}^{-1}\bm{H}{\bm{w}}^{\ast},\bm{H}={\bm{Q}}^{\bm{T}}\mathbf{\Lambda}\bm{Q}
$$

$$
\Rightarrow \stackrel{~}{\bm{w}}=\bm{Q}{\left(\mathit{\alpha}\bm{I}+\mathbf{\Lambda}\right)}^{-1}\mathbf{\Lambda}{\bm{Q}}^{\bm{T}}{\bm{w}}^{\ast}
$$

$$
\Rightarrow {\stackrel{~}{w}}_{i}=\frac{{\mathit{\lambda}}_{i}}{{\mathit{\lambda}}_{i}+\mathit{\alpha}}{w}_{i}^{\ast},\ regularization\ rule
$$

*if *${\mathit{\lambda}}_{i}\gg \mathit{\alpha}\Rightarrow {\stackrel{~}{w}}_{i}\to {w}_{i}^{\ast}$
*since weight aligned with large eigenvalue in ****H**** contributes most to gradient,*
*it's better keep it still*
*if *${\mathit{\lambda}}_{i}\ll \mathit{\alpha}\Rightarrow {\stackrel{~}{w}}_{i}\to 0$
*since weight aligned with small eigenvalue in ****H**** contributes almost nothing to gradient,*
*it will decay by regularization*
*Same way on L1 regularization will get *${\stackrel{~}{w}}_{i}=\frac{{\mathit{\lambda}}_{i}}{{\mathit{\lambda}}_{i}+\frac{\mathit{\alpha}}{\left|{\stackrel{~}{w}}_{i}\right|}}{w}_{i}^{\ast},$provided H is diagnal (data has been PCA), which doesn^′ t have clean algebraic solution

$$
\stackrel{~}{E}\left[\bm{w}\right]=\mathit{\alpha}{\left|\left|\bm{w}\right|\right|}_{1}+E\left[\bm{w}\right],{\nabla}_{{\bm{w}}^{\ast}}\stackrel{~}{E}=\mathit{\alpha}\bm{s}\bm{i}\bm{g}\bm{n}{\left({\bm{w}}^{\ast}\right)}^{\bm{T}}
$$

do taylor quadratic approximation for $\stackrel{~}{E}$ on ${\bm{w}}^{\ast}$

$$
\widehat{E}\left[\bm{w}\right]=\stackrel{~}{E}\left[{\bm{w}}^{\ast}\right]+\mathit{\alpha}\bm{s}\bm{i}\bm{g}\bm{n}{\left({\bm{w}}^{\ast}\right)}^{\bm{T}}\left(\bm{w}-{\bm{w}}^{\ast}\right)+\frac{1}{2}{\left(\bm{w}-{\bm{w}}^{\ast}\right)}^{\bm{T}}\bm{H}\left(\bm{w}-{\bm{w}}^{\ast}\right),\bm{H}=\bm{d}\bm{i}\bm{a}\bm{g}\left[{H}_{i,i}\right]
$$

$$
\widehat{E}\left[\bm{w}\right]=E\left[{\bm{w}}^{\ast}\right]+\mathit{\alpha}\bm{s}\bm{i}\bm{g}\bm{n}{\left({\bm{w}}^{\ast}\right)}^{\bm{T}}{\bm{w}}^{\ast}+\mathit{\alpha}\bm{s}\bm{i}\bm{g}\bm{n}{\left({\bm{w}}^{\ast}\right)}^{\bm{T}}\left(\bm{w}-{\bm{w}}^{\ast}\right)+\frac{1}{2}{\left(\bm{w}-{\bm{w}}^{\ast}\right)}^{\bm{T}}\bm{H}\left(\bm{w}-{\bm{w}}^{\ast}\right)
$$

$$
\ \ \ \ \ \ \ \ \ \ \ =E\left[{\bm{w}}^{\ast}\right]+\mathit{\alpha}\bm{s}\bm{i}\bm{g}\bm{n}{\left({\bm{w}}^{\ast}\right)}^{\bm{T}}\bm{w}+\frac{1}{2}{\left(\bm{w}-{\bm{w}}^{\ast}\right)}^{\bm{T}}\bm{H}\left(\bm{w}-{\bm{w}}^{\ast}\right)
$$

$$
\ \ \ \ \ \ \ \ \ \ \ =E\left[{\bm{w}}^{\ast}\right]+{\sum}_{i}\left[\frac{1}{2}{H}_{i,i}{\left({w}_{i}-{w}_{i}^{\ast}\right)}^{2}+\mathit{\alpha}sign\left({w}_{i}^{\ast}\right){w}_{i}\right]
$$

Solve $\underset{\bm{w}}{\mathrm{argmin}}\widehat{E}\left[\bm{w}\right]\ $ by each dimension i

$$
set\ f\left({w}_{i}\right)=\frac{1}{2}{H}_{i,i}{\left({w}_{i}-{w}_{i}^{\ast}\right)}^{2}+\mathit{\alpha}sign\left({w}_{i}^{\ast}\right){w}_{i},{w}_{i}\ne 0
$$

$$
\frac{df}{d{w}_{i}}={H}_{i,i}\left({w}_{i}-{w}_{i}^{\ast}\right)+\mathit{\alpha}sign\left({w}_{i}^{\ast}\right)=0
$$

$$
\Rightarrow {w}_{i}={w}_{i}^{\ast}-\frac{\mathit{\alpha}}{{H}_{i,i}}sign\left({w}_{i}^{\ast}\right)=sign\left({w}_{i}^{\ast}\right)\left(\left|{w}_{i}^{\ast}\right|-\frac{\mathit{\alpha}}{{H}_{i,i}}\right)
$$

$$
\Rightarrow {w}_{i}=sign\left({w}_{i}^{\ast}\right)\mathrm{max}\left(\left|{w}_{i}^{\ast}\right|-\frac{\mathit{\alpha}}{{H}_{i,i}},0\right)\ or\ 
$$

$$
\Rightarrow {w}_{i}=sign\left({w}_{i}^{\ast}\right)\mathrm{max}\left(\left|{w}_{i}^{\ast}\right|-\frac{\mathit{\alpha}}{{\mathit{\lambda}}_{i}},0\right)
$$

*if *${\mathit{\lambda}}_{i}\gg \mathit{\alpha}\Rightarrow {w}_{i}\to {w}_{i}^{\ast}$
*since weight aligned with large eigenvalue in ****H**** contributes most to gradient,*
*it's better keep it still*
*if *${\mathit{\lambda}}_{i}\ll \mathit{\alpha}\Rightarrow {\stackrel{~}{w}}_{i}=0$
*since weight aligned with small eigenvalue in ****H**** contributes almost nothing to gradient,*
*it will directly pressed to 0, leading to a sparse solution*
*Same as L2 regularization correspond to**** Gaussian prior**** on weights, L1 regularization*
*is to the log-form of ****isotropic Laplace prior**** over weights*

$$
\mathrm{log}p\left(\bm{w}\right)={\sum}_{i}\mathrm{log}Laplace\left({w}_{i};0,\frac{1}{\mathit{\alpha}}\right)=-\mathit{\alpha}{\left|\left|\bm{w}\right|\right|}_{1}+n\mathrm{log}\mathit{\alpha}-n\mathrm{log}2
$$

