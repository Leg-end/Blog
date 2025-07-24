---
title: SVM
published: 2023-03-13
description: "Introduction to Support Vector Machine"
tags: ["Sperable Hyperplane", "Slacking"]
category: Classification
draft: false
---

**Problem&Analysis**  
Provided with two linearly separable datasets, we need to find a hyperplane that exactly divide them apart. i.e. a hyperplane is required that both side of data points are away from it at reverse direction, according to **strict separable hyperplane therom**:

$$
\mathcal{X}=\mathrm{C}\cup D
$$

$$
C\cap D=\varnothing ,\ \exists w\ne 0,\ b\Rightarrow \left\{\begin{array}{c}{w}^{T}x+b<0,\ \forall x\in C\\ {w}^{T}z+b>0,\ \forall z\in D\end{array}\right.,\ l:\left\{x|{w}^{T}x+b=0\right\}
$$

These strict inequalities are not powerful enough in finding desired hyperplane, Since we can get infinity hyperplanes meet the requirements, but any local solution may not lead to good generalization, so we can turn to an equivalent easier one, this is equivalent to induce regularization.
Note that that also has an explanation from [Lagrange Method](onenote:#Preliminary&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={FC3FD93B-B8A9-4DAE-B196-0E6AE03017A3}&object-id={7A3C25D5-B74D-0EE0-39CF-E4E230C10B73}&68&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one), where strict inequality constraints are **inactive** in finding optimal, so we need **active** constraints, i.e. equality constraints.
according to **supporting hyperplane theorem**:

$$
convC\cap convD=\varnothing \Rightarrow \left\{\begin{array}{c}{w}_{C}x\le {w}_{C}{x}_{0},\ \forall x\in convC,{l}_{C}:\left\{x|{w}_{C}^{T}x={w}_{C}^{T}{x}_{0}\right\}\\ {w}_{D}z\le {w}_{D}{z}_{0},\ \forall z\in convD,{l}_{D}:\left\{x|{w}_{D}^{T}x={w}_{D}^{T}{x}_{0}\right\}\end{array}\right.
$$

   ${x}_{0},{z}_{0}$ are support points of C and D, respectively
   ${l}_{C},{l}_{D}$ are support hyperplanes of C and D, respectively, ${w}_{C}\parallel {w}_{D}\parallel w$
  in such way, we can say $l$ is the support hyperplane both for C,D, with margin
So when support points are far enough away from $l$, so are the rest points

$$
\left\{\begin{array}{c}d\left(x,l\right)\ge d\left({x}_{0},l\right),\ \forall x\in C\\ d\left(z,l\right)\ge d\left({z}_{0},l\right),\ \forall z\in D\end{array}\right.,\ set\ margin\equiv \underset{x\in \mathcal{X}}{\mathrm{min}}d(x,l)
$$

And margins from both sides reach maximum when they are equal

$$
d\left({x}_{0},l\right)=d\left({z}_{0},l\right)=a\Rightarrow \forall x\in \mathcal{X},d\left(x,l\right)\ge a
$$

Now it's more easy to find our desired hyperplane $l$, which only need to meet few requirements:

$$
\left\{\begin{array}{c}d\left({x}_{0},l\right)=d\left({z}_{0},l\right)=a\\ \forall x\in \mathcal{X},d\left(x,l\right)\ge a\end{array}\right.\Rightarrow \underset{w,b}{\mathrm{argmax}}\left\{\underset{x\in \mathcal{X}}{\mathrm{min}}d(x,l)\right\}
$$

***Ideas behind***  
1. ***Find equivalent easier problem***
2. ***Meet the requirements that solve it***

**Analogy**  
It's bit of taste of KNN, which makes decision based on instances. While SVM only depends on support vectors to make decision.
They both use a **kernel function** to measure similarity between new data and support data, more specificly:
Note: you can take kernel function as a metric function, but in kernel-specific feature space. (In that way you can also treat it as a tranformation between feature spaces)
KNN, kernel function(new data, all data)
SVM, kernel function(new data, support vectors)
  actually, when using radial basis function as kernel fucntion, the number of support vectors is in positive relevance with the value of sigma. And once sigma is small enough, SVM will degenerate to KNN

**Adaptation**  
hyperplane $\left\{\bm{x}\right|f\left(\bm{x}\right)={\bm{w}}^{T}\mathit{\phi}\left(\bm{x}\right)+b=0\}$

$$
margin\ :\ \mathrm{distance}\ \mathrm{of}\ \mathrm{point}\ \mathrm{to}\ \mathrm{hyperplane}\text{'}\mathrm{s}\ \mathrm{pependicular}\ \mathrm{line}\ 
$$

$$
d\left(x,l\right)=\ \frac{\left|f\left(\bm{x}\right)\right|}{\left|\left|\bm{w}\right|\right|}
$$

$$
geometry\ margin\ :\ \frac{y\cdot\left(x\right)}{\left|\left|w\right|\right|},y\in \left\{-1,1\right\}
$$

$$
\exists \bm{w},b,\ \ \forall \left({\bm{x}}_{n},{y}_{n}\right)\in X,\ f\left({\bm{x}}_{n}\right)\left\{\begin{array}{c}>0,{y}_{n}=+1\\ <0,{y}_{n}=-1\end{array}\right.
$$

  In that case, any point far away from hyperplane, $y\cdot\left(\bm{x}\right)$ will be huge number and $y\cdot\left(\bm{x}\right)>0$

**Optimization**  

$$
\underset{\bm{w},b}{\mathrm{argmax}}\left\{\frac{1}{\left|\left|\bm{w}\right|\right|}\underset{n}{\mathrm{min}}\left({y}_{n}\cdot\left({\bm{x}}_{n}\right)\right)\right\}
$$

1. Decouple it

$$
\frac{\underset{n}{min}\left({y}_{n}\cdot\left({\bm{x}}_{n}\right)\right)}{\left|\left|\bm{w}\right|\right|}=d\Rightarrow \underset{n}{min}\left({y}_{n}\cdot\left({\bm{x}}_{n}\right)\right)=d\left|\left|\bm{w}\right|\right|=\mathit{\delta}
$$

since rescaling parameters won't change margin, we can use this freedom to ease the unknown d in SV's definition
set 

$$
\bm{w}\to \frac{\bm{w}}{\mathit{\delta}},\ b\to \frac{b}{\mathit{\delta}}\Rightarrow \underset{n}{\mathrm{min}}\left({y}_{n}\cdot\left({\bm{x}}_{n}\right)\right)=1,\ \left|\left|\bm{w}\right|\right|\to \frac{\left|\left|\bm{w}\right|\right|}{\mathit{\delta}}
$$

$$
\Rightarrow \ \forall {\bm{x}}_{n}\in \mathcal{X},{y}_{n}\cdot\left({\bm{x}}_{n}\right)\ge 1,\ n=1,\dots ,N
$$

$$
\underset{\bm{w},b}{\mathrm{argmax}}\left\{\frac{1}{\left|\left|\bm{w}\right|\right|}\underset{n}{\mathrm{min}}\left({y}_{n}\cdot\left({\bm{x}}_{n}\right)\right)\right\}\equiv \underset{\bm{w},b}{\mathrm{argmin}}\frac{1}{2}{\left|\left|\bm{w}\right|\right|}^{2}
$$

$$
subject\ to\ {y}_{n}\cdot\left({\bm{x}}_{n}\right)\ge 1
$$

2. Optimize it
1) use Lagrange multipliers, $\bm{a}=\left({a}_{1},\dots ,{a}_{N}\right)\ge {\left[0\right]}_{N}$

$$
L\left(\bm{w},b,\bm{a}\right)=\frac{1}{2}{\left|\left|\bm{w}\right|\right|}^{2}-{\sum}_{n=1}^{N}{a}_{n}\left\{{y}_{n}\cdot\left({\bm{x}}_{n}\right)-1\right\}
$$

*Note:*
a) *the minus sign in front of *$\bm{a}$* is due to *$\nabla f=\mathit{\lambda}\nabla g$
 $\nabla f,\nabla g$ have oppsite direction
b) the formula tells that the norm of parameters will not be penalized when points far from plane, but they will be if their norm is huge or when points are close to the plane, which results in maximizing on margin.

$$
By\frac{\mathit{\partial}L}{\mathit{\partial}\bm{w}}=\frac{\mathit{\partial}L}{\mathit{\partial}b}=0
$$

$$
\bm{w}={\sum}_{n=1}^{N}{a}_{n}{y}_{n}\mathit{\phi}\left({\bm{x}}_{n}\right),\ {\sum}_{n=1}^{N}{a}_{n}{y}_{n}=0
$$

$$
\Rightarrow L\left(\bm{a}\right)={\sum}_{n=1}^{N}{a}_{n}-\frac{1}{2}{\sum}_{n=1}^{N}{\sum}_{m=1}^{N}{a}_{n}{a}_{m}{y}_{n}{y}_{m}k\left({\bm{x}}_{n},{\bm{x}}_{m}\right)
$$

$$
\ \ \ \ \ \ k\left({\bm{x}}_{n},{\bm{x}}_{m}\right)={\bm{\phi}}^{\bm{T}}\left({\bm{x}}_{n}\right)\bm{\phi}\left({\bm{x}}_{m}\right),\ kernel\ function
$$

$$
\ \ \ \ \ \ subject\ to\ {a}_{n}\ge 0,\ n=1,\dots ,N\ \ and\ {\sum}_{n=1}^{N}{a}_{n}{y}_{n}=0
$$

2）after solving $L\left(\bm{a}\right)$, update a and w, so as to update b by support vectors

$$
f\left(\bm{x}\right)={\left({\sum}_{n=1}^{N}{a}_{n}{y}_{n}\bm{\phi}\left({\bm{x}}_{n}\right)\right)}^{T}\bm{\phi}\left(\bm{x}\right)+b
$$

$$
\ \ \ \ \ \ \ \ \ \ ={\sum}_{n=1}^{N}{a}_{n}{y}_{n}k\left(\bm{x},{\bm{x}}_{\bm{n}}\right)+b,subject\ to\ {y}_{n}\cdot\left({\bm{x}}_{n}\right)\ge 1
$$

With KKT conditions:$\ \ \left\{\begin{array}{c}{a}_{n}\ge 0\\ {y}_{n}\cdot\left({\bm{x}}_{n}\right)-1\ge 0\\ {a}_{n}\left({y}_{n}\cdot\left({\bm{x}}_{n}\right)-1\right)=0\end{array}\right.$  
if ${a}_{n}=0\ $  
${x}_{n}$ contributes nothing to $f\left(x\right)$'s predictions
if ${a}_{n}>0\Rightarrow {y}_{n}\cdot\left({\bm{x}}_{n}\right)-1=0$
  only support vectors contribute $f\left(x\right)$*'s *predictions

$$
{y}_{n}\left({\sum}_{\bm{m}=1}^{\left|S\right|}{a}_{m}{y}_{m}k\left({\bm{x}}_{\bm{n}},{\bm{x}}_{\bm{m}}\right)+b\right)=1,\ for\ ({x}_{n},{y}_{n})\in S
$$

$$
\Rightarrow b=\frac{1}{\left|S\right|}{\sum}_{n=1}^{\left|S\right|}\left({y}_{n}-{\sum}_{\bm{m}=1}^{\left|S\right|}{a}_{m}{y}_{m}k\left({\bm{x}}_{n},{\bm{x}}_{m}\right)\right)
$$

**Overlapping Class Distribution**  
**Problem&Analysis**  
Similar to Bayes classifier, class-conditional distribution may overlap,i.e. datasets are not 100% separable.
![](image_1.5fa7aa72.jpg)
In that case, an exact separation on the training data may lead to poor generalization. Therefore behavior of misclassifying must be allowed.
equivalent to ($E\left[Loss\right]={\left(bias\right)}^{2}\downarrow +var\uparrow +noise$)
If we still use a hyperplane to separate it, then will results each side has data points assign to its counter part.

$$
C\cap D\ne \varnothing 
$$

$$
set\left\{\begin{array}{c}{D}_{miss}=\left\{z\in D,\ {w}^{T}z+b<0\ \right\}\\ {C}_{miss}=\left\{x\in C,\ {w}^{T}x+b>0\right\}\end{array}\right.
$$

If we allow missclassification, then we can get new separable sets

$$
{C}^{\prime}=C-{C}_{miss}+{D}_{miss}
$$

$$
{D}^{\prime}=D-{D}_{miss}+{C}_{miss}
$$

$$
\mathcal{X}=C\cup D={C}^{\prime}\cup {D}^{\prime}
$$

and

$$
{C}^{\prime}\cap {D}^{\prime}=\varnothing ,\ \exists w\ne 0,\ b\Rightarrow \left\{\begin{array}{c}{w}^{T}x+b\le 0,\ \forall x\in {C}^{\prime}\\ {w}^{T}z+b\ge 0,\ \forall z\in {D}^{\prime}\end{array}\right.,l:\left\{x|{w}^{T}x+b=0\right\}
$$

Now we return to non-overlap case, but how can we find the support points?
We already know the support points can be simplify as

$$
\frac{\underset{x\in \mathcal{X}}{\mathrm{min}}d\left(x,\ l\right)}{a}=1\Rightarrow \underset{x\in \mathcal{X}}{\mathrm{min}}d\left(x,\frac{l}{a}\right)=1,\ and\ \forall x\in \mathcal{X},\ d\left(x,\frac{l}{a}\right)\ge 1
$$

But for overlap condition, we have
Points inside margin: $\exists x\in \mathcal{X},0<\mathrm{d}\left(x,\frac{l}{a}\right)<1$
Points missclassified: $\exists x\in {C}_{miss}\cup {D}_{miss}\ ,-1<\ d\left(x,\frac{l}{a}\right)<0$
*Note: for missclassified point, its y has opposite sign to its margin, leading to negative geometry margin*
They both have distance to supporting hyperplane

$$
{\mathit{\xi}}_{n}=1-d\left({x}_{n},\frac{l}{a}\right)
$$

Inspired by the way that altering inequlity constraint into equility one:

$$
g\left(x\right)\ge c\Rightarrow g\left(x\right)-\mathit{\xi}=0,\mathit{\xi}\ge 0
$$

 $\mathit{\xi}$ is called "**slack variable**"
By introducing a slack variables for each point, played as an offset so as to meet the support points constraint, i.e.

$$
\forall {x}_{n}\in \mathcal{X},\ d\left({x}_{n},\frac{l}{a}\right)+{\mathit{\xi}}_{n}\ge 1,{\mathit{\xi}}_{n}=\left\{\begin{array}{c}0,d\left({x}_{n},\frac{l}{a}\right)>1\\ 1-{y}_{n}f\left({\bm{x}}_{\bm{n}}\right),-1<d\left({x}_{n},\frac{l}{a}\right)<1\end{array}\right.
$$

In other words, we pull all points on the wrong side of margin back to margin, and treat them as support points. Now we can solve it in the old way, plus with a new requirement that the separation must has as less missclassified points as possible

$$
\underset{l}{\mathrm{min}}\left|{C}_{miss}+{D}_{miss}\right|\propto \underset{l}{\mathrm{min}}{\sum}_{n}{\mathit{\xi}}_{n},\ for\ \left|{C}_{miss}+{D}_{miss}\right|<{\sum}_{n}{\mathit{\xi}}_{n}\ 
$$

**Adaptation**  

$$
{\mathit{\xi}}_{n}=\left\{\begin{array}{c}0,\ \ \ {y}_{n}f\left({\bm{x}}_{\bm{n}}\right)-1\ge 0\\ \left|{y}_{n}-f\left({\bm{x}}_{\bm{n}}\right)\right|,\ \ {y}_{n}f\left({\bm{x}}_{\bm{n}}\right)-1<0\end{array}\right.
$$

$$
\Rightarrow \left\{\begin{array}{c}{y}_{n}=1\ \left\{\begin{array}{c}0<f\left({x}_{n}\right)<1\Rightarrow 0<{\mathit{\xi}}_{n}<1\\ f\left({x}_{n}\right)<0\Rightarrow {\mathit{\xi}}_{n}>1(misclassified\ {y}_{n}\ to\ -1)\end{array}\right.\\ {y}_{n}=-1\ \left\{\begin{array}{c}0<f\left({x}_{n}\right)<1\Rightarrow {\mathit{\xi}}_{n}>1(misclassified\ {y}_{n}\ to\ 1)\\ f\left({x}_{n}\right)<0\Rightarrow 0<{\mathit{\xi}}_{n}<1\end{array}\right.\end{array}\right.
$$

*for each data, once *${y}_{n}f\left({\bm{x}}_{\bm{n}}\right)-1<0$*, means it fall inside the margin, then its class will be decided jointly with *${\mathit{\xi}}_{n}$
*also, penalty for misclassification increases linearly with *$\mathit{\xi}$

$$
\underset{\bm{w},b}{\mathrm{argmin}}\left[\frac{1}{2}{\left|\left|\bm{w}\right|\right|}^{2}+C{\sum}_{n=1}^{N}{\mathit{\xi}}_{n}\right],C>0\ 
$$

$$
subject\ to\ {y}_{n}\cdot\left({\bm{x}}_{n}\right)\ge 1-{\mathit{\xi}}_{n},\ \ {\mathit{\xi}}_{n}\ge 0
$$

use Lagrange multipliers, $\bm{a}=\left({a}_{1},\dots ,{a}_{N}\right)\ge {\left[0\right]}_{N},\bm{\mu}=\left({\mathit{\mu}}_{1},\dots ,{\mathit{\mu}}_{N}\right)\ge {\left[0\right]}_{N}$

$$
L\left(\bm{w},b,\bm{a},\bm{\mu},\bm{\xi}\right)=\frac{1}{2}{\left|\left|\bm{w}\right|\right|}^{2}+C{\sum}_{n=1}^{N}{\mathit{\xi}}_{n}-{\sum}_{n=1}^{N}{a}_{n}\left\{{y}_{n}\cdot\left({\bm{x}}_{n}\right)-1+{\mathit{\xi}}_{n}\right\}-{\sum}_{n=1}^{N}{\mathit{\mu}}_{n}{\mathit{\xi}}_{n}
$$

*With KKT conditions*$\ \ \left\{\begin{array}{c}{a}_{n}\ge 0\\ {y}_{n}\cdot\left({\bm{x}}_{n}\right)-1+{\mathit{\xi}}_{n}\ge 0\\ {a}_{n}\left({y}_{n}\cdot\left({\bm{x}}_{n}\right)-1+{\mathit{\xi}}_{n}\right)=0\\ {\mathit{\mu}}_{n}\ge 0\\ {\mathit{\xi}}_{n}\ge 0\\ {\mathit{\mu}}_{n}{\mathit{\xi}}_{n}=0\end{array}\right.\ by\ $*derivativing*

$$
\Rightarrow L\left(\bm{a}\right)={\sum}_{n=1}^{N}{a}_{n}-\frac{1}{2}{\sum}_{n=1}^{N}{\sum}_{m=1}^{N}{a}_{n}{a}_{m}{y}_{n}{y}_{m}k\left({\bm{x}}_{n},{\bm{x}}_{m}\right)
$$

$$
subject\ to\ 0\le {a}_{n}\le C,\ n=1,\dots ,N\ \ and\ {\sum}_{n=1}^{N}{a}_{n}{y}_{n}=0
$$

$$
f\left(\bm{x}\right)={\left({\sum}_{n=1}^{N}{a}_{n}{y}_{n}\bm{\phi}\left({\bm{x}}_{n}\right)\right)}^{T}\bm{\phi}\left(\bm{x}\right)+b
$$

$$
\ \ \ \ \ \ \ \ \ \ ={\sum}_{n=1}^{N}{a}_{n}{y}_{n}k\left(\bm{x},{\bm{x}}_{n}\right)+b,subject\ to\ {y}_{n}\cdot\left({\bm{x}}_{n}\right)\ge 1-{\mathit{\xi}}_{n}
$$

With KKT conditions $\ \ \left\{\begin{array}{c}0\le {a}_{n}\le C\\ {a}_{n}=C-{\mathit{\mu}}_{n}\\ {y}_{n}\cdot\left({\bm{x}}_{n}\right)-1+{\mathit{\xi}}_{n}\ge 0\\ {a}_{n}\left({y}_{n}\cdot\left({\bm{x}}_{n}\right)-1+{\mathit{\xi}}_{n}\right)=0\\ {\mathit{\mu}}_{n}\ge 0\\ {\mathit{\xi}}_{n}\ge 0\\ {\mathit{\mu}}_{n}{\mathit{\xi}}_{n}=0\end{array}\right.$

$$
\Rightarrow \left\{\begin{array}{c}{a}_{n}=0\Rightarrow {\mathit{\xi}}_{n}=0\Rightarrow {y}_{n}f\left({x}_{n}\right)\ge 1\\ 0<{a}_{n}<C\Rightarrow {\mathit{\xi}}_{n}=0\Rightarrow {y}_{n}f\left({x}_{n}\right)=1\\ {a}_{n}=C\Rightarrow {\mathit{\xi}}_{n}\ge 0\Rightarrow {y}_{n}f\left({x}_{n}\right)\le 1\end{array}\right.
$$

if ${a}_{n}=0\ \ $  
$\ \ \ \ \ \ \ \ {x}_{n}$ contributes nothing to $f\left(x\right)$'s predictions  
if $\ {a}_{n}>0\Rightarrow {y}_{n}\cdot\left({\bm{x}}_{n}\right)-1+{\mathit{\xi}}_{n}=0\Rightarrow {y}_{n}\cdot\left({\bm{x}}_{n}\right)\ge 1$  
data points satisfy the constraint forming support vectors and contribute $f\left(x\right)$'s predictions

$$
S=\left\{\left({x}_{n},{y}_{n}\right)|{a}_{n}>0\right\}
$$

if ${a}_{n}<C\Rightarrow {\mathit{\mu}}_{n}>0\Rightarrow {\mathit{\xi}}_{n}=0\Rightarrow {y}_{n}\cdot\left({\bm{x}}_{n}\right)=1$
data points on the margin contribute $f\left(x\right)$'s predictions  
if ${a}_{n}=C\Rightarrow {\mathit{\mu}}_{n}=0\Rightarrow {\mathit{\xi}}_{n}\ge 0\Rightarrow {y}_{n}\cdot\left({\bm{x}}_{n}\right)\le 1$
  Contribute $f\left(x\right)$'s predictions  
if $0\le {\mathit{\xi}}_{n}\le 1\ $ correctly classified  
if ${\mathit{\xi}}_{n}>1$ missclassified

Base on ${y}_{n}\cdot\left({\bm{x}}_{n}\right)=1$

$$
y_n \left( \sum_{m=1}^{|S_{0<a<C}|} a_m y_m k(\bm{x}_n, \bm{x}_m) + b \right) = 1, \quad \text{for } (x_n, y_n) \in S_{0<a<C}
$$

$$
\Rightarrow b = \frac{1}{|S_{0<\bm{a}<\bm{C}}|} \sum_{n=1}^{|S_{0<\bm{a}<\bm{C}}|} \left( y_n - \sum_{m=1}^{|S_{0<\bm{a}<\bm{C}}|} a_m y_m k(\bm{x}_n, \bm{x}_m) \right)
$$


**Relation to logistic regression**  
1. *Loss function*
since penaly grow linearly with $\mathit{\xi}$

$$
{\mathit{\xi}}_{n}=\left\{\begin{array}{c}0,\ \ \ {y}_{n}f\left({\bm{x}}_{n}\right)\ge 1\\ 1-{y}_{n}f\left({\bm{x}}_{n}\right),\ \ {y}_{n}f\left({\bm{x}}_{\bm{n}}\right)<1\end{array}\right.={\left[1-{y}_{n}f\left({\bm{x}}_{n}\right)\right]}_{+}
$$

proof:

$$
{\mathit{\xi}}_{n}=\left|{y}_{n}-f\left({\bm{x}}_{n}\right)\right|,\ when\ {y}_{n}f\left({\bm{x}}_{n}\right)<1
$$

When ${y}_{n}=1$

$$
{\mathit{\xi}}_{n}=\left|1-1\ast f\left({\bm{x}}_{n}\right)\right|=1-{y}_{n}f\left({x}_{n}\right)
$$

When ${y}_{n}=-1$

$$
{\mathit{\xi}}_{n}=\left|-1-f\left({\bm{x}}_{n}\right)\right|=\left|1+f\left({\bm{x}}_{\bm{n}}\right)\right|=\left|1-\left(-1\right)f\left({\bm{x}}_{n}\right)\right|=1-{y}_{n}f\left({\bm{x}}_{n}\right)
$$

Note ${\mathit{\xi}}_{n}={y}_{n}^{2}-{y}_{n}f\left({\bm{x}}_{n}\right)={y}_{n}\left({y}_{n}-f\left({\bm{x}}_{n}\right)\right)$

$$
\underset{\bm{w},b}{\mathrm{argmin}}\left[\frac{1}{2}{\left|\left|\bm{w}\right|\right|}^{2}+C{\sum}_{n=1}^{N}{\mathit{\xi}}_{n}\right],C>0\ turn\ into
$$

$$
\frac{1}{2}{\left|\left|\bm{w}\right|\right|}^{2}+C{\sum}_{n=1}^{\left|{S}_{sv}\right|}{\left[1-{y}_{n}f\left({\bm{x}}_{n}\right)\right]}_{+}
$$

$$
={\sum}_{n=1}^{\left|{S}_{sv}\right|}{\left[1-{y}_{n}f\left({\bm{x}}_{\bm{n}}\right)\right]}_{+}+\mathit{\lambda}{\left|\left|\bm{w}\right|\right|}^{2},\mathit{\lambda}=\frac{1}{2C}\ \ \ a\ hinge\ loss\ \left(monotonically\right)
$$

*can be optimized by gradient descent*
*logistic regression's loss function*

$$
-{\sum}_{n=1}^{N}\mathrm{p}\left({\mathrm{y}}_{n}|{\bm{x}}_{n}\right)+\mathit{\lambda}{\left|\left|\bm{w}\right|\right|}^{2}
$$

$$
\mathrm{p}\left({\mathrm{y}}_{n}|{\bm{x}}_{n}\right)=\mathit{\sigma}\left(f\left({\bm{x}}_{\bm{n}}\right)\right)=\left\{\begin{array}{c}\mathrm{p}\left({\mathrm{y}}_{n}=1|{\bm{x}}_{n}\right)=\mathit{\sigma}\left(f\left({\bm{x}}_{n}\right)\right)\\ \mathrm{p}\left({\mathrm{y}}_{n}=-1|{\bm{x}}_{n}\right)=1-\mathit{\sigma}\left(f\left({\bm{x}}_{\bm{n}}\right)\right)=\mathit{\sigma}\left(-f\left({\bm{x}}_{\bm{n}}\right)\right)\end{array}\right.
$$

$$
\Rightarrow \mathrm{p}\left({\mathrm{y}}_{n}|{\bm{x}}_{n}\right)=\mathit{\sigma}\left({y}_{n}f\left({\bm{x}}_{\bm{n}}\right)\right)
$$

$$
\Rightarrow -{\sum}_{n=1}^{N}\mathrm{ln}\left(\mathit{\sigma}\left({y}_{n}{\bm{x}}_{n}\right)\right)+\mathit{\lambda}{\left|\left|\bm{w}\right|\right|}^{2}\ \ \ \ \ \ \ \ \ \ a\ maxlikelihood\ loss\ \left(monotonically\right)
$$

$$
{\left[1-{y}_{n}f\left({\bm{x}}_{n}\right)\right]}_{+}\ \ vs\ \ -\frac{1}{\mathrm{ln}2}\mathrm{ln}\left(\mathit{\sigma}\left({y}_{n}{\bm{x}}_{n}\right)\right)
$$

*Both can be viewed as continuous approximations to the misclassification error.*
*And strongly weighted at points of misclassification, weighted less on points far*
*away from hyperplane.*
*Both has a similar form in draw line, but the former tends to give less loss when*
*correctly classified, and distribute 0 loss over margin bound, that's why it leads to*
*sparse solutions.*  
**SVM for Regression**  
***Find Support Vectors : form a sparse solution***  
  *Same as before, only a pile of data points on the margin (tube wrapping the predicted curve) will be at work when predicting new inputs*
  *That means, when predicted curve *$f\left(\bm{x}\right)$* fixed, points almost in predicted curve*
  *contribute nothing, only those points on the boundary of predicted curve's tube contribute to its adjustment (also, prediction for new inputs)*
  By introducing slack variables, support vectors will be formed by data points on the boundary of tube or outside the tube  
an $\mathit{\epsilon}$*\-insensitive error function*

$$
{E}_{\mathit{\epsilon}}\left(f\left(\bm{x}\right)-y\right)=\left\{\begin{array}{c}0,\ \left|f\left(\bm{x}\right)-y\right|<\mathit{\epsilon}\\ \left|f\left(\bm{x}\right)-y\right|-\mathit{\epsilon},\ otherwise\end{array}\right.
$$

$$
C{\sum}_{n=1}^{N}{E}_{\mathit{\epsilon}}\left(f\left({\bm{x}}_{\bm{n}}\right)-{y}_{n}\right)+\frac{1}{2}{\left|\left|\bm{w}\right|\right|}^{2},\ subject\ to\ \left|f\left(\bm{x}\right)-y\right|-\mathit{\epsilon}\ge 0
$$

add slack-variables for each data point
${\mathit{\xi}}_{n}>0$ for upper region outside tube

$$
\ \ \ \ \ \ \ \ \ \ \ f\left({\bm{x}}_{\bm{n}}\right)+\mathit{\epsilon}<{y}_{n}\le f\left({\bm{x}}_{n}\right)+\mathit{\epsilon}+{\mathit{\xi}}_{n}\ and\ {\widehat{\mathit{\xi}}}_{n}=0
$$

${\widehat{\mathit{\xi}}}_{n}>0$ for lower region outside tube

$$
\ \ \ \ \ \ \ \ \ \ \ f\left({\bm{x}}_{\bm{n}}\right)-\mathit{\epsilon}-\ {\widehat{\mathit{\xi}}}_{n}\le {y}_{n}<f\left({\bm{x}}_{\bm{n}}\right)-\mathit{\epsilon}\ and\ {\mathit{\xi}}_{n}=0
$$

${\mathit{\xi}}_{n}=0,\ {\widehat{\mathit{\xi}}}_{n}=0\ $ when inside tube or on the edge of tube

$$
\ \ \ \ \ \ \ \ \ \ \ \ \ f\left({\bm{x}}_{\bm{n}}\right)-\mathit{\epsilon}\le {y}_{n}\le f\left({\bm{x}}_{\bm{n}}\right)+\mathit{\epsilon}
$$

*re-express error function*

$$
C{\sum}_{n=1}^{N}\left({\mathit{\xi}}_{n}+{\widehat{\mathit{\xi}}}_{n}\right)+\frac{1}{2}{\left|\left|\bm{w}\right|\right|}^{2},\ subject\ to\ \left\{\begin{array}{c}f\left({\bm{x}}_{\bm{n}}\right)+\mathit{\epsilon}+{\mathit{\xi}}_{n}-{y}_{n}\ge 0\\ -f\left({\bm{x}}_{\bm{n}}\right)+\mathit{\epsilon}+{\widehat{\mathit{\xi}}}_{n}+{y}_{n}\ge 0\\ {\mathit{\xi}}_{n}\ge 0\\ {\widehat{\mathit{\xi}}}_{n}\ge 0\end{array}\right.
$$

*by Lagrange multiplier*

$$
L=C{\sum}_{n=1}^{N}\left({\mathit{\xi}}_{n}+{\widehat{\mathit{\xi}}}_{n}\right)+\frac{1}{2}{\left|\left|\bm{w}\right|\right|}^{2}-{\sum}_{n=1}^{N}\left({\mathit{\mu}}_{n}{\mathit{\xi}}_{n}+{\widehat{\mathit{\mu}}}_{n}{\widehat{\mathit{\xi}}}_{n}\right)
$$

$$
\ \ \ \ \ \ \ \ -{\sum}_{n=1}^{N}{a}_{n}\left(f\left({\bm{x}}_{\bm{n}}\right)+\mathit{\epsilon}+{\mathit{\xi}}_{n}-{y}_{n}\right)-{\sum}_{n=1}^{N}{\widehat{a}}_{n}\left(-f\left({\bm{x}}_{\bm{n}}\right)+\mathit{\epsilon}+{\widehat{\mathit{\xi}}}_{n}+{y}_{n}\right)
$$

*after derivating*

$$
L\left(\bm{a},\widehat{\bm{a}}\right)={\sum}_{n=1}^{N}\left({a}_{n}-{\widehat{a}}_{n}\right){y}_{n}-\mathit{\epsilon}{\sum}_{n=1}^{N}\left({a}_{n}+{\widehat{a}}_{n}\right)
$$

$$
\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ -\frac{1}{2}{\sum}_{n=1}^{N}{\sum}_{m=1}^{N}\left({a}_{n}-{\widehat{a}}_{n}\right)\left({a}_{m}-{\widehat{a}}_{m}\right)k\left({\bm{x}}_{\bm{n}},{\bm{x}}_{\bm{m}}\right)\ subject\ to\ \left\{\begin{array}{c}0\le {a}_{n}\le C\\ 0\le {\widehat{a}}_{n}\le C\\ {\sum}_{n=1}^{N}\left({a}_{n}-{\widehat{a}}_{n}\right)=0\end{array}\right.
$$

$$
f\left(\bm{x}\right)={\sum}_{n=1}^{N}\left({a}_{n}-{\widehat{a}}_{n}\right)k\left(\bm{x},{\bm{x}}_{n}\right)+b
$$

With KKT conditions $\ \ \left\{\begin{array}{c}{a}_{n}\left(f\left({\bm{x}}_{\bm{n}}\right)+\mathit{\epsilon}+{\mathit{\xi}}_{n}-{y}_{n}\right)=0\\ {a}_{n}\left(-f\left({\bm{x}}_{\bm{n}}\right)+\mathit{\epsilon}+{\widehat{\mathit{\xi}}}_{n}+{y}_{n}\right)=0\\ \left(C-{a}_{n}\right){\mathit{\xi}}_{n}=0\\ \left(C-{a}_{n}\right){\widehat{\mathit{\xi}}}_{n}=0\end{array}\right.$

$$
\left(C-{a}_{n}\right){\mathit{\xi}}_{n}=0\ \ from\ {a}_{n}+{\mathit{\mu}}_{n}=C\ and\ {\mathit{\mu}}_{n}{\mathit{\xi}}_{n}=0
$$

if ${a}_{n}={\widehat{a}}_{n}=0$
  *contribute nothing to prediction*
if ${a}_{n}\ne 0,{\widehat{a}}_{n}=0$

$$
\Rightarrow f\left({\bm{x}}_{\bm{n}}\right)+\mathit{\epsilon}+{\mathit{\xi}}_{n}-{y}_{n}=0\ \left({\mathit{\xi}}_{n}\ge 0\right)
$$

  data points lies above the upper boundary or lies in the upper
  boundary contribute to prediction
if ${a}_{n}=0,{\widehat{a}}_{n}\ne 0$

$$
\Rightarrow -f\left({\bm{x}}_{\bm{n}}\right)+\mathit{\epsilon}+{\widehat{\mathit{\xi}}}_{n}+{y}_{n}=0\ \left({\widehat{\mathit{\xi}}}_{n}\ge 0\right)
$$

  data points lies above the lower boundary or lies in the lower
  boundary contribute to prediction
if ${a}_{n}\ne 0,{\widehat{a}}_{n}\ne 0$

$$
\Rightarrow \left\{\begin{array}{c}f\left({\bm{x}}_{\bm{n}}\right)+\mathit{\epsilon}+{\mathit{\xi}}_{n}-{y}_{n}=0\ \left({\mathit{\xi}}_{n}\ge 0\right)\\ -f\left({\bm{x}}_{\bm{n}}\right)+\mathit{\epsilon}+{\widehat{\mathit{\xi}}}_{n}+{y}_{n}=0\ \left({\widehat{\mathit{\xi}}}_{n}\ge 0\right)\end{array}\right.\ \ are\ incompatible
$$

$$
S=\left\{\left({x}_{n},{y}_{n}\right)|{a}_{n}\ne 0\ or\ {\widehat{a}}_{n}\ne 0\right\}
$$

update b by data point on the boundary of tube.
i.e. $0<{a}_{n}<C\Rightarrow f\left({\bm{x}}_{n}\right)+\mathit{\epsilon}-{y}_{n}=0\ and\ 0<{\widehat{a}}_{n}<C\Rightarrow -f\left({\bm{x}}_{n}\right)+\mathit{\epsilon}+{y}_{n}=0\ $

$$
\mathrm{M} = |S_{a \in (0, C)}| + |S_{\widehat{a} \in (0, C)}|
$$

$$
b=\frac{1}{\mathrm{M}}{\sum}_{n=1}^{\mathrm{M}}\left({y}_{n}-\mathit{\epsilon}-{\sum}_{m=1}^{\mathrm{M}}\left({a}_{m}-{\widehat{a}}_{m}\right)k\left({\bm{x}}_{n},{\bm{x}}_{m}\right)\right)
$$

-----
**SMO(Sequential Minimal Optimization) algorithm** :
Solving $L\left(\bm{a}\right)$  
The secret lies in ${\sum}_{n=1}^{N}{a}_{n}{y}_{n}=0\ $  
That ${a}_{n}$ must obey a linear equality constraint, a diagonal line *and a*n* ineqiality constraint *$0<{a}_{n}<C\Rightarrow $ box constraint  
So at every step, SMO choose two Lagrange multipliers to jointly optimize. After few rounds scan on data, all multipliers converge.  
Note that two is the minimum number that fulfill the linear euality constraint.
3 components of SMO
1. an analytic method to solve for two Lagrange multipliers
• equality constraint in two multipliers

$$
{a}_{1}{y}_{1}+{a}_{2}{y}_{2}=\left\{\begin{array}{c}{a}_{1}+{a}_{2}=\mathit{\gamma},\ {y}_{1}={y}_{2}\\ {a}_{1}-{a}_{2}=\mathit{\gamma},\ {y}_{1}\ne {y}_{2}\end{array}\right.
$$

⇒

$$
\mathit{\gamma}={a}_{1}+s{a}_{2},\ \ s={y}_{1}{y}_{2}
$$

$$
\ \ \ \ \ \mathit{\gamma}={a}_{1}^{old}+s{a}_{2}^{old}
$$

*so one increase, the other one decrease*
*• objective function for two multipliers*

$$
L\left({a}_{1},{a}_{2}\right)={a}_{1}+{a}_{2}-\frac{1}{2}{K}_{11}{a}_{1}^{2}-\frac{1}{2}{K}_{22}{a}_{2}^{2}-s{K}_{12}{a}_{1}{a}_{2}-{y}_{1}{a}_{1}{v}_{1}-{y}_{2}{a}_{2}{v}_{2}+C
$$

$$
{v}_{i}={\sum}_{j=3}^{N}{y}_{j}{a}_{j}^{old}{K}_{ij}={f}^{old}\left({\bm{x}}_{\bm{i}}\right)+{b}^{old}-{y}_{1}{a}_{1}^{old}{K}_{1i}-{y}_{2}{a}_{2}^{old}{K}_{2i},\ {K}_{ij}=k\left({\bm{x}}_{\bm{i}},{\bm{x}}_{\bm{j}}\right)
$$

$$
subject\ to\ \left\{\begin{array}{c}\mathit{\gamma}={a}_{1}+s{a}_{2}\\ \mathit{\gamma}={a}_{1}^{old}+s{a}_{2}^{old}\end{array}\right.\Rightarrow {a}_{1}=\mathit{\gamma}-s{a}_{2}
$$

subsitute ${a}_{1}\ with\ {a}_{2}$

$$
\Rightarrow L\left({a}_{2}\right)=\mathit{\gamma}+\left(1-s\right){a}_{2}-\frac{1}{2}{K}_{11}{\left(\mathit{\gamma}-s{a}_{2}\right)}^{2}-\frac{1}{2}{K}_{22}{a}_{2}^{2}-s{K}_{12}\left(\mathit{\gamma}{a}_{2}-s{a}_{2}^{2}\right)
$$

$$
\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ -{y}_{1}\left(\mathit{\gamma}-s{a}_{2}\right){v}_{1}-{y}_{2}{a}_{2}{v}_{2}+C
$$

$$
\frac{dL\left({a}_{2}\right)}{d{a}_{2}}=s\mathit{\gamma}\left({K}_{11}-{K}_{12}\right)+{y}_{2}\left({v}_{1}-{v}_{2}\right)+\left(1-s\right)-\left({K}_{11}+{K}_{22}-2{K}_{12}\right){a}_{2}
$$

$$
if\ \frac{{d}^{2}L\left({a}_{2}\right)}{d{a}_{2}^{2}}<0\Rightarrow \left({K}_{11}+{K}_{22}-2{K}_{12}\right)>0
$$

$$
\Rightarrow L\left({a}_{2}\right)\ can\ get\ maximum\ by\ solving\ \frac{dL\left({a}_{2}\right)}{d{a}_{2}}=0
$$

$$
\Rightarrow \left({K}_{11}+{K}_{22}-2{K}_{12}\right){a}_{2}=s\mathit{\gamma}\left({K}_{11}-{K}_{12}\right)+{y}_{2}\left({v}_{1}-{v}_{2}\right)+\left(1-s\right)
$$

$$
subject\ to\left\{\begin{array}{c}{v}_{i}=f\left({\bm{x}}_{\bm{i}}\right)+{b}^{old}-{y}_{1}{a}_{1}^{old}{K}_{1i}-{y}_{2}{a}_{2}^{old}{K}_{2i}\\ \mathit{\gamma}={a}_{1}^{old}+s{a}_{2}^{old}\end{array}\right.
$$

$$
\Rightarrow \left({K}_{11}+{K}_{22}-2{K}_{12}\right){a}_{2}^{new}=\left({K}_{11}+{K}_{22}-2{K}_{12}\right){a}_{2}^{old}
$$

$$
+{y}_{2}\left[{f}^{old}\left({\bm{x}}_{1}\right)-{y}_{1}-\left({f}^{old}\left({\bm{x}}_{2}\right)-{y}_{2}\right)\right]
$$

$$
\Rightarrow {a}_{2}^{new}={a}_{2}^{old}+\frac{{y}_{2}\left[{f}^{old}\left({\bm{x}}_{1}\right)-{y}_{1}-\left({f}^{old}\left({\bm{x}}_{2}\right)-{y}_{2}\right)\right]}{{K}_{11}+{K}_{22}-2{K}_{12}}
$$

$$
\Rightarrow {a}_{2}^{new}={a}_{2}^{old}+\frac{{y}_{2}\left[{E}_{1}-{E}_{2}\right]}{\mathit{\eta}}
$$

if $\ \frac{{d}^{2}L\left({a}_{2}\right)}{d{a}_{2}^{2}}=0\Rightarrow {\bm{x}}_{1}={\bm{x}}_{2}$ jump to next pair  

• inequality constraint in two multipliers  
after updating, multipler need do clip to fulfill inequality constraint

$$
{a}_{2}^{new,clipped}=\mathrm{max}\left(\mathrm{min}\left(H,{a}_{2}^{new}\right),L\right)
$$

$$
\left\{\begin{array}{c}L=\mathrm{max}\left(0,\ {a}_{2}^{old}-{a}_{1}^{old}\right),\ H=\mathrm{min}\left(C,\ C+{a}_{2}^{old}-{a}_{1}^{old}\right),\ {y}_{1}\ne {y}_{2}\\ L=\mathrm{max}\left(0,\ {a}_{2}^{old}+{a}_{1}^{old}-C\right),\ H=\mathrm{min}\left(C,\ {a}_{2}^{old}+{a}_{1}^{old}\right),\ {y}_{1}={y}_{2}\end{array}\right.
$$

$$
{a}_{1}^{new}={a}_{1}^{old}+s\left({a}_{2}^{old}-{a}_{2}^{new,clipped}\right)
$$

proof:  when ${y}_{1}={y}_{2}\Rightarrow l:{a}_{1}+{a}_{2}=\mathit{\gamma},\ for\ a\ state\ P({a}_{1}^{old},{a}_{2}^{old})$
*when l on the left bottom of *${a}_{1}+{a}_{2}=C$*,*
  *l forms an isosceles triangle with digtal axis, according to triangel's similarity therom, *${a}_{2}^{new}\le {a}_{1}^{old}+{a}_{2}^{old}=H$
*when l on the right upon *${a}_{1}+{a}_{2}=C$*,*
  *l forms an isosceles triangle with *${a}_{1}=C\ and\ {a}_{2}=C$*, according to triangel's similarity therom, *${a}_{2}^{new}\ge {a}_{1}^{old}+{a}_{2}^{old}-C=L$
*similar proof can be done for *${y}_{1}\ne {y}_{2}$
2. a heuristic for choosing which multipliers to optimize

$$
\left\{\begin{array}{c}{a}_{n}=0\Rightarrow {\mathit{\xi}}_{n}=0\Rightarrow {y}_{n}f\left({x}_{n}\right)\ge 1\\ 0<{a}_{n}<C\Rightarrow {\mathit{\xi}}_{n}=0\Rightarrow {y}_{n}f\left({x}_{n}\right)=1\\ {a}_{n}=C\Rightarrow {\mathit{\xi}}_{n}\ge 0\Rightarrow {y}_{n}f\left({x}_{n}\right)\le 1\end{array}\right.
$$

Iterate until all examples satisfy the condition within $\mathit{\epsilon}$  
• first Lagrange multiplier  
Data violates KKT condition prior to others for the first round
And iterate over ${a}_{n}\in \left(0-\mathit{\epsilon},C+\mathit{\epsilon}\right)$ for KKT violator since then, if no qualification, restart iteration on entire data  
• second Lagrange multiplier  
cache ${E}_{i}$ for ${a}_{n}\in \left(0-\mathit{\epsilon},C+\mathit{\epsilon}\right)$, since calculating kernel function is
time consuming
 ${E}_{1}={f}^{old}\left({\bm{x}}_{1}\right)-{y}_{1}$ for first Lagrange multiplier
 $If\ {E}_{1}>0\Rightarrow \underset{x}{\mathrm{min}}{E}_{2}$ for second multiplier
 $If\ {E}_{1}<0\Rightarrow \underset{x}{\mathrm{max}}{E}_{2}$ for second multiplier
Hierarchical strategy for picking second multiplier when both multipliers share same input vector  
3. a method for computing b  
select b such that the KKT conditions are satisfied for first and second examples

$$
\left\{\begin{array}{c}{a}_{n}=0\Rightarrow {\mathit{\xi}}_{n}=0\Rightarrow {y}_{n}f\left({x}_{n}\right)\ge 1\\ 0<{a}_{n}<C\Rightarrow {\mathit{\xi}}_{n}=0\Rightarrow {y}_{n}f\left({x}_{n}\right)=1\\ {a}_{n}=C\Rightarrow {\mathit{\xi}}_{n}\ge 0\Rightarrow {y}_{n}f\left({x}_{n}\right)\le 1\end{array}\right.
$$

under optimal value of two multipliers
i.e. using $0 < a_n < C \quad \text{and} \quad y_n f(x_n) = 1$ update b  
If $0<{a}_{1}^{\ast}<C,\ let\ {b}_{1}\ satisfy\ {y}_{1}f\left({x}_{1}\right)=1$

$$
b_1^* = y_1 - \sum_{m \in S_{0<a<C}} a_m y_m k(\bm{x}_1, \bm{x}_m)
$$

If $0<{a}_{2}^{\ast}<C,\ let\ {b}_{2}\ satisfy\ {y}_{2}f\left({x}_{2}\right)=1$

$$
b_2^* = y_2 - \sum_{m \in S_{0<a<C}} a_m y_m k(\bm{x}_2, \bm{x}_m)
$$

but now, we only have updated multipliers, not yet optimal, but we can have update share on b

$$
\Delta{b}_{1}={y}_{1}\left({a}_{1}^{new}-{a}_{1}^{old}\right)k\left({\bm{x}}_{1},{\bm{x}}_{1}\right)-{y}_{2}\left({a}_{2}^{new,clipped}-{a}_{2}^{old}\right)k\left({\bm{x}}_{1},{\bm{x}}_{2}\right)
$$

$$
\Delta{b}_{2}={y}_{1}\left({a}_{1}^{new}-{a}_{1}^{old}\right)k\left({\bm{x}}_{1},{\bm{x}}_{2}\right)-{y}_{2}\left({a}_{2}^{new,clipped}-{a}_{2}^{old}\right)k\left({\bm{x}}_{2},{\bm{x}}_{2}\right)
$$

$$
{b}_{1}={E}_{1}+\Delta{b}_{1}+{b}^{old}
$$

$$
{b}_{2}={E}_{2}+\Delta{b}_{2}+{b}^{old}
$$

By adding ${E}_{i}\ in\ {b}_{i},\ $ we can force $\ {f}^{old}\left({x}_{i}\right)\ $ output to be $\ {y}_{i}$
also, since ${a}_{i}$* has updated, so *${f}^{old}\left({x}_{i}\right)$* turn into *${f}^{new}\left({x}_{i}\right)$*, we need add its corresponding share on b, which is *$\Delta{b}_{i}$*, so to force *${f}^{new}\left({x}_{i}\right)\ $ output to be $\ {y}_{i}$

$$
{b}^{new}=\left\{\begin{array}{c}{b}_{1},\ \ 0<{a}_{1}<C\\ {b}_{2},\ \ 0<{a}_{2}<C\\ \frac{{b}_{1}+{b}_{2}}{2},\ \ {a}_{i}=0\ or\ {a}_{i}=C\end{array}\right.
$$

$$
when\ {a}_{i}=0\ or\ {a}_{i}=C,\ {b}^{new}=\forall b\in \left({b}_{1},{b}_{2}\right)
$$

