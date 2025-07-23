---
title: Convex Optimization
published: 2023-09-17
description: "Search the optimal solution"
tags: ["Convex", "extented R space"]
category: Optimization
draft: false
---

**The key to understand Convex Optimization**  
There are many definition decorated with obscure and abstract description that is extremely hard to understand. Nor can it be understanded in geometric way, which will rack our brain to imagine the extension cases in high dimension, or pure mathematical symbols, which benefits nothing for the learning purpose.  
1\. Wiring the practical issues  
As the name of it is telling, we should connect the abstract definition with practical optimization problem. All its definitions and methods have its deep root in better optimization. So we can analyze the acts of objects related to optimization, e.g. target functions, gradient, under such definitions or methods  
2\. Extent from real number system  
In fact, lots definitions have its special form in real number system, and for that, they share lots similarity of their counterpart in the real number system.
e.g. matrix can have its analog to real number
Positive matrix similar to positive number  
3\. Catch the property which can be abstracted from geometrical explanation  
Geometric explanation can anchor a graphical understand for these definition, but we need to extract some properties related to optimization and can live independent without these planes or lines. Those properties are intuitive and simple enough in geometrical form and can be extent to more abstract forms  
4\. Motivation behind these definitions  
To describe some rules in language of math, we can just simply create a function that satisfies those axioms of it, but it can be obscure and too abstract, like, we are only define it for the definition itself.
e.g. summation of all elements in a matrix, that won't do much help in practice
So in the perspective of utility, we need to attach the definition with meaningful stuff, like, geometrical meaning or behavior of operator

**Definition of Vector Space**  
Vector space is space made of vectors, which are linear combination of basis
e.g. if basis is real number vector, then the vector space is a subspace of ${\mathrm{R}}^{\mathrm{n}}$ space
If basis is function, then the vector in space represents a function, since it's a combination of basis functions, e.g. polynomial function, triangle function  
**An informal connection between real number space and function space: discrete to continuous**  
We can take real number vector as a discrete function, e.g. for $\mathbf{v}\in {\mathrm{R}}^{3}$
$$\mathbf{v}={\left[{v}_{1},{v}_{2},{v}_{3}\right]}^{T}=\bm{f}\left(i\right),i=1,2,3\left\{\begin{array}{c}f\left(1\right)={v}_{1}\\ f\left(2\right)={v}_{2}\\ f\left(3\right)={v}_{3}\end{array}\right.$$
That brings summation of its inner product
$${\mathbf{v}}^{\mathbf{T}}\mathbf{v}={\sum}_{i=1}^{3}f\left(i\right)\bullet f\left(i\right)$$
So the continuous function is generally what we so called function vector
$$\bm{f}={\left[f\left({x}_{1}\right),f\left({x}_{2}\right),\dots ,f\left({x}_{n}\right)\right]}^{T},\ \ n\to +\infty $$
That brings integration of its inner product
$${\bm{f}}^{\bm{T}}\bm{f}=\int f\left(x\right)\bullet f\left(x\right)dx$$
Note : that does not mean function space is ${\mathrm{R}}^{\infty}$ space, but we can say function space is isomorphic to ${\mathrm{R}}^{\infty}$ space
There are also some properties generalized from ${\mathrm{R}}^{\mathrm{n}}$ vector space to other vector space
The most important one is inner product, it's the building block of metric and orthogonality
In the process of generalization, the consistent rules a property(operation) should follow weight more than the exact form of property(operation)  
**Relationship between inner product and orthogonality**  
Definition of perpendicular:
  [Two vectors are **orthogonal** to each other if their inner product is zero. That means that the projection of one vector onto the other "collapses" to a point.](https://www.math.drexel.edu/~jwd25/LM_SPRING_07/lectures/lecture7.html) So the distances from $\mathbf{u}$ to $\mathbf{v}$ or from $\mathbf{u}$ to $-\mathbf{v}$  should be identical if they are orthogonal (perpendicular) to each other.
$$\mathbf{u}\perp \bm{v}\Rightarrow \left|\left|\bm{u}-\bm{v}\right|\right|=\left|\left|\bm{u}-\left(-\bm{v}\right)\right|\right|\Rightarrow {\bm{u}}^{\bm{T}}\bm{v}=0$$
$$due\ to\ {\Vert u\Vert}^{2}+{\Vert v\Vert}^{2}-2uv={\Vert u\Vert}^{2}+{\Vert v\Vert}^{2}+2uv$$
The second one is orthogonal basis vectors, which is the fundamental bricks building any vector in the vector space. All can be derived from a simple equation
$$\bm{u}={\mathbf{p}\mathbf{r}\mathbf{o}\mathbf{j}}_{\bm{v}}\bm{u}+\left(\bm{u}-{\mathbf{p}\mathbf{r}\mathbf{o}\mathbf{j}}_{\bm{v}}\bm{u}\right),\ {\bm{u}}^{\bm{T}}\left(\bm{u}-{\mathbf{p}\mathbf{r}\mathbf{o}\mathbf{j}}_{\bm{v}}\bm{u}\right)=0,{\mathbf{p}\mathbf{r}\mathbf{o}\mathbf{j}}_{\bm{v}}\bm{u}=a\frac{\bm{v}}{\left|\left|\bm{v}\right|\right|}$$
Cauchy-Schwarz Inequality
$$\left|{\bm{u}}^{\bm{T}}\bm{v}\right|\le {\left|\left|\bm{u}\right|\right|}_{2}{\left|\left|\bm{v}\right|\right|}_{2}$$
$$\mathrm{Proof}:\ \left|\left|\bm{p}\bm{r}\bm{o}{\bm{j}}_{\bm{v}}\bm{u}\right|\right|=\frac{\left|{\bm{u}}^{\bm{T}}\bm{v}\right|}{\left|\left|\bm{v}\right|\right|}\le \left|\left|\bm{u}\right|\right|$$
General form: Holder Inequality (with weighted norm)
$$E\left[\left|\bm{U}\bm{V}\right|\right]\le E{\left[{\left|\bm{U}\right|}^{p}\right]}^{\frac{1}{p}}E{\left[{\left|\bm{V}\right|}^{q}\right]}^{\frac{1}{q}},\ \ \frac{1}{p}+\frac{1}{q}=1$$
*Weighted inner product <= weighted norm \* weighted norm*  
**Definition of Inner Product Space**  
Any vector in a vector space follows the rule of inner product
Inner Product Space = vector space + inner product applied  
**What is Norm**  
A norm is a function of a vector: $f\left(x\right):{R}^{n}\to R$
we can see that definition of norm always involve sup, such a norm defines a constraint on a set
e.g. for a vector, its norm defines its length, we can turn it into a sup-form (rough)
$${\left|\left|x\right|\right|}_{\ast}=\left|\left|x\right|\right|=\underset{x\ne 0}{\mathrm{sup}}\frac{{x}^{T}x}{\left|\left|x\right|\right|}$$
if we treat x as a set of point forming the x line, then the sup achieved exactly at x
from the unit ball case, we can also find that the definition is searching the max ratio number t from origin to C's edge, e.g.
if C is a ellipisoid, then t must define on the longest line from C's edge to origin, then this sup gives a bound for the set
and the following cases with sup definition, all define a constriant or bound for set that all element in the set satisfy, or in a more abstract way, we can say:
norm define a constraint(constantly, <=) on a set so that this set can be a convex set w.r.t the constraint, i.e. all elements in conv(set) are satisfied. and this constraint follows as least three basic properties.  
**Distinguishment between close set and fully bounded set**  
Closed doesn't mean fully bounded, although fully bounded is closed, e.g. a circle with edge, a half space : $\left\{\bm{x}\right|{\bm{a}}^{\bm{T}}\bm{x}\ <=\ b\}$ is also closed, cause it contains all the limit points, these limit points exist at edge, and it contains edge, as for $\bm{x}\to \ inf$, there are no such convergent sequence, so as no limit point, so even half space is not fully bounded, it still a closed set. For further comparsion, half space $\left\{\bm{x}\right|{\bm{a}}^{\bm{T}}\bm{x}\ <\ b\}$ is open, since it doesn't contain limit points at edge

**Equivalence between quadratic norm and weighted inner product**  
 $\bm{P}\in {\bm{S}}_{++}^{\bm{n}},{\left|\left|\bm{x}\right|\right|}_{\bm{P}}={\left({\bm{x}}^{T}\bm{P}\bm{x}\right)}^{\frac{1}{2}}={\left|\left|{\bm{P}}^{\frac{1}{2}}\bm{x}\right|\right|}_{2}$ <equation>
 $\bm{P}=\bm{Q}\mathbf{\Sigma}{\mathbf{Q}}^{\mathrm{T}},\mathbf{Q}$ is unit orthogonal matrix
We can use coordinate system with column vector in $\mathbf{Q}$ as basis to represent $\bm{x}$
$$\bm{x}=\bm{Q}\bm{y}\Rightarrow {\bm{x}}^{T}\bm{P}\bm{x}={\bm{y}}^{T}{\bm{Q}}^{T}\bm{Q}\mathbf{\Sigma}{\mathbf{Q}}^{\mathrm{T}}\mathbf{Q}\mathbf{y}={\mathbf{y}}^{\mathrm{T}}\mathbf{\Sigma}\mathbf{y}$$
This is equivalent to stretch $\mathbf{y}$, which is $\bm{x}$ under Q's coordinate system, by scale of corresponding eigenvalues, then do innerproduct to itself
$$\mathbf{\Sigma}=\mathbf{d}\mathbf{i}\mathbf{a}\mathbf{g}\left(\mathbf{\lambda}\right)\Rightarrow {\bm{x}}^{T}\bm{P}\bm{x}={\sum}_{i=1}^{n}{\mathit{\lambda}}_{i}{y}_{i}^{2}$$
That is exactly the weighted inner product of $\mathbf{y}$**, **or weighted norm of $\mathbf{y}$**,** and the weights come from eignvalue of $\mathbf{P}$  
**Norm of matrix**  
A matrix represents relationship between two vector spaces, or a mapping from one vector space to another, so it would make more sense when defining its norm with objects it is operating on, that's exactly the operator norm where matrix is taken as a operator: operator norm
  $${\Vert X\Vert}_{a,b}=\mathrm{sup}\left\{{\Vert Xu\Vert}_{a}|{\Vert u\Vert}_{b}\le 1\right\},\ \ X\in {R}^{m\times n}$$
It simply tells the maximum transformation that a matrix can apply on the element from b-norm ball. That can attach to the behavior of an operator
There is another norm for matrix called kernel norm which is the summation of all non-zero singular values
  $${\Vert X\Vert}_{\ast}={\sum}_{i=1}^{r}{\mathit{\sigma}}_{i},\ \ r=rank\left(X\right)$$
Such definition strongly tells the sparsity of structure(magnitude and direction of axis) of basis space that forms the matrix  
**Analog from real number to matrix**  
Lots definition of matrix can be seen as an extent version of its counterpart in real number system, e.g.
Positive defined matrix to positive real number(that can also give inspiration for definition of general inequality)
Gradient w.r.t matrix has similar rules as gradient for real variable
Hessian matrix describes similar property for the **curvature** of specific point as second order derivative did, instead the former is in multi-dimension case where the **curvature** extents to a super ball or super ellipse that has its border plane **perpendicular** to gradient.
So a Hessian matrix has its curvature approximates to a ball tells that we can pick any gradient as the optimization direction since they are all good enough, a elliptic case will be a bit of thorny since different gradients are diverse in magnitudes where a good enough gradient can be hard to choose.
Such a property can be defined by** conditional number** of Hessian matrix, which carves the gap between largest singular value and the smallest one. A ball case, obviously, will have same singular value in all direction  
**Equivalence of norms**  
$$x\in X,{\left|\left|x\right|\right|}_{a}~{\left|\left|x\right|\right|}_{b}\iff \mathit{\alpha}{\left|\left|x\right|\right|}_{a}\le {\left|\left|x\right|\right|}_{b}\le \mathit{\beta}{\left|\left|x\right|\right|}_{a},\ \ \mathit{\alpha}>0,\mathit{\beta}>0$$
They define the same set of open sets, i.e. in the form of [metric space](https://byjus.com/maths/metric-spaces/)(set + metric, e.g. norm space)
Open set: $${\mathrm{B}}_{r}^{i}\left(x\right)=\left\{y\in X|{d}_{i}\left(x,y\right)<r\right\}$$
$${d}_{a}\left(x,y\right)\to 0\Rightarrow {d}_{b}\left(x,y\right)\to 0,\ by\ sandwich\ theorem$$
$$\left\{\begin{array}{c}{d}_{a}\left(x,y\right)\le \frac{1}{\mathit{\alpha}}{d}_{b}\left(x,y\right)={c}_{1}{d}_{b}\left(x,y\right)\\ {d}_{b}\left(x,y\right)\le \mathit{\beta}{d}_{b}\left(x,y\right)={c}_{2}{d}_{a}\left(x,y\right)\end{array}\right.\Rightarrow \left\{\begin{array}{c}{B}_{\frac{r}{{c}_{1}}}^{b}\left(x\right)\subseteq {B}_{r}^{a}\left(x\right)\\ {B}_{\frac{r}{{c}_{2}}}^{a}\left(x\right)\subseteq {B}_{r}^{b}\left(x\right)\end{array}\right.$$
e.g. Imagine that we can always find a pair of stretching coefficients for L1 norm to enclose L2 norm, so as L2 norm
Since their open set includes each other, so they define same set of open sets.
Note that different $x$ induce different open sets(subset of $\mathrm{X}$), so we have the following conclusion:
Equivalent norms(metric spaces) induce same topology(set of open sets)
[Topology](https://en.wikipedia.org/wiki/Topology#Concepts) on sets $X$:$\tau =\left\{{X}_{sub}\subseteq X\right\},{X}_{sub}={\mathrm{B}}_{r}^{i}\left(x\right)$
1. $$X\in \mathit{\tau},\varnothing \in \mathit{\tau}$$
2. $$\forall {X}_{1},\dots {X}_{k}\in \mathit{\tau},{\bigcup}_{i=1}^{k}{X}_{i}\in \mathit{\tau}$$
3. $$\forall {X}_{1},\dots {X}_{k}\in \mathit{\tau},{\bigcap}_{i=1}^{k}{X}_{i}\in \mathit{\tau}$$
Topological space $\left(X,\mathit{\tau}\right)$
That is similar to definition of metric space $\left(X,{\left|\left|\bullet \right|\right|}_{p}\right)$  
**Definition of Banach Space**  
Complete norm vector space or complete metric space
$$\left(X,\left|\left|\bullet \right|\right|\right),\ convergent\ cauchy\ sequence\underset{n\to +\infty}{\mathrm{lim}}\left|\left|{x}_{n}-x\right|\right|=0,\ x\in X,{x}_{n}\in X$$
Norm, a function, applied on vector space has its Cauchy sequence limit still in the same space  
[Example of non-complete norm](https://math.stackexchange.com/questions/1948207/example-of-a-non-complete-normed-vector-space)  
The set of continuous function(vector space) on the unit interval $\left[0,\ 1\right]$
$$\left|\left|f\right|\right|={\int}_{0}^{1}\left|f\left(x\right)\right|dx,{f}_{n}=\left\{\begin{array}{c}1,\ \ x\le \frac{1}{2}\\ \frac{1}{2}n+1-nx,\ \ \frac{1}{2}<x\le \frac{1}{2}+\frac{1}{n}\\ 0,\ \ x>\frac{1}{2}+\frac{1}{n}\end{array}\right.$$
$$\underset{n\to +\infty}{\mathrm{lim}}{f}_{n}=\left\{\begin{array}{c}1,x\le \frac{1}{2}\\ 0,x>\frac{1}{2}\end{array}\right.,\ \ which\ is\ not\ continuous\ function$$  
**General Clue**  
**Optimization target: Mathematical optimization problem**  
$$\mathrm{minimize}\ {f}_{0}\left(x\right):X\to Y$$
  $$\mathrm{s}.\mathrm{t}.\ {f}_{i}\left(x\right)\le {b}_{i},\ \ i=1,\dots ,m$$

Constraint on ${f}_{i}\left(x\right),\ \ i=0,1,\dots ,m$
  Linear: ${f}_{i}\left(ax+by\right)=a{f}_{i}\left(x\right)+b{f}_{i}\left(x\right)$
    e.g. least-square: ${f}_{0}\left(x\right)={\left|\left|Ax-b\right|\right|}_{2}^{2}+\mathit{\rho}{\left|\left|x\right|\right|}_{2}^{2},\mathit{\rho}>0$,with regularization
  linear programming: ${f}_{0}\left(x\right)={c}^{T}x,\ \ \mathrm{s}.\mathrm{t}.\ {f}_{i}\left(x\right)={a}_{i}^{T}\le {b}_{i}$
  Convex: ${f}_{i}\left(ax+by\right)\le a{f}_{i}\left(x\right)+b{f}_{i}\left(x\right),\ \ a,b\in \left[0,1\right],a+b=1$
    Almost-strong-convex: $f\left(\mathit{\lambda}x+\left(1-\mathit{\lambda}\right)y\right)<\mathrm{max}\left\{f\left(x\right),f\left(y\right)\right\}$
    Strong convex: $g\left(x\right)=f\left(x\right)-\frac{m}{2}{\Vert x\Vert}^{2}$  
    
Constraint on $\mathrm{X}$ (set), ${x}_{i},{x}_{j}\in X$
  Affine: ${\theta}_{1}{x}_{i}+{\theta}_{2}{x}_{j}\in X=subspace+{x}_{i},\ \ {\theta}_{1}+{\theta}_{2}=1$
    e.g. hyperplane: $\left\{x|{a}^{T}x=0\right\}$
      Application [SVM](onenote:#SVM&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={11A9696D-1BFF-4700-8B1D-CF78A9E2CCFA}&end&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one)
  Convex: ${\theta}_{1}{x}_{i}+{\theta}_{2}{x}_{j}\in X,\ \ {\theta}_{1},{\theta}_{2}\in \left[0,1\right],\ \ {\theta}_{1}+{\theta}_{2}=1$
    e.g. half space: $\left\{x|{a}^{T}x\le 0\right\}$
    Norm ball: $\mathrm{B}\left(x,r\right)=\left\{y\ |\ \left|\left|y-x\right|\right|\le r\right\}$
      Ellipsoid: $\mathit{\epsilon}\left({x}_{c}\right)=\left\{x|{\left(x-{x}_{c}\right)}^{T}{P}^{-1}\left(x-{x}_{c}\right)\le 1\right\},P={P}^{T}>0$
      Euclidean ball: $\mathrm{B}\left({x}_{c},r\right)=\left\{x|{\left|\left|x-{x}_{c}\right|\right|}_{2}\le r\right\},P={r}^{2}I$
  Cone: ${\theta}_{1}{x}_{i}\in X,{\theta}_{1}\ge 0$
    e.g. Convex cone: ${\theta}_{1}{x}_{i}+{\theta}_{2}{x}_{j}\in X,{\theta}_{1}\ge 0,{\theta}_{2}\ge 0$
      Norm cone: $\mathrm{epi}\left|\left|\cdot \right|\right|=\left\{\left(x,t\right)\ |\ \left|\left|x\right|\right|\le t\right\}\subseteq {R}^{n+1}$
      Positive semidefinite cone: ${\mathrm{S}}_{+}^{n}={\bigcap}_{x\ne 0}\left\{M\in {S}^{n}|{x}^{T}Mx\ge 0\right\}$
      Here $\left\{M\in {S}^{n}|{x}^{T}Mx\ge 0\right\}$ defines a half space in ${\mathrm{S}}^{\mathrm{n}}$, since
       ${x}^{T}Mx$ is a linear function of $\mathrm{M}$.
        e.g. $x={\left[a,b\right]}^{T},M=\left[\begin{array}{cc}x& y\\ y& z\end{array}\right],{x}^{T}Mx=\left[{a}^{2},2ab,{b}^{2}\right]\left[\begin{array}{c}x\\ y\\ z\end{array}\right]$

  Polyhedra: $\mathrm{P}=\left\{x|Ax\le b,Cx=d\right\}$
Simplexes: $\{\mathrm{conv}\left\{{x}_{0},\dots ,{x}_{k}\right\}\ \ {x}_{0},\dots ,{x}_{k}\}\ $affine independent
    i.e. $\left\{{x}_{0},\dots ,{x}_{k}\right\}-{x}_{i}$ linear independent, $0\le \mathrm{i}\le \mathrm{k}$

Properties to mark out function's convexity
  As long as convexity exists in any line($\bm{x}+t\bm{v}$), so it is for all dom
    $\forall \bm{x}\in domf,\bm{v}\in {R}^{n},g\left(t\right)=f\left(\bm{x}+t\bm{v}\right)\ $is convex fucntion for $t$
So is $f\left(\bm{x}\right)$ convex function for $\bm{x}$  
      
  Relationship between convex set and function
     $\mathrm{epi}\left(f\right)$ is convex set $\u27fa$ $f\left(x\right)$ is convex function
  Gradient conditions
    $$\forall x,y\ f\left(y\right)\ge f\left(x\right)+\mathit{\nabla}\bm{f}{\left(\bm{x}\right)}^{T}\left(y-x\right)$$
    $${\nabla}^{2}\bm{f}\left(\bm{x}\right)\in {\bm{S}}^{+}$$
    $${\left(\mathit{\nabla}\bm{f}\left(\bm{x}\right)-\mathit{\nabla}\bm{f}\left(\bm{y}\right)\right)}^{T}\left(\bm{y}-\bm{x}\right)\ge 0,\ \forall \bm{x},\bm{y}\in domf$$
      $$\left\{\begin{array}{c}f\left(y\right)\ge f\left(x\right)+\mathit{\nabla}\bm{f}{\left(\bm{x}\right)}^{T}\left(y-x\right)\\ f\left(x\right)\ge f\left(y\right)+\mathit{\nabla}\bm{f}{\left(\bm{y}\right)}^{T}\left(x-y\right)\end{array}\right.$$

Operation that gain convexity
  Hull: expand arbitrary set $\mathrm{C}$ to Affine | Convex | Cone set
    $$\mathrm{aff}\ \mathrm{C}=\left\{{\theta}_{1}{x}_{1}+\dots +{\theta}_{k}{x}_{k}|{x}_{1},\dots ,{x}_{k}\in C,{\theta}_{1}+\dots +{\theta}_{k}=1\right\}$$
    $$\mathrm{conv}\ \mathrm{C}=\left\{{\theta}_{1}{x}_{1}+\dots +{\theta}_{k}{x}_{k}|{x}_{i}\in C,{\theta}_{i}\in \left[0,1\right],i=1,\dots ,k,\ {\theta}_{1}+\dots +{\theta}_{k}=1\right\}$$
    $$\mathrm{conic}\ \mathrm{C}=\left\{{\theta}_{1}{x}_{1}+\dots +{\theta}_{k}{x}_{k}|{x}_{i}\in C,{\theta}_{i}\ge 0,i=1,\dots ,k\right\}$$

Operation that preserve convexity
  Intersection: $\ \mathrm{epi}\ g=\ {\bigcap}_{y\in A}\mathrm{epi}\ f\left(\bullet ,y\right),g\left(x\right)=\underset{y\in A}{\mathrm{sup}}f\left(x,y\right)=\mathrm{max}\left\{{f}_{y}\left(x\right)|y\in A\right\}$
  Affine function;
  Perspective Function: ${\mathrm{R}}^{\mathrm{n}+1}\to {\mathrm{R}}^{\mathrm{n}}\u2254\ \mathrm{P}\left(z,t\right)=\frac{z}{t},t>0$
  Linear-fractional function : ${\mathrm{R}}^{\mathrm{n}}\to {\mathrm{R}}^{\mathrm{m}+1}\to {\mathrm{R}}^{\mathrm{m}}\u2254$Perspective function $\circ $ Affine function
  [Conjugate](https://math.stackexchange.com/questions/2700835/understanding-the-conjugate-of-a-function)
    ${f}^{\ast}\left(y\right)=\underset{x\in domf}{\mathrm{sup}}\left({y}^{T}x-f\left(x\right)\right)\ $is convex function
  Note: Using these ops as unit to construct powerful function that can approximate lots intractable functions, e.g. neural network is the repetition of Affine function +nonlinear activation  
    
Brick to build optimization target
  Norm is a generalization of physical length, it's a function that
  $$f\left(x\right):V\to R,V\subset {\mathrm{R}}^{\mathrm{n}}\ \mathrm{with}\ \mathrm{properties}\left\{\begin{array}{c}f\left(x\right)\ge 0\\ f\left(x\right)=0\iff \mathrm{x}=0\\ f\left(cx\right)=\left|c\right|f\left(x\right)\\ f\left(x+y\right)\le f\left(x\right)+f\left(y\right)\end{array}\right.$$
  Lots definition involving norm contains "**sup**", so it can be informally treated as a bound that an operation can obtain, in other words, all consequence of the operation are bounded inside this norm.

Generalized inequalities
Think in a programming way that comparison between instance of custom class requires partial order definition, so we can compare them as we did with real numbers. Generalized inequality is a bit taste of it.
$$x,y\in R\Rightarrow \left\{\begin{array}{c}x>y,x-y>0\\ x<y,x-y<0\end{array}\right.\Rightarrow x,y\in {R}^{n}\ \Rightarrow \left\{\begin{array}{c}x>y,?\\ x<y,?\end{array}\right.$$
By introducing generalized inequality, we define the behavior of optimization, since optimization problem is equivalent to finding a partial ordering sequence base on specific rule of inequality.
Proper cone: $\mathrm{K}\subseteq {R}^{n}\left\{\begin{array}{c}convex\\ closed:\underset{n\to +\infty}{\mathrm{lim}}{x}_{n}\in K,{x}_{n}\in K\\ solid:intK\ne \varnothing \\ pointed:x\in K,-x\in K,x=0\end{array}\right.$
  $$x{\le}_{K}y\u27fay-x\in K$$
  $$x{<}_{\mathrm{K}}y\u27fay-x\in intK$$
  e.g. component-wise inequality $\mathrm{K}\subseteq {R}_{+}^{2}:y{\ge}_{K}x\ \u27fa\ y-x\in {K}_{+}^{2}$
  Same as we find min/max element of a set $\mathrm{S}$ when coding, a comparable function passed as an argument, here ${\le}_{K}$ plays the same role
  ![](image_1.74fe7891.png)
   $\left\{x\right\}=minimum\left(S\right):S\subseteq \left\{x\right\}+K,\ \ \forall y\in S,y{\ge}_{K}x,$ full comparable
  ![](image_2.20c961bd.png)
  $$\left\{x\right\}=minimal\left(S\right):S\cap \left(\left\{x\right\}-K\right)=\left\{x\right\},\ \ \exists y\in S,y\ is\ not\ comparable\ to\ x$$
Dual cone: ${\mathrm{K}}^{\ast}=\left\{y|{y}^{T}x\ge 0,\forall x\in K\right\}\left\{\begin{array}{c}convex\\ closed:\underset{n\to +\infty}{\mathrm{lim}}{x}_{n}\in {K}^{\ast},{x}_{n}\in {K}^{\ast}\\ {K}_{1}\subseteq {K}_{2}\Rightarrow {K}_{2}^{\ast}\subseteq {K}_{1}^{\ast},\left[1\right]\\ int{K}^{\ast}\ne \varnothing \Rightarrow {K}^{\ast}\ is\ pointed,\left[2\right]\\ cl\left(K\right)\ is\ pointed\Rightarrow int{K}^{\ast}\ne \varnothing ,\left[3\right]\\ {\left({K}^{\ast}\right)}^{\ast}=cl\left(conv\left(K\right)\right),\left[4\right]\\ \dots \end{array}\right.$
  A set of hyperplanes that can enclose $\mathrm{K}$, $\mathrm{y}$ is the normal of the hyperplane
  \[1\]: with smaller cone, the more hyperplane can enclose this cone
  \[2\]: if K has empty interior
    e.g. $x=\left(0,\ \ast ,\ \ast \right)$ then $\mathrm{y}=\left(a,0,0\right),-y=\left(-a,0,0\right)\Rightarrow {y}^{T}x=-{y}^{T}x$
But $\mathrm{y}\ne 0$, which means K\* is not pointed
  \[3\]: since ${\left({K}^{\ast}\right)}^{\ast}=cl\left(conv\left(K\right)\right)$, and $K*$ has nonempty interior,
    so $conv\left(K\right)$ is pointed,and, $cl\left(K\right)\ \subseteq \ cl\left(conv\right(K\left)\right)$, so $cl\left(K\right)$ is pointed
  \[4\]: assume $\exists y\ \in {\left({K}^{\ast}\right)}^{\ast}\ |\ y\ \notin \ cl(convK)$, according to strick hyperplane therom
    $$\exists \ a,\ b\ =>\ ay\ >\ b,\ \ ax\ <\ b,\ \forall x\in \ cl\left(convK\right)$$
    since $0\ \in \ K\ =>\ 0\ \in \ cl\left(convK\right)\ =>\ b\ >\ 0$
    $$\exists \ t\ >\ 0,\ ty\ \in \ {\left({K}^{\ast}\right)}^{\ast},\ and\ \ ty\ \notin \ cl\left(convK\right)$$
    since $a\ \ast \ t\ \ast \ y\ >\ tb\ <\ b\ when\ t\ <\ 1$, which is a contradiction
  Note :if K is closed convex(proper cone), then dual cone on dual cone return to original cone  
    

  $$x{\le}_{K}y\u27fa{\mathit{\lambda}}^{T}\left(y-x\right)\ge 0,\ \ \mathit{\lambda}\in {K}^{\ast}\u27fa\mathit{\lambda}{\ge}_{{K}^{\ast}}0$$
  $$x{<}_{K}y\u27fa{\mathit{\lambda}}^{T}\left(y-x\right)>0,\ \ \mathit{\lambda}\in {K}^{\ast}\u27fa\mathit{\lambda}{\ge}_{{K}^{\ast}}0,\mathit{\lambda}\ne 0$$  
    
  ![](image_3.79c7279f.png)
  Minimum $\u27fa$ has all **strict** supporting hyperplanes at $x$
  $$x\ =\ minimum\left(S\right)\Rightarrow \ S\ \subseteq \ \left\{x\right\}+\ K,\ \forall z\ \in \ S,\ z\ -\ x\ \in K$$
  $$\forall \mathit{\lambda}{>}_{{K}^{\ast}}0,\ \forall \ z\ \in \ S,{\mathit{\lambda}}^{T}\left(z\ -\ x\right)\ge \ 0$$
  since ${K}^{\ast}$ contains all normal that its hyperplane support K at $x$, $x$ become supporting point both of K and S, and the supporting hyperplane is $\left\{z\ \right|{\mathit{\lambda}}^{T}\left(\ z\ -\ x\right)=\ 0,\mathit{\lambda}\ne 0\}$  
    
  ![](image_4.3c93408c.png)
  Minimal$\u27fa$ has only one **strict** supporting hyperplanes at $x$
  $$\exists \mathit{\lambda}{>}_{{K}^{\ast}}0,\forall z\ \in \ S,\ {\mathit{\lambda}}^{T}\left(z-x\right)\ge 0\Rightarrow \left\{x\right\}=minimal\left(S\right),\nRightarrow {S}^{\prime}s\ convexity$$
  $$\left\{x\right\}=minimal\left(S\right)+S\ is\ convex\Rightarrow \exists \mathit{\lambda}{\ge}_{{K}^{\ast}}0,\mathit{\lambda}\ne 0,\forall z\ \in \ S,\ {\mathit{\lambda}}^{T}\left(z-x\right)\ge 0$$
  Proof:
  $$S\cap \left(\left(\left\{x\right\}-K\right)\backslash \left\{x\right\}\right)=\varnothing ,\ S\ is\ convex$$
  Applying the separating hyperplane theorem, $\exists \mathit{\lambda}\ne 0,\mathit{\mu}$
  $$\left\{\begin{array}{c}{\mathit{\lambda}}^{T}z\ge \mathit{\mu},\ \ \forall z\ \in \ S\ \Rightarrow \mathit{\lambda}{\ge}_{{K}^{\ast}},{\mathit{\lambda}}^{T}x\ge \mathit{\mu}\\ {\mathit{\lambda}}^{T}\left(x-y\right)\le \mathit{\mu},\forall y\ \in K\Rightarrow x\in x-K,{\mathit{\lambda}}^{T}x\le \mathit{\mu}\end{array}\right.\Rightarrow {\mathit{\lambda}}^{T}x=\mathit{\mu}\Rightarrow {\mathit{\lambda}}^{T}z\ge {\mathit{\lambda}}^{T}x$$  
    
  ![](image_5.64cff9bc.png)
  $$\left\{x\right\}=minimal\left(S\right)\nRightarrow \exists \mathit{\lambda}{\ge}_{{K}^{\ast}}0,\mathit{\lambda}\ne 0,\forall z\ \in \ S,\ {\mathit{\lambda}}^{T}\left(z-x\right)\ge 0$$  
    
  ![](image_6.f70ee4b5.png)
  $$\left\{x\right\}=minimal\left(S\right),S\ is\ convex\nRightarrow \exists \mathit{\lambda}{>}_{{K}^{\ast}}0,\mathit{\lambda}\ne 0,\forall z\ \in \ S,\ {\mathit{\lambda}}^{T}\left(z-x\right)\ge 0$$
  $$i.e.\ \ \mathit{\lambda}=\left(1,0\right)\in cl\left({K}^{\ast}\right)\notin int{K}^{\ast}$$  
    
  ![](image_7.d02823eb.png)
  $$\left\{x\right\}\ne minimal\left(S\right)\nRightarrow \nexists \mathit{\lambda}{\ge}_{{K}^{\ast}}0,\mathit{\lambda}\ne 0,\forall z\ \in \ S,\ {\mathit{\lambda}}^{T}\left(z-x\right)\ge 0$$
  $$\mathrm{i}.\mathrm{e}.\ {x}_{2}\ is\ not\ minimal,\ but\ \exists \mathit{\lambda}=\left(1,0\right){\ge}_{{K}^{\ast}}0\ supports\ {S}_{2}\ at\ {x}_{2}$$  
    
**The importance of convexity in optimization**  
Convexity means global optimal and convergence to it, since a convex function satisfies
First order conditions: $f\left(y\right)\ge f\left(x\right)+\nabla f{\left(x\right)}^{T}\left(y-x\right),\forall x,y\in domf$
  $$\nabla f\left(x\right)=0\Rightarrow f\left(y\right)\ge f\left(x\right),\forall x,y\in domf$$
Second order conditions: ${\nabla}^{2}f\left(x\right)\ge 0$
The two conditions indicates a global optimal of $f$
The optimization of a target function maybe hard to achieve, e.g. there may lack of analytical solution, like objective in Variational Inference
$$\mathrm{log}p\left(X\right)=\mathrm{log}{\sum}_{z}p\left(X,Z\right)$$
Instead, the optimization can be equivalently be done by a lower bound of the target objective, given they are convex functions.
$$\mathrm{max}\mathrm{log}{\sum}_{z}p\left(X,Z\right)\equiv \mathrm{max}{\sum}_{z}p\left(Z|X\right)\mathrm{log}p\left(X,Z\right)$$
$${\sum}_{z}p\left(Z|X\right)\mathrm{log}p\left(X,Z\right)\le \mathrm{log}p\left(X\right)$$
Why ?
Imagine that in convex case, both lower bound and its supreme are convex, so a point in lower bound has lower value, so is it in supreme.
But in non-convex case, the same point may has higher value in supreme, since supreme is not convex function, so there may be lots peaks in it

**Lagrange Multiplier & KKT: Chapter 5.4**  
$$\underset{\bm{x}\in {\bm{R}}^{\bm{n}}}{\mathrm{min}}f\left(\bm{x}\right)$$
  $$\mathrm{s}.\mathrm{t}.\left\{\begin{array}{c}{c}_{i}\left(\bm{x}\right)=0,i\in \mathcal{E}\\ {c}_{i}\left(\bm{x}\right)\le 0,i\in I\end{array}\right.$$
$$available\ field:\ \mathrm{\Omega}=\left\{x|{c}_{i}\left(\bm{x}\right)=0,i\in \mathcal{E},{c}_{i}\left(\bm{x}\right)\le 0,i\in I\right\}$$
$$\Rightarrow L\left(x,\mathit{\lambda},v\right)=f\left(x\right)+{\sum}_{i\in I}{\mathit{\lambda}}_{i}{c}_{i}\left(x\right)+{\sum}_{i\in \mathcal{E}}{v}_{i}{c}_{i}\left(x\right),f\left(x\right)\ge L\left(x,\mathit{\lambda},v\right)$$
$$\Rightarrow \underset{\bm{x}\in \mathbf{\Omega}}{\mathrm{min}}f\left(\bm{x}\right)=\underset{\mathit{\lambda}\le 0,v}{\mathrm{max}}g\left(\mathit{\lambda},v\right),\ \ g\left(\mathit{\lambda},v\right)=\underset{x\in {R}^{n}}{\mathrm{inf}}L\left(x,\mathit{\lambda},v\right)$$
Which is concave function
We map a minimization problem in original space into its bounded problem, in here bounding it above, in dual space, which is a convex function with respect to original space and can be solved easier if provided with appropriate Lagrange multipliers.
In general
1. Find assistant function that below target function over its domain
2. Maximize assistant function so that it bounds target function tightest by adjusting Lagrange multipliers
 $g\left(\mathit{\lambda},v\right)$ is a concave function with respect to Lagrange multiplier,
  $$\underset{x\in {R}^{n}}{\mathrm{inf}}L\left(x,\mathit{\lambda},v\right)=\underset{\begin{array}{c}\left|\mathrm{\Pi}\right|\to 0\\ n\to \infty \end{array}}{\mathrm{lim}}\mathrm{min}\left\{L\left({x}_{{k}_{1}},\mathit{\lambda},v\right),\dots ,L\left({x}_{{k}_{n}},\mathit{\lambda},v\right)\right\},\mathrm{\Pi}=\underset{i=1,..,n}{\mathrm{max}}\left\{{x}_{{k}_{i+1}}-{x}_{{k}_{i}}\right\}$$
So $g\left(\mathit{\lambda},v\right)$ indicates a infinum w.r.t $x:\ \forall \stackrel{~}{x}\in {R}^{n},g\left(\mathit{\lambda},v\right)\le L\left(\stackrel{~}{x},\mathit{\lambda},v\right)\le f\left(\stackrel{~}{x}\right)$
since we are trying to find its maximum that bounds target function tightest, i.e.
  $$\underset{\mathit{\lambda}\le 0,v}{\mathrm{max}}g\left(\mathit{\lambda},v\right)$$
Informal explanation for the sign of Lagrange multiplier is that for a minimization function, its Lagrange function always bound it above, Lagrange multipliers must be chosen so that:
  $$f\left(x\right)\ge L\left(x,\mathit{\lambda},v\right)$$
Which implies the sign of Lagrange multiplier
  $${c}_{i}\left(x\right)\le 0,i\in I,{\mathit{\lambda}}_{i}\ge 0$$  
    
But a deeper inspection can relate to gradients
The core question is when do we reach optimal ? That is when we cannot find a feasible direction that can reach to smaller or bigger function value.
For constraint-free problem, optimal reaches when gradient is 0.
  $$\nabla f\left(x\right)=0$$
For constraint problem, the allowed gradients can only be in region defined by constraints (available field $\mathrm{\Omega}$), so optimal reaches only when no feasible direction found in available field
![](image_8.3161c824.png)
Let's first define feasible direction(tangent at $x$, updating sequence towards $x$ in available field) and its set--tangent cone
  $$\forall x\in \mathrm{\Omega},\exists {\left\{{z}_{k}\right\}}_{k=1}^{\infty}\subset \mathrm{\Omega},\underset{k\to \infty}{\mathrm{lim}}{z}_{k}=x,\exists {\left\{{t}_{k}\right\}}_{k=1}^{\infty},\underset{k\to \infty}{\mathrm{lim}}{t}_{k}=0$$
  $$\underset{k\to \infty}{\mathrm{lim}}\frac{{z}_{k}-x}{{t}_{k}}=d$$
Tangent cone is assembly of all tangent vectors at $x$
  $${T}_{\mathrm{\Omega}}\left(x\right)=\left\{d\right\}$$
And a feasible direction satisfies(for minimization)
  $${d}^{T}\nabla f\left(x\right)<0$$
So a local minimum at ${x}^{\ast}\in \mathrm{\Omega}$ satisfies, i.e. no feasible direction found in available field
  $$\forall d\in {T}_{\mathrm{\Omega}}\left({x}^{\ast}\right),{d}^{T}\nabla f\left({x}^{\ast}\right)\ge 0$$
  Or equivalently
  $${T}_{\mathrm{\Omega}}\left({x}^{\ast}\right)\cap \left\{d|{d}^{T}\nabla f\left({x}^{\ast}\right)<0\right\}=\varnothing $$
Tangent cone defines on geometric properties, which is unanalytical, we use its linear approximation as replacement
  $${\mathcal{F}}_{\mathrm{\Omega}}\left(x\right)\u2254\left\{\begin{array}{c}{d}^{T}\nabla {c}_{i}\left(x\right)=0,i\in \mathcal{E}\\ {d}^{T}\nabla {c}_{i}\left(x\right)\le 0,i\in \mathcal{A}\left(x\right)\cap I\\ \forall d\in {R}^{n},i\in I\backslash \mathcal{A}\left(x\right)\end{array}\right.,\ \ \mathcal{A}\left(x\right)=\mathcal{E}\cup \left\{i\in I:{c}_{i}\left(x\right)=0\right\}$$
  $${T}_{\mathrm{\Omega}}\left({x}^{\ast}\right)\subseteq {\mathcal{F}}_{\mathrm{\Omega}}\left(x\right)$$
![](image_9.209443b3.png)
To ensure ${T}_{\mathrm{\Omega}}\left({x}^{\ast}\right)={\mathcal{F}}_{\mathrm{\Omega}}\left({x}^{*}\right)$, some **constraint qualities** are required
  LICQ: $if\ \nabla {c}_{i}\left(x\right),\ i\in \mathcal{A}\left(x\right)\ are\ linear\ independent,\ then\ {T}_{\mathrm{\Omega}}\left({x}^{\ast}\right)={\mathcal{F}}_{\mathrm{\Omega}}\left({x}^{*}\right)$

For equalities constraint, available field is made of points satisfy
  $${c}_{i}\left(x\right)=0,i\in \mathcal{E}$$
So tangent cone was confined on infinitesimal plane at $x$, e.g. for 2-d case, tangent cone only contains one tangent vector, and they are perpendicular to constraint surfaces' gradients,
Which means all tangent vectors in tangent cone also perpendicular to gradients
  $${d}^{T}\nabla {c}_{i}\left(x\right)=0,\forall d\in {\mathcal{F}}_{\left\{x|{c}_{i}\left(x\right)\right\}}\left(x\right)$$
And optimization along such direction won't violate the equalities constraint, i.e.
  $$if\ {d}^{T}\nabla f\left(x\right)<0,{x}^{\prime}=x+\mathit{\epsilon}d,then\ {c}_{i}\left({x}^{\prime}\right)=0$$
  Proof:
    $${c}_{i}\left({x}^{\prime}\right)={c}_{i}\left(x\right)+\nabla {c}_{i}{\left(x\right)}^{T}\left(x-{x}^{\prime}\right)$$
$$\ \ \ \ \ \ \ \ \ \ \ \ =\mathit{\epsilon}\nabla {c}_{i}{\left(x\right)}^{T}d=0$$

For inequalities constraint, available field is made of points satisfy
  $${c}_{i}\left(\bm{x}\right)\le 0,i\in I$$
Which is solid region with equalities as edge, so we need to analyze points at border and internal respectively
Tangent cone of points at border were bounded by their tangents along the surface, which is perpendicular to gradients, so angles between any tangent vectors and gradients are greater or equal to 90, since a feasible direction must stay in constraint region.
  $${c}_{i}\left(x\right)=0,i\in I,\forall d\in {\mathcal{F}}_{\left\{x|{c}_{i}\left(x\right)\right\}}\left(x\right),{d}^{T}\nabla {c}_{i}\left(x\right)\le 0$$
And optimization along such direction won't violate the inequalities constraint, i.e.
  $$if\ {d}^{T}\nabla f\left(x\right)<0,{x}^{\prime}=x+\mathit{\epsilon}d,then\ {c}_{i}\left({x}^{\prime}\right)\le 0$$
  Proof:
    $${c}_{i}\left({x}^{\prime}\right)={c}_{i}\left(x\right)+\nabla {c}_{i}{\left(x\right)}^{T}\left({x}^{\prime}-x\right)$$
$$\ \ \ \ \ \ \ \ \ \ \ \ =\mathit{\epsilon}\nabla {c}_{i}{\left(x\right)}^{T}d\le 0,\ \exists \mathit{\epsilon}\ge 0$$
Now we apply the same scheme to internal points
  $${c}_{i}\left(\bm{x}\right)<0,i\in I$$
Actually, such point has its feasible direction any vector in real space, since we are in internal available field, an appropriate movement will still stay in available field. And we can always find a feasible direction that can lead us to better function value.
  $$if\ {\mathcal{F}}_{\left\{x|{c}_{i}\left(x\right)\right\}}\left(x\right)={R}^{n},\exists d\in {\mathcal{F}}_{\left\{x|{c}_{i}\left(x\right)\right\}}\left(x\right),\ {d}^{T}\nabla f\left(x\right)<0$$
  $${x}^{\prime}=x+\mathit{\epsilon}d,then\ {c}_{i}\left({x}^{\prime}\right)\le 0$$
  Proof:
    $${c}_{i}\left({x}^{\prime}\right)={c}_{i}\left(x\right)+\nabla {c}_{i}{\left(x\right)}^{T}\left(x-{x}^{\prime}\right)$$
$$\ \ \ \ \ \ \ \ \ \ \ \ ={c}_{i}\left(x\right)+\mathit{\epsilon}\nabla {c}_{i}{\left(x\right)}^{T}d\le 0,\exists \mathit{\epsilon}$$
We find out that a feasible direction for target function requires
  $${d}^{T}\nabla f\left(x\right)<0$$
And allowed directions provided by available field are
  $${\mathcal{F}}_{\mathrm{\Omega}}\left(x\right)\u2254\left\{\begin{array}{c}{d}^{T}\nabla {c}_{i}\left(x\right)=0,i\in \mathcal{E}\\ {d}^{T}\nabla {c}_{i}\left(x\right)\le 0,i\in \mathcal{A}\left(x\right)\cap I\\ \forall d\in {R}^{n},i\in I\backslash \mathcal{A}\left(x\right)\end{array}\right.$$
So if we cannot find a descent vector $d$ meets both requirements at same time, we arrivate at a local minimum
  $$\left\{d|{d}^{T}\nabla f\left({x}^{\ast}\right)<0\right\}\cap {\mathcal{F}}_{\mathrm{\Omega}}\left({x}^{\ast}\right)=\varnothing $$
The third statement in ${T}_{\mathrm{\Omega}}\left(x\right)$ contributes nothing to the intersection, which means strict inequalities constraints are inactive.
  $$f\left({x}^{\ast}\right)\ is\ local\ optimal\ \Rightarrow \left\{d|\begin{array}{c}{d}^{T}\nabla f\left({x}^{\ast}\right)<0\\ {d}^{T}\nabla {c}_{i}\left({x}^{\ast}\right)=0,i\in \mathcal{E}\\ {d}^{T}\nabla {c}_{i}\left({x}^{\ast}\right)\le 0,i\in \mathcal{A}\left({x}^{\ast}\right)\cap I\end{array}\right\}=\varnothing $$
Equivalently, it can transform to
  $$f\left({x}^{\ast}\right)\ is\ local\ optimal\ \Rightarrow \left\{d|\begin{array}{c}{d}^{T}\left(-\nabla f\left({x}^{\ast}\right)\right)>0\\ {d}^{T}\nabla {c}_{i}\left({x}^{\ast}\right)=0,i\in \mathcal{E}\\ {d}^{T}\nabla {c}_{i}\left({x}^{\ast}\right)\le 0,i\in \mathcal{A}\left({x}^{\ast}\right)\cap I\end{array}\right\}=\varnothing $$
Yielding two infinitesimal half spaces
  $$A:\left\{d|{d}^{T}\left(-\nabla f\left({x}^{\ast}\right)\right)>0\right\},\ norm\ is\ -\nabla f\left({x}^{\ast}\right)$$
  $$B:\left\{d|{d}^{T}\nabla {c}_{i}\left({x}^{\ast}\right)=0,i\in \mathcal{E};{d}^{T}\nabla {c}_{i}\left({x}^{\ast}\right)\le 0,i\in \mathcal{A}\left({x}^{\ast}\right)\cap I\right\},$$
$$\ \ \ \ \ norm\ is\ {\sum}_{i\in \mathcal{A}\left({x}^{\ast}\right)}{\mathit{\lambda}}_{i}\nabla {c}_{i}\left({x}^{\ast}\right)+{\sum}_{i\in I\backslash \mathcal{A}\left({x}^{\ast}\right)}{\mathit{\lambda}}_{i}\nabla {c}_{i}\left({x}^{\ast}\right),\ \ {\mathit{\lambda}}_{i}=0,i\in I\backslash \mathcal{A}\left({x}^{\ast}\right)$$
  $$\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ ={\sum}_{i\in I\cup \u2107}{\mathit{\lambda}}_{i}\mathit{\nabla}{c}_{i}\left({x}^{\ast}\right)$$
According to strict hyperplane separating theorem
  $$A\cap B=\varnothing ,\exists \bm{a}\ne 0,\forall \bm{x}\in A,{\bm{a}}^{\bm{T}}\bm{x}<0;\forall \bm{y}\in B,{\bm{a}}^{\bm{T}}\bm{y}\ge 0$$
So optimal reaches only when the two half spaces share parallel norms
  $$-\nabla f\left({x}^{\ast}\right)={\sum}_{i\in I\cup \u2107}{\mathit{\lambda}}_{i}\nabla {c}_{i}\left({x}^{\ast}\right),\ \ s.t.{\mathit{\lambda}}_{i}{c}_{i}\left({x}^{\ast}\right)=0,i\in I\left\{\begin{array}{c}{\mathit{\lambda}}_{i}=0,{c}_{i}\left({x}^{\ast}\right)<0,i\in I\backslash \mathcal{A}\left(x\right)\\ {\mathit{\lambda}}_{i}\ge 0,{c}_{i}\left({x}^{\ast}\right)=0,i\in \mathcal{A}\left({x}^{\ast}\right)\cap I\end{array}\right.$$
That's exactly the extended form of solving optimal with constraint in 1-d case
Let's dig further to the sign of ${\lambda}_{i}$ by multiplying the equation with $d$ on both sides
  $$-{d}^{T}\nabla f\left({x}^{\ast}\right)={\sum}_{i\in I\cup \u2107}{\mathit{\lambda}}_{i}{d}^{T}\nabla {c}_{i}\left({x}^{\ast}\right),\ \ \ \bm{F}\bm{a}\bm{r}\bm{k}\bm{a}\bm{s}\ \bm{l}\bm{e}\bm{m}\bm{m}\bm{a}$$
  $$\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ ={\sum}_{\mathrm{i}\in \mathcal{E}}{\mathit{\lambda}}_{i}{d}^{T}\mathit{\nabla}{c}_{i}\left({x}^{\ast}\right)+{\sum}_{i\in \mathcal{A}\left({x}^{\ast}\right)\cap I}{\mathit{\lambda}}_{i}{d}^{T}\mathit{\nabla}{c}_{i}\left({x}^{\ast}\right)+{\sum}_{i\in I\backslash \mathcal{A}\left(x\right)}{\mathit{\lambda}}_{i}{d}^{T}\mathit{\nabla}{c}_{i}\left({x}^{\ast}\right)$$
  $$\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ ={\sum}_{i\in \mathcal{A}\left({x}^{\ast}\right)\cap I}{\mathit{\lambda}}_{i}{d}^{T}\mathit{\nabla}{c}_{i}\left({x}^{\ast}\right),\ \ \left\{\begin{array}{c}{d}^{T}\mathit{\nabla}{c}_{i}\left({x}^{\ast}\right)=0,i\in \mathcal{E}\\ {\mathit{\lambda}}_{i}=0,i\in I\backslash \mathcal{A}\left(x\right)\end{array}\right.$$
  $$\Rightarrow -{d}^{T}\nabla f\left({x}^{\ast}\right)={\sum}_{i\in \mathcal{A}\left({x}^{\ast}\right)\cap I}{\mathit{\lambda}}_{i}{d}^{T}\nabla {c}_{i}\left({x}^{\ast}\right),\ \ \left\{\begin{array}{c}{d}^{T}\nabla f\left({x}^{\ast}\right)<0\\ {d}^{T}\nabla {c}_{i}\left({x}^{\ast}\right)\le 0\end{array}\right.$$
As we know from the aforementioned content, optimal reaches only when no existence of such feasible direction, i.e. no solution for the equation, which equivalent to specific sign of ${\lambda}_{i}$
  $${\lambda}_{i}\ge 0\Rightarrow -{d}^{T}\nabla f\left({x}^{\ast}\right)>0\ne {\sum}_{i\in \mathcal{A}\left({x}^{\ast}\right)\cap I}{\mathit{\lambda}}_{i}{d}^{T}\nabla {c}_{i}\left({x}^{\ast}\right)\le 0,\ \ i\in \mathcal{A}\left({x}^{\ast}\right)\cap I$$
So in conclusion, a stationary points reaches when
  $$-\nabla f\left({x}^{\ast}\right)={\sum}_{i\in I\cup \u2107}{\mathit{\lambda}}_{i}\nabla {c}_{i}\left({x}^{\ast}\right),\left\{\begin{array}{c}{\mathit{\lambda}}_{i}=0,{c}_{i}\left({x}^{\ast}\right)<0,i\in I\backslash \mathcal{A}\left(x\right)\\ {\mathit{\lambda}}_{i}\ge 0,{c}_{i}\left({x}^{\ast}\right)=0,i\in \mathcal{A}\left({x}^{\ast}\right)\cap I\\ {\mathit{\lambda}}_{i}\in R,i\in \mathcal{E}\end{array}\right.$$
In its Lagrange form, such Lagrange multipliers ${\bm{\lambda}}^{\ast}$ can be described by KKT conditions
  $$\mathrm{if}\ f\left({x}^{\ast}\right)\ is\ local\ optimal\ and\ {T}_{\mathrm{\Omega}}\left({x}^{\ast}\right)={\mathcal{F}}_{\mathrm{\Omega}}\left({x}^{*}\right)$$
  $$L\left({\bm{x}}^{\ast},{\bm{\lambda}}^{\ast}\right)=f\left({\bm{x}}^{\ast}\right)+{\sum}_{i\in I\cup \u2107}{\mathit{\lambda}}_{i}^{\ast}{c}_{i}\left({x}^{\ast}\right)\ $$
  $${\nabla}_{\bm{x}}L\left({\bm{x}}^{\ast},{\bm{\lambda}}^{\ast}\right)={\nabla}_{\bm{x}}f\left({\bm{x}}^{\ast}\right)+{\sum}_{i\in I\cup \u2107}{\mathit{\lambda}}_{i}^{\ast}{\nabla}_{\bm{x}}{c}_{i}\left({x}^{\ast}\right)=0$$
  $$\mathrm{s}.\mathrm{t}.\ \left\{\begin{array}{c}{c}_{i}\left({x}^{\ast}\right)=0,\forall i\in \mathcal{E}\\ {c}_{i}\left({x}^{\ast}\right)\le 0,\forall i\in I\\ {\mathit{\lambda}}_{i}^{\ast}\ge 0,\forall i\in I\\ {\mathit{\lambda}}_{i}^{\ast}{c}_{i}\left({x}^{\ast}\right)=0,\forall i\in I\end{array}\right.$$
Note that the KKT conditions only states that no existence of descent direction, but not equivalent to solution of local optimal
-----  
**Purpose for defining feasible optimization issues**  
What kind of properties the set of target of interest should have ? This is exactly the constraint applied on the set of target.
All these definition are for compatibility beyond real space, or even, to infinite space
Convexity
The consistency and continuity between any two points ensure the optimization is meaningful.
To illustrate its importance, we can consider a extreme case where one point, which is the optimal point, is missing in the set, so it’s out of the consideration for a feasible optimization problem.
Cone
From perspective of optimization, a cone set stands for sub gradients of non-differentiable point.
And dual cone defines a set of directions have degree less than 90 with these sub gradients, so in a constraint optimization problem, a optimal point reaches when feasible region has no intersection with these directions, otherwise directions in the intersection can slowly lead to sub gradients and then to the optimal.
Support hyperplane
Support hyperplane has simple and straight geometrical explanation but illustrates a extreme useful property of optimization that a support point exclusively tells its update direction which also yield its optimal when has no intersection with region defined by constraint
The word "support" can make an graphical analogy to gravity in physics where any points beside support point in set have force support them up while the opposite case exists points drop downward
Generalized inequalities
Let's first take a look on inequality in real number system
  $$a\ge b\equiv a-b\in {R}^{+}$$
And ${R}^{+}$ is exactly a cone
Now if we extent it to elements of unknown vector space
  $$x\succcurlyeq y\equiv x-y\in K$$
Base on generalized inequalities, we can define partial order relationship, e.g.
How can we compare between matrixes ?
Follow the frame provided from Generalized inequalities, we need to find a cone of matrix to satisfy the inequality
  $$A\succcurlyeq B\equiv A-B\in {S}^{+}$$
 ${S}^{+}$ is positive semidefinite cone
Generalized inequalities is a fundamental and essential definition for defining good optimization problem, since the essence of best solution is that it is bigger or smaller than other solution in some measurable space, which means a partial must exist between these solutions, that in turn depends on the definition of generalized inequalities
Operation that preserve convexity
Max function
  $$g\left(x\right)=\underset{y\in A}{\mathrm{sup}}f\left(x,y\right)=\mathrm{max}\left\{{f}_{y}\left(x\right)|y\in A\right\}$$
  Application for max function can be related to alternating optimization problem, e.g. EM algorithm
  We fix one component of parameters, then optimize the other, and then switch them while doing same process.
Conjugate
  $${f}^{\ast}\left(y\right)=\underset{x\in domf}{\mathrm{sup}}\left({y}^{T}x-f\left(x\right)\right)$$
  It has deep connection to Lagrange Method where Lagrange multiplier was expressed as $\mathrm{y}$ and $f\left(x\right)$ is our target function.
  We map the original space $x\in \mathcal{X}$ into a dual space $\left(x,y\right)\in \mathcal{D}$ where proper $y$ turns $f\left(x\right)$ into convex function $f\left(x;y\right)$
  The most familiar application is regularization for cost function.  
    
**Gradient-descent-based methods**  
$$\underset{\bm{p}\to 0}{\mathrm{lim}}\frac{f\left(\bm{x}+\bm{p}\right)-f\left(\bm{x}\right)-{\bm{g}}^{\bm{T}}\bm{p}}{\left|\left|\bm{p}\right|\right|}=0,\ \bm{g}\ is\ gradient\ at\ \bm{x}$$
Actually, the definition tells that projection of gradient on direction $\bm{p}$ is the direction derivative
$${\bm{x}}^{k+1}={\bm{x}}^{k}+{\mathit{\alpha}}_{k}{\bm{d}}^{k}$$
1. Find descent direction ${\bm{d}}^{k}$
2. Search step size according to some principle
3. Accept or reject updated state according to belief field
$${\bm{z}}^{k}={\bm{x}}^{k}+{\bm{d}}^{k}$$
$${\bm{d}}^{k}=\underset{\bm{d}}{\mathrm{argmin}}{\left({\bm{g}}^{k}\right)}^{T}\bm{d}+{\bm{d}}^{T}\bm{B}\bm{d},\ s.t.\ {\Vert \bm{d}\Vert}_{2}\le \Delta_{k}$$
  $${\bm{x}}^{k+1}={\bm{z}}^{k}$$

  $${\bm{x}}^{k+1}={\bm{x}}^{k}$$

Classical gradient descent
  Large magnitude gap in different directions of gradient => "Z" descent trajectory(with optimal step size)
  Proof:
    $${x}^{k+1}={x}^{k}-{\mathit{\alpha}}^{\ast}{\nabla}_{\bm{x}}f\left({x}^{k}\right)$$
    Assume the step size is optimal
    $$\frac{\partial f\left({x}^{k}-{\mathit{\alpha}}^{\ast}{\nabla}_{{x}^{k}}f\left({x}^{k}\right)\right)}{\mathit{\partial}\mathit{\alpha}}=0$$
$$\Rightarrow {\nabla}_{{x}^{k+1}}f{\left({x}^{k+1}\right)}^{T}{\nabla}_{{x}^{k}}f\left({x}^{k}\right)=0$$
  So gradients from current step and next step are perpendicular, results in "Z" descent trajectory

Newton method
  Rectify the magnitude of gradients by using second order information
  Using taylor expansion (to 2-ord) to get new function has gradient = 0
  $$f\left(\bm{x}\right)=f\left({\bm{x}}^{k}\right)+\nabla f\left({\bm{x}}^{k}\right)\left(\bm{x}-{\bm{x}}^{k}\right)+\frac{1}{2}{\left(\bm{x}-{\bm{x}}^{k}\right)}^{T}{\nabla}^{2}f\left({\bm{x}}^{k}\right)\left(\bm{x}-{\bm{x}}^{k}\right)$$
  $$\nabla f\left(\bm{x}\right)=0$$
$$\Rightarrow \nabla f\left({\bm{x}}^{k}\right)+{\nabla}^{2}f\left({\bm{x}}^{k}\right)\left(\bm{x}-{\bm{x}}^{k}\right)=0$$
  $$\Rightarrow \bm{x}={\bm{x}}^{k}-{\left({\mathit{\nabla}}^{2}f\left({\bm{x}}^{k}\right)\right)}^{-1}\mathit{\nabla}f\left({\bm{x}}^{k}\right)$$
  $$\Rightarrow {\bm{d}}^{k}={\left({\nabla}^{2}f\left({\bm{x}}^{k}\right)+{\bm{E}}^{k}\right)}^{-1}\nabla f\left({\bm{x}}^{k}\right),\ rectified,\ ensurese\ inversible$$
  $$\Rightarrow {\bm{x}}^{k+1}={\bm{x}}^{k}-{\mathit{\alpha}}_{k}{\left({\nabla}^{2}f\left({\bm{x}}^{k}\right)+{\bm{E}}^{k}\right)}^{-1}\nabla f\left({\bm{x}}^{k}\right)$$
  Note with too large ${\bm{E}}^{\bm{k}}$, Newton method degenerates to classical descent

Simulated-Newton method
  $$\nabla f\left(\bm{x}\right)=\nabla f\left({\bm{x}}^{k+1}\right)+{\nabla}^{2}f\left({\bm{x}}^{k+1}\right)\left(\bm{x}-{\bm{x}}^{k+1}\right),\ {x}^{k}=x$$
  $$\nabla f\left({\bm{x}}^{k+1}\right)-\nabla f\left({\bm{x}}^{k}\right)={\nabla}^{2}f\left({\bm{x}}^{k+1}\right)\left({\bm{x}}^{k+1}-{\bm{x}}^{k}\right)$$
  $${\mathbf{y}}^{\mathrm{k}} = {\nabla}^{2}f\left({\bm{x}}^{k+1}\right){\bm{s}}^{\bm{k}},\left\{\begin{array}{c}{\bm{y}}^{k}=\nabla f\left({\bm{x}}^{k+1}\right)-\nabla f\left({\bm{x}}^{k}\right)\\ {\bm{s}}^{\bm{k}}={\bm{x}}^{k+1}-{\bm{x}}^{k}\end{array}\right.$$
   ${\mathbf{y}}^{\mathrm{k}}=$ ${\bm{B}}^{k+1}{\bm{s}}^{k}$, positive definite
  $${\left({\bm{s}}^{k}\right)}^{T}{\bm{B}}^{k+1}{\bm{s}}^{k}={\left({\bm{s}}^{k}\right)}^{T}{\bm{y}}^{k}>0$$
  Update ${\bm{B}}^{k}$
  SR1: ${\bm{B}}^{k+1}={\bm{B}}^{k}+a\bm{u}{\bm{u}}^{T}$
    Cannot guarantee positive definite
  BFGS: ${\bm{B}}^{k+1}={\bm{B}}^{k}+a\bm{u}{\bm{u}}^{T}+b\bm{v}{\bm{v}}^{T}$

Sub gradient
  $$\partial f\left(\bm{x}\right)=\left\{\bm{g}|\bm{g}\in {R}^{n},f\left(\bm{y}\right)\ge f\left(\bm{x}\right)+{\bm{g}}^{T}\left(\bm{y}-\bm{x}\right),\forall \bm{y}\in domf\right\}$$
  Any gradient in sub-gradients may not be the descent direction
  e.g. $f\left(x\right)={\Vert x\Vert}_{1},\ \nabla f\left(0\right)\in \left[-1,\ 1\right],minf=f\left(0\right)=0$
  $$f\left(0+\mathit{\alpha}\nabla f\left(0\right)\right)\ge 0$$  
    
Search of step size
  Assistant function
    $$\varphi \left(\mathit{\alpha}\right)=f\left({\bm{x}}^{k}+\mathit{\alpha}{\bm{d}}^{k}\right),\mathit{\alpha}>0$$
    Appropriate ${\alpha}_{k}$ should descent $f\left(x\right)$ well
    Should not compute consuming on searching ${\alpha}_{k}$
  Brute-force
    $${\alpha}_{k}=\underset{\mathit{\alpha}}{\mathrm{argmin}}\varphi \left(\mathit{\alpha}\right)$$
  Armijo principle:
    $$f\left({\bm{x}}^{k}+\mathit{\alpha}{\bm{d}}^{k}\right)\le f\left({\bm{x}}^{k}\right)+{c}_{1}\mathit{\alpha}\bm{\nabla}\bm{f}{\left({\bm{x}}^{k}\right)}^{T}{\bm{d}}^{k}$$
      $$\mathrm{s}.\mathrm{t}.\ \mathit{\nabla}\bm{f}{\left({\bm{x}}^{k}\right)}^{T}{\bm{d}}^{k}<0;{c}_{1}\in \left(0,\ 1\right)$$
    Equivalent to $\varphi \left(\mathit{\alpha}\right)\le \varphi \left(0\right)+{c}_{1}\mathit{\alpha}\bm{\nabla}\bm{f}{\left({\bm{x}}^{k}\right)}^{T}{\bm{d}}^{k}=l\left(\mathit{\alpha}\right)$
    Require $\left(\alpha ,\varphi \left(\mathit{\alpha}\right)\right),\ and\ corresponding\ \left(\bm{x},f\left(\bm{x}\right)\right)$ below line $l\left(\mathit{\alpha}\right)$
    i. Require descent each step monotomically, or
  ii. Require descent after M steps, to jump out of local optimal
    May result over-small $\mathit{\alpha}$
  Goldstein principle
    Require $\left(\alpha ,\varphi \left(\mathit{\alpha}\right)\right)$ above line while meet Armijo principle
      $$f\left({\bm{x}}^{k}+\mathit{\alpha}{\bm{d}}^{k}\right)\ge f\left({\bm{x}}^{k}\right)+\left(1-{c}_{1}\right)\mathit{\alpha}\bm{\nabla}\bm{f}{\left({\bm{x}}^{k}\right)}^{T}{\bm{d}}^{k}$$
    To avoid over-small $\mathit{\alpha}$
    May result missing local optima
  Wolfe principle
    Require ${\varphi}^{\prime}\left(\mathit{\alpha}\right)\ge {c}_{2}{\varphi}^{\prime}\left(0\right)$ while meet Armijo principle, ${\mathrm{c}}_{1}>{c}_{2}$
    i.e. $\left(\alpha ,\varphi \left(\mathit{\alpha}\right)\right)$ should has direction derivative close to $\left(0,\varphi \left(0\right)\right)$
    While decrease $f\left(x\right)$ well

Convergence premise
  Gradient satisfies Lipstic continuous
    $$\left|\left|\nabla f\left(x\right)-\nabla f\left(y\right)\right|\right|\le L\left|\left|x-y\right|\right|$$
  and weith Woffe step size won't ensure montonical movement, especially when far from ${x}^{\ast}$
    $$\angle \left(-\bm{\nabla}\bm{f}\left({\bm{x}}^{k}\right),{\bm{d}}^{k}\right)<{90}^{o}\Rightarrow \mathrm{cos}{\mathit{\theta}}_{k}$$
  Second order gradient satisfies Lipsic continuous will make converge fast when close to ${x}^{\ast}$, but require good initialization  
    
Approximate
  Low frequent information -> high frequent information (by high-ord derivative)

Vicinity gradient for solving non-smooth part, e.g. regularization part
Vicinity operator
  Find a point **u** close to $\bm{x}$ while has its $\mathrm{h}\left(\bm{u}\right)$ as small as possible
  $${\mathrm{prox}}_{h}\left(\bm{x}\right)=\underset{\bm{u}}{\mathrm{argmin}}\left(h\left(\bm{u}\right)+\frac{1}{2}{\Vert \bm{u}-\bm{x}\Vert}_{2}^{2}\right)$$
  The objective is a strong convex function if $\mathrm{h}\left(\bm{u}\right)$ is a convex function
  $$0\in \mathit{\partial}{\mathrm{prox}}_{h}\left(\bm{x}\right)\Rightarrow \bm{x}-\bm{u}\in \mathit{\partial}h\left(\bm{u}\right)$$
  Approximate gradient
    $$\mathrm{min}\psi \left(\bm{x}\right)=f\left(\bm{x}\right)+\mathrm{h}\left(\bm{x}\right)$$
    $${\bm{x}}^{k+1}=pro{x}_{{t}_{k}h}\left({\bm{x}}^{k}-{t}_{k}\mathit{\nabla}\bm{f}\left({\bm{x}}^{k}\right)\right)$$
  1. Gradient descent on smooth part
2. Vicinity operator on non-smooth part after updating smooth part

Composed optimization
  Split descent and constraint
1. Do descent without constraint
2. Project back into constrint space (by updating parameters in control of constrint)
Augmented Lagrange
  $${L}_{\mathit{\sigma}}\left(x,\mathit{\lambda}\right)=f\left(x\right)+{\sum}_{i\in \mathcal{E}}{\mathit{\lambda}}_{i}{c}_{i}\left(x\right)+\frac{1}{2}\mathit{\sigma}{\sum}_{i\in \mathcal{E}}{c}_{i}^{2}\left(x\right)$$
  For optimal
  $${\nabla}_{x}{L}_{{\mathit{\sigma}}^{k}}\left({x}^{k+1},{\mathit{\lambda}}^{k}\right)=\nabla f\left({x}^{k+1}\right)+{\sum}_{i\in \mathcal{E}}\left({\mathit{\lambda}}_{i}^{k}+{\mathit{\sigma}}_{k}{c}_{i}\left({x}^{k+1}\right)\right)\nabla {c}_{i}\left({x}^{k+1}\right)=0$$
  Should be consistent with Lagrange solution, for large k
  $$\Rightarrow \nabla f\left({x}^{\ast}\right)+{\sum}_{i\in \mathcal{E}}{\mathit{\lambda}}_{i}^{\ast}\nabla {c}_{i}\left({x}^{\ast}\right)=0\Rightarrow {\mathit{\lambda}}_{i}^{\ast}\approx {\mathit{\lambda}}_{i}^{k}+{\mathit{\sigma}}_{k}{c}_{i}\left({x}^{k+1}\right),\forall i\in \mathcal{E}$$
Update lagrange multiplier can mitegate violation
  $${x}^{k+1}=\underset{x}{\mathrm{argmin}}{L}_{\mathit{\sigma}}\left(x,{\mathit{\lambda}}^{k}\right)$$
  $$\Rightarrow {\lambda}_{\mathrm{i}}^{\mathrm{k}+1}={\mathit{\lambda}}_{i}^{k}+{\mathit{\sigma}}_{k}{c}_{i}\left({x}^{k+1}\right),\forall i\in \mathcal{E}$$  
    
ADMM
  $$\underset{{\bm{x}}_{1},{\bm{x}}_{2}}{\mathrm{min}}{f}_{1}\left({\bm{x}}_{1}\right)+{f}_{2}\left({\bm{x}}_{2}\right)\ .s.t.\ {\bm{A}}_{1}{\bm{x}}_{1}+{\bm{A}}_{2}{\bm{x}}_{2}=b$$
  Non constraint to constraint
    $$\underset{x}{\mathrm{min}}f\left(x\right)+r\left(x\right)\Rightarrow \underset{x,y}{\mathrm{min}}f\left(x\right)+r\left(y\right).s.t\ x-y=0$$
  Lagrange to augmented Lagrange with panty function
    $${\mathrm{L}}_{\mathit{\rho}}\left({\bm{x}}_{1},{\bm{x}}_{2},\bm{y}\right)={f}_{1}\left({\bm{x}}_{1}\right)+{f}_{2}\left({\bm{x}}_{2}\right)+{\bm{y}}^{T}\left({\bm{A}}_{1}{\bm{x}}_{1}+{\bm{A}}_{2}{\bm{x}}_{2}-b\right)$$
$$+\frac{\mathit{\rho}}{2}{\Vert {\bm{A}}_{1}{\bm{x}}_{1}+{\bm{A}}_{2}{\bm{x}}_{2}-b\Vert}_{2}^{2}$$
  Update target arguments and Lagrange multipliers
    $$\left({x}_{1}^{k+1},{x}_{2}^{k+1}\right)=\underset{{x}_{1},{x}_{2}}{\mathrm{argmin}}{L}_{\mathit{\rho}}\left({x}_{1},{x}_{2},{y}^{k}\right)$$
    $${\mathrm{y}}^{\mathrm{k}+1}={\mathrm{y}}^{\mathrm{k}}+\tau \mathit{\rho}\left({\bm{A}}_{1}{\bm{x}}_{1}^{\bm{k}+1}+{\bm{A}}_{2}{\bm{x}}_{2}^{k+1}-b\right)$$
  Update alternatively
    $${x}_{1}^{k+1}=\underset{{x}_{1}}{\mathrm{argmin}}{L}_{\mathit{\rho}}\left({x}_{1},{x}_{2},{y}^{k}\right)$$
    $${x}_{2}^{k+1}=\underset{{x}_{2}}{\mathrm{argmin}}{L}_{\mathit{\rho}}\left({x}_{1},{x}_{2},{y}^{k}\right)$$
    $${\mathrm{y}}^{\mathrm{k}+1}={\mathrm{y}}^{\mathrm{k}}+\tau \mathit{\rho}\left({\bm{A}}_{1}{\bm{x}}_{1}^{k+1}+{\bm{A}}_{2}{\bm{x}}_{2}^{k+1}-b\right)$$  
      
