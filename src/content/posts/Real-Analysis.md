---
title: Real Analysis
published: 2023-10-05
description: "Build Real space from scratch"
tags: ["Set", "Natural Number", "Ratio Number", "Real Number"]
category: Top-Design
draft: false
---

## Start Over: Redefinition of Number System

It's important to axiomatically define Number System, instead of constructing them.
i.e. we don’t create their physical image or any essence they should connect to the real world, like, what are they made of? are they attachment to physical conception ?
We extract them from the natural world and generalize them to an abstract form by only describing properties and operations related.
As the old quote goes: one is the child of the divine law, after one come two, after two come three, after three come all things. So we can define any complex derivative from its simple origin
The process of redefinition of number system is to slowly fill every spot on the number axis

## Natural Number Set

$$
\mathbb{N}=\left\{0,1,2,3,4,\dots \right\}
$$

**Properties** of $\forall \ n\in \mathbb{N}$  
Peano axiom 1

$$
0\in \mathbb{N}
$$

Peano axiom 2: increment closure  
  n is result after recursively applying increment on 0

$$
\mathrm{n}=\left(\left(0++\right)++\right)++\dots 
$$

$$
n\in \mathbb{N}\Rightarrow n++\in \mathbb{N},\ \ 
$$

Question: $n++ \in N \Rightarrow n \in N $ ? or $∃?n∈N,n++=0 n++\in \mathbb{N}\Rightarrow n\in \mathbb{N} ?$ or $ \exists ?n\in \mathbb{N},n++=0$  
Peano axiom 3: non-wrap-around

$$
n++\ne 0
$$

Peano axiom 4: identity, multual exclusive of elements in set

$$
n,m\in \mathbb{N},n\ne m\Rightarrow n++\ne m++
$$

Bug: $\mathrm{n}=0.5,\mathrm{m}=1.5$ still satisfy, but they are not natural numbers
So we need to exclude numbers violating properties of natural numbers

Peano axiom (schema) 5: Induction  
  All natural numbers have their properties **consistently followed** with 0(its predecessor)

$$
p\left(0\right)\ true\Rightarrow p\left(0++\right)\ true\Rightarrow p\left(\left(0++\right)++\right)\ true\Rightarrow \dots \Rightarrow p\left(n++\right)\ true
$$

$$
if\ p\left(0\right)\ true,\ p\left(n\right)\ true\Rightarrow p\left(n++\right)\ true
$$

$$
\mathrm{then}\ \forall \ n\ ,p\left(n\right)\ true
$$

  e.g. $p\left(n\right):n\ is\ not\ half\ natural\ number$

### Addition of Natural Number  
Base on axioms 1 to 5, we now can recursively define sequence

$$
\forall \ n\in \mathbb{N},\exists {f}_{n}:\mathbb{N}\to \mathbb{N},\ uniquely\ \exists {a}_{n}\left\{\begin{array}{c}{a}_{0}=c,c\in \mathbb{N}\\ {a}_{n++}={f}_{n}\left({a}_{n}\right)\end{array}\right.
$$

$$
{f}_{n}\left({a}_{n}\right)={a}_{n}++
$$

$$
\left\{\begin{array}{c}{a}_{0}=0+m=m\\ {a}_{1}=f\left({a}_{0}\right)=\left(0++\right)+m=m++\\ \vdots \\ {a}_{n}=n+m\\ {a}_{n++}=f\left({a}_{n}\right)=\left(n++\right)+m=\left(n+m\right)++\end{array}\right.
$$

Definition of addition has same form as induction (Peano axiom 5)

$$
\forall \ n,m\in \mathbb{N},n+m\left\{\begin{array}{c}0+m=m\\ assume\ n+m\ is\ already\ known\\ \left(n++\right)+m=\left(n+m\right)++\end{array}\right.
$$

Properties : All can be proved by following the same pattern as Induction
(1) commutative law

$$
\mathrm{n}+\mathrm{m}=\mathrm{m}+\mathrm{n}
$$

  Informal Proof
  (i) $\mathrm{prove}\ 0+\mathrm{m}=\mathrm{m}+0,\ \mathrm{by}$

$$
\left\{\begin{array}{c}0+m=m\\ n+0=n\end{array}\right.
$$

  (ii) assume $\mathrm{n}+\mathrm{m}=\mathrm{m}+\mathrm{n}$
  (iii) prove $\left(\mathrm{n}++\right)+\mathrm{m}=\mathrm{m}+\left(n++\right),\ by$

$$
\left\{\begin{array}{c}\left(n++\right)+m=\left(n+m\right)++\\ n+\left(m++\right)=\left(n+m\right)++\end{array}\right.
$$

(2) associative law

$$
a+\left(b+c\right)=\left(a+b\right)+c,\ \forall a,b,c\in \mathbb{N}
$$

(3) elimination law

$$
a+b=a+c\Rightarrow b=c
$$

Order built on addition

$$
\left\{\begin{array}{c}n\ge m\Rightarrow n=m+a,a\in \mathbb{N}\\ n>m\Rightarrow n=m+a,a\in \mathbb{N},a\ne 0\end{array}\right.
$$

$$
\forall n,m\in \mathbb{N}\Rightarrow \left\{\begin{array}{c}n<m\\ n=m\\ n>m\end{array}\right.,\ only\ one\ predicate\ is\ true
$$

Note that order is a shared property among entities
i.e. an entity can be ordered only when it can be bounded by other entities
For Natural Number, we can find that:

$$
\forall \ i\in N,\exists n,m\in N,\ n\le i<m
$$

While for infinite, i.e. $\pm \infty $, there is no such entity can bound it, so it doesn't have property of order.
So it is for the order definition in Integer, proportional number and real number, their order all build on in such way.
Order + Peano axiom 5 = Strong Induction

$$
{m}_{0},m,{m}^{\prime}\in \mathbb{N},\forall m\ge {m}_{0},{m}_{0}\le {m}^{\prime}<m,\ p\left({m}^{\prime}\right)\ true\Rightarrow p\left(m\right)\ true
$$

e.g. converge of series

$$
p\left(n\right):\left|{a}_{n}-A\right|<\mathit{\epsilon}
$$

$$
{n}_{0},n,{n}^{\prime}\in \mathbb{N},\forall n\ge {n}_{0},{n}_{0}\le {n}^{\prime}<n,\ \left|{a}_{{n}^{\prime}}-A\right|<\mathit{\epsilon}\Rightarrow {a}_{n}\to A
$$

### Multiplication of Natural Number

Follow the same thoughts as did in defining addition, we can define multiplication

$$
\forall \ n,m\in \mathbb{N},n\times m\left\{\begin{array}{c}0\times m=0\\ assume\ n\times m\ is\ already\ known\\ \left(n++\right)\times m=\left(n\times m\right)+m\end{array}\right.
$$

Properties :
(1) commutative law

$$
\mathrm{n}\times \mathrm{m}=\mathrm{m}\times \mathrm{n}
$$

  Informal Proof
  (i) $\mathrm{prove}\ 0\times \mathrm{m}=\mathrm{m}\times 0,\ \mathrm{by}$

$$
\left\{\begin{array}{c}0\times m=m\\ n\times 0=n\end{array}\right.
$$

  (ii) assume $\mathrm{n}\times \mathrm{m}=\mathrm{m}\times \mathrm{n}$
  (iii) prove $\left(\mathrm{n}++\right)\times \mathrm{m}=\mathrm{m}\times \left(n++\right),\ by$

$$
\left\{\begin{array}{c}\left(n++\right)\times m=\left(n\times m\right)+m\\ n\times \left(m++\right)=\left(n\times m\right)+n\end{array}\right.
$$

(2) distributive law

$$
a\times \left(b+c\right)=a\times b+a\times c,\ \forall a,b,c\in \mathbb{N}
$$

(3) associative law

$$
a\times \left(b\times c\right)=\left(a\times b\right)\times c
$$

(4) order preservation

$$
a<b,c\ne 0\Rightarrow a\times c<b\times c
$$

(5) elimination law

$$
a\times b=a\times c,a\ne 0\Rightarrow b=c
$$

**Euclidean Algorithm**: represent number with combination of addition and multiplication

$$
n,q\in \mathbb{N},q\ne 0,\exists m,r\in \mathbb{N},0\le r<q\Rightarrow n=mq+r
$$

  Or in a familiar form $\mathrm{n}/\mathrm{q}=\mathrm{m}\dots \mathrm{r}$
**Exponential Operation** of Natural Number

$$
\forall \ n,m\in \mathbb{N},{m}^{n}\left\{\begin{array}{c}{m}^{0}=1\\ assume\ {m}^{n}\ is\ already\ known\\ {m}^{n++}={m}^{n}\times m\end{array}\right.
$$


## Set  
We now can generalize the **natural number set** into more abstract one

$$
\mathrm{A}:\left\{{x}_{1},{x}_{2},\dots ,{x}_{k}\right\},i,k\in \mathbb{N}\ \left\{\begin{array}{c}{x}_{i}\in A,1\le i\le k\\ {x}_{i}\notin A,i>k\end{array}\right.
$$

Axioms of equality on class T
(1) reflexive

$$
\forall \ x\in T,\ x=x
$$

(2) symmetric

$$
\forall x,y\in T,x=y\iff y=x
$$

(3) transitive

$$
\forall x,y,z\in T,x=y,y=z\Rightarrow x=z
$$

(4) substitutive

$$
\forall x,y\in T,\forall f:T\to T,x=y\iff f\left(x\right)=f\left(y\right)
$$

$$
\forall x,y\in T,\forall P:T\to \left\{0,1\right\},x=y\iff P\left(x\right)\equiv P\left(y\right)
$$

**Zermelo-Fraenkel axiom 1**: identity of set

$$
\mathrm{A}\ \mathrm{is}\ \mathrm{an}\ \mathrm{object},\ \mathrm{A}=\mathrm{B}\iff \forall x\in A,x\in B\ and\ \forall y\in B,y\in A
$$

$$
\mathrm{distinct}:\ \mathrm{A}\ne \mathrm{B}\Rightarrow \exists x\in A,x\notin B
$$

  Note: That means set itself can be an element of another set
   $\in $** follow the substitutive axiom**

$$
\mathrm{P}\left(A\right):x\in A,A=B\Rightarrow P\left(B\right):x\in B
$$

$$
\Rightarrow A=B\Rightarrow P\left(A\right)=P\left(B\right)
$$

**So the following axioms will base on **$\in $** to maintain substitutive**  
**Why? Operation following substitutive is a successfully defined one**  
**Zermelo-Fraenkel axiom 2**: origin of a set, empty set
  Any set exist at the contrast to empty set

$$
\exists \varnothing =\left\{\right\},\forall x,x\notin \varnothing \Rightarrow A\ne \varnothing ,\exists x,x\in A
$$

**Zermelo-Fraenkel axiom 3**: basic unique sets, for constructing bigger set
  singleton set: $\mathrm{A}=\left\{a\right\},\forall x\in A,x=a$
  pair set: $\mathrm{B}=\left\{a,b\right\},\forall y\in B,y=a\ or\ y=b$  
**Zermelo-Fraenkel axiom 4**: Dual Union operation, method for constructing bigger set

$$
x\in A\cup B\iff x\in A\ or\ x\in B
$$

  **Again! Dual Union was defined on **$\in $
  **And it follows substitutive**

$$
{B}^{\prime}=B,P\left(B\right):x\in A\cup B\Rightarrow P\left({B}^{\prime}\right):x\in A\cup {B}^{\prime}
$$

  Properties of Dual Union: All these can be proved by substitutive of $\in $
  (1) commutative ; (2) associative ;
  **Subset** can be derived from Dual Union operation

$$
\mathrm{\Omega}=A\cup B\Rightarrow \left\{\begin{array}{c}A\subseteq \mathrm{\Omega}:\ \forall x\in A\Rightarrow x\in \mathrm{\Omega}\\ A\subset \mathrm{\Omega}:\ ,A\ne \mathrm{\Omega},\forall x\in A\Rightarrow x\in \mathrm{\Omega}\end{array}\right.
$$

  $\mathrm{A}$ is sub set of $\mathrm{\Omega}$
  Subset implicates relationship of **order**

$$
\left\{\begin{array}{c}A\subseteq B,B\subseteq C\Rightarrow A\subseteq C\\ A\subseteq B,B\subseteq A\Rightarrow A=B\\ A\subset B,B\subset C\Rightarrow A\subset C\end{array}\right.
$$

**Zermelo-Fraenkel axiom 5: Separation axiom, **constructing subset from a big set

$$
B=\left\{x\in A:P\left(x\right)=1\right\}\Rightarrow B\subseteq A
$$

$$
\Rightarrow x\in A,P\left(x\right)=0\Rightarrow \varnothing \subseteq A
$$

$$
y\in \left\{x\in A:P\left(x\right)=1\right\}\iff y\in A\ and\ P\left(y\right)=1
$$

  We can use it to define **Intersection** and **Difference**

$$
{S}_{1}\cap {S}_{2}=\left\{x\in {S}_{1}|P\left(x\right):x\in {S}_{2}\right\}=\left\{x\in {S}_{2}|P\left(x\right):x\in {S}_{1}\right\}=\left\{x\in {S}_{1}:x\in {S}_{2}\right\}
$$

$$
x\in {S}_{1}\cap {S}_{2}\iff x\in {S}_{1}\ and\ x\in {S}_{2}
$$

$$
{S}_{1}-{S}_{2}=\left\{x\in {S}_{1}|P\left(x\right):x\notin {S}_{2}\right\}=\left\{x\in {S}_{1}:x\notin {S}_{2}\right\}
$$

$$
x\in {S}_{1}-{S}_{2}\iff x\in {S}_{1}\ and\ x\notin {S}_{2}
$$

  Duality: $A\to X\backslash A\ or\ A\to ~A,X\to \varnothing $
  The dual statement of $\left(A\cup B\right)$ is obtained by $\sim \left(~A\cup ~B\right)=\left(A\cap B\right)$, or
   $\left\{\begin{array}{c}X\backslash \left(A\cup B\right),X\backslash \left(A\cap B\right)\\ A\cup \left(X\backslash \mathrm{A}\right)=X,A\cap \left(X\backslash \mathrm{A}\right)=\varnothing \end{array}\right.$ are dual statements of each other  
But for now, we are only circle around inside a set, to jump out of a set into another form of set, we need more powerful axiom  

**Zermelo-Fraenkel axiom 6: Replacement axiom**  

$$
\mathrm{z}\in \left\{y:\exists x\in A,P\left(x,y\right)=1\right\}\iff \exists x\in A,P\left(x,z\right)=1,\ \ P\left(x,y\right):T\times T\to \left\{0,1\right\}
$$

  Or $\mathrm{P}\left(x,y\right)\equiv y=f\left(x\right)\Rightarrow \left\{y:\exists x\in A,y=f\left(x\right)\right\}$
  We use **Separation axiom** to tease out subset and transform its elements into new form by **Replacement axiom**
  Connection between Replacement and Separation
    **Replacement axiom **can be seen as **Separation axiom** of Set y belong to

$$
\left\{y:\exists x\in A,P\left(x,y\right)=1\right\}\equiv \left\{y\in Y|P\left(y,x\right):x\in A,y=f\left(x\right)\right\}
$$


**Zermelo-Fraenkel axiom 7: Infinite Set, Specialize to Natural Number Set**  

$$
\mathbb{N}=\left\{n|P\left(n\right):n\ satisfies\ \bm{P}\bm{e}\bm{a}\bm{n}\bm{o}\ \bm{A}\bm{x}\bm{i}\bm{o}\bm{m}\bm{s}\right\}
$$

Actually, axiom 1 to 7 can generalize to a generalization of Separation Axiom  
**Zermelo-Fraenkel axiom 8: axiom comprehension, Universal Separation axiom**  

$$
\mathrm{y}\in \left\{x:P\left(x\right)=1\right\}\iff P\left(y\right)=1,\ \ \forall x,P\left(x\right)
$$

Russell Paradox: Axiom 8 failed under such property

$$
{P}_{R}\left(x\right):x\ is\ a\ set,\ x\notin x
$$

  Proof:
    Axiom 8 allows us to define a universal set $\mathrm{S}$ as set of any sets(including itself)

$$
\mathrm{i}.\mathrm{e}.\ S\in S,S=\left\{S,\mathrm{\Omega}\dots \right\},\mathrm{\Omega}=\left\{x:x\in S,{P}_{R}\left(x\right)=1\right\}
$$

  If $\mathrm{\Omega}\notin \mathrm{\Omega}\Rightarrow {\mathrm{P}}_{R}\left(\mathrm{\Omega}\right)=1\Rightarrow \mathrm{\Omega}\in \mathrm{\Omega}$
    Else $\mathrm{\Omega}\in \mathrm{\Omega}\Rightarrow {\mathrm{P}}_{R}\left(\mathrm{\Omega}\right)=0\Rightarrow \mathrm{\Omega}\notin \mathrm{\Omega}$  

**Zermelo-Fraenkel axiom 9: foundation axiom, regularity, patch for axiom 8**  

$$
A\ne \varnothing \Rightarrow \exists x\in A,\ x\left\{\begin{array}{c}\ne A,\ if\ x\ is\ set\\ x\ is\ not\ set\end{array}\right.\Rightarrow A\notin A
$$


Now function can be defined as mapping between sets

$$
P\left(x,y\right)=1\Rightarrow y=f\left(x\right),\ \ P:X\times Y\to \left\{0,1\right\}\Rightarrow f:X\to Y
$$

And Again!, it has to follow the **law of substitutive**

$$
\forall x,{x}^{\prime}\in X,\exists y\in Y,x={x}^{\prime},P\left(x,y\right):y=f\left(x\right)\Rightarrow P\left({x}^{\prime},y\right):y=f\left({x}^{\prime}\right)
$$

$$
x={x}^{\prime}\Rightarrow f\left(x\right)=f\left({x}^{\prime}\right)
$$

  That means, any $x$ in $X$ for a function can only map to one $y$ in $Y$
Properties of function can be derived from axioms of set
(1) equality

$$
f:X\to Y,g:X\to Y
$$

$$
\forall x\in X,f\left(x\right)=g\left(x\right)\iff f=g
$$

(2) compound

$$
f:X\to Y,g:Y\to Z
$$

$$
\left(g\circ f\right)\left(x\right)=g\left(f\left(x\right)\right):X\to Z
$$

(3) injective

$$
x={x}^{\prime}\iff f\left(x\right)=f\left({x}^{\prime}\right)
$$

(4) surjective

$$
\forall y\in Y,\exists x\in X\Rightarrow y=f\left(x\right)
$$

(5) bijective = injective & surjective

$$
\forall y\in Y,\exists x\in X\Rightarrow x={f}^{-1}\left(y\right),\ \ \exists {f}^{-1}:Y\to X
$$

**How big is a Set**:
Cardinal of set is defined by a bijective function(it's similar to count number from 1 to n)

$$
f:X\to \left\{i\in \mathbb{N}:1\le i\le n\right\}\iff \#\left(X\right)=n
$$

  Also, the bijective function to $\mathbb{N}$ indicates **measurable** of $X$, since $\mathbb{N}$ is a measurable set, so is $X$
  Now we can prove axiom 7, why $\mathbb{N}$ is a infinite set
    Assume $\#\left(\mathbb{N}\right)=n$

$$
\Rightarrow \exists bijective\ f:\left\{i\in \mathbb{N}:1\le i\le n\right\}\to \mathbb{N}
$$

$$
\Rightarrow \exists M\in \mathbb{N},\forall i\in \left\{i\in \mathbb{N}:1\le i\le n\right\},f\left(i\right)\le M
$$

$$
\Rightarrow M++\notin \mathbb{N},\text{ contradict to Peano axiom 2}
$$

Equality of Cardinal
  Existence of bijective function between $X$ and $Y$

$$
f:X\to \left\{i\in \mathbb{N}:1\le i\le n\right\},\ \ g:Y\to \left\{i\in \mathbb{N}:1\le i\le n\right\}\Rightarrow {g}^{-1}:\left\{i\in \mathbb{N}:1\le i\le n\right\}\to Y
$$

$$
\Rightarrow \mathrm{h}=\left({g}^{-1}\circ f\right):X\to Y\Rightarrow \#\left(X\right)=\#\left(Y\right)
$$

**Zermelo-Fraenkel axiom 10: power set, set of functions**  
  If we treat function as an object, then we can have set of functions

$$
f\in {Y}^{X},{Y}^{X}=\left\{\forall f:X\to Y\right\}
$$

  e.g. ${2}^{\mathrm{X}}=\left\{Z:Z\subseteq X\right\}:P\left(X\right):X\to \left\{0,1\right\}$  
  
**Zermelo-Fraenkel axiom 11: Union, for constructing way larger set**  

$$
x\in \bigcup A\iff \exists S\in A,x\in S,\ or
$$

$$
x\in {\cup}_{I\in \mathit{\alpha}}{A}_{\mathit{\alpha}}\iff \exists \mathit{\alpha}\in I,x\in {A}_{\mathit{\alpha}},\ \ A=\left\{{A}_{\mathit{\alpha}}:\mathit{\alpha}\in I\right\}
$$

## Integer Set  
Integer is a generalization of Natural Number, as subtraction result between two natural numbers

$$
\mathbb{Z}=\left\{a\text{—}b:\forall a,b\in \mathbb{N}\right\}
$$

  — is a placeholder for subtraction, since subtraction result directly on natural number is problematic--they can not represent as natural number, so it can only be defined on integer.
  And we can not define subtraction between integers without firstly declaring it, which is subtraction result between natural numbers. In case of recurrent definition, a placeholder is needed.  
Now our simple idea is to define Integer as an analogy to natural number with all the axioms and operations we already testified
(1) identity (equality), follow substitutive

$$
\forall n,m\in \mathbb{Z},n=a\text{—}b,m=c\text{—}d
$$

$$
n=m\iff a+d=c+b
$$

(2) addition, follow substitutive

$$
n+m=\left(a+c\right)\text{—}\left(b+d\right)\in \mathbb{Z}
$$

(3) multiplication, follow substitutive

$$
nm=\left(ac+bd\right)-\left(ad+bc\right)\in \mathbb{Z}
$$

(4) negative, follow substitutive

$$
-n=0\text{—}\left(a\text{—}b\right)=0+\left(b\text{—}a\right)=b\text{—}a
$$

(5) trichofomy, if and only one holds

$$
\forall x\in \mathbb{Z}
$$

$$
x\left\{\begin{array}{c}=0\\ =n\\ =\text{—}n\end{array}\right.,\ \ n\in {\mathbb{N}}^{+}
$$

(6) base on definition of **negative**, now we can define subtraction between integers

$$
n-m=n+\left(-m\right)=n\text{—}0+\left(0\text{—}m\right)=n\text{—}m
$$

  Since it follows substitutive, now we can replace — with $-$  
Generalization of Natural Number
  Order, we can redefine order with subtraction

$$
\left\{\begin{array}{c}n\ge m\Rightarrow n-m\ge 0\\ n>m\Rightarrow n-m>0\end{array}\right.
$$

  order preservation with negative operation

$$
\mathrm{n}>\mathrm{m}\Rightarrow -\mathrm{n}<-\mathrm{m}
$$

  Integer fill symmetric part for Natural Number on the left side of 0 by subtraction
Now any property of natural number is compatible with integer, so any natural number is a integer, we complete the construction of integer(added with subtraction)

## Proportional Number Set

Proportional Number is a generalization of Integer, as division result between two Integers

$$
\mathbb{Q}=\left\{a//b,\forall a,b\in \mathbb{Z},b\ne 0\right\}
$$

  // is a placeholder for division, since definition of division base on definition of Proportional number.
  And we can not define division between proportional numbers without firstly declaring it, which is division result between integers. In case of recurrent definition, a placeholder is needed.
Now our simple idea is to define Proportional number as an analogy to Integer with all the axioms and operations we already testified
(1) identity (equality), follow substitutive

$$
\forall x,y\in \mathbb{Q},x=a//b,y=c//d
$$

$$
x=y\iff ad=cb
$$

(2) addition, follow substitutive

$$
x+y=\left(ad+bc\right)//\left(bd\right)\in \mathbb{Q}
$$

(3) multiplication, follow substitutive

$$
xy=ac//bd\in \mathbb{Q}
$$

(4) negative, follow substitutive

$$
-x=0-\left(a//b\right)=(-a)//b\in \mathbb{Q}
$$

(5) inverse, follow substitutive

$$
\forall x\in \mathbb{Q},x\ne 0,{x}^{-1}=b//a
$$

$$
x{x}^{-1}={x}^{-1}x=1
$$

(6) base on definition of **inverse**, now we can define division between proportional numbers

$$
x/y=x{y}^{-1}=\left(a//b\right)(d//c)=\left(a{b}^{-1}\right)/\left(d{c}^{-1}\right)\ =x//y,y\ne 0
$$

$$
a/b=a{b}^{-1}=a//b,b\ne 0
$$

  Since it follows substitutive, now we can replace // with $/$
(7) trichofomy, if and only one holds

$$
\forall x\in \mathbb{Q}
$$

$$
x\left\{\begin{array}{c}=0\\ =\frac{a}{b}\\ =-\frac{a}{b}\end{array}\right.,\ \ a,b\in \mathbb{Z},a>0,b\ne 0
$$

(8) absolute value can be built upon negative operation

$$
\forall x,y\in \mathbb{Q}
$$

$$
\left|x\right|=\left\{\begin{array}{c}x,x>0\\ 0,x=0\\ -x,x<0\end{array}\right.
$$

Distance can be built upon absolute operation and subtraction  
It can be used to measure how close are two proportional numbers
$\bm{\epsilon}$**\-approximate**: placehoder for defining **limit and Cauchy sequence**

$$
\mathrm{d}\left(x,y\right)\le \mathit{\epsilon}
$$


Generalization of Integer

$$
\forall x,y\in \mathbb{Q}
$$

  exponential operation

$$
\left|{x}^{n}\right|={\left|x\right|}^{n}
$$

$$
{x}^{-n}=\frac{1}{{x}^{n}}
$$

$$
{x}^{n}{x}^{m}={x}^{n+m},{\left({x}^{n}\right)}^{m}={x}^{nm},{\left(xy\right)}^{n}={x}^{n}{y}^{n}
$$

  order preservation with exponential operation

$$
x>y\ge 0\Rightarrow \left\{\begin{array}{c}{x}^{n}>{y}^{n}\ge 0,n>0\\ {x}^{n}<{y}^{n}<0,n<0\end{array}\right.
$$

Now any property of integer is compatible with proportional number, so any integer is a proportional number, we complete the construction of proportional number(added with division and absolute operation)  
  Any two Integers are separated by a proportional number

$$
\forall x\in \mathbb{Q},uniquely\ \exists n\in \mathbb{Z}\Rightarrow n\le x<n+1,n=\left[x\right]
$$

  There's huge empty space between two integers, proportional number fill it by division
  Any two proportional numbers are separated by a proportional number

$$
\forall x,y\in \mathbb{Q},x<y\Rightarrow \exists z\in \mathbb{Q},x<z<y
$$

**Is there exist empty space between two proportional numbers** ?

Void between proportional numbers

$$
\nexists x\in \mathbb{Q},{x}^{2}=2
$$

Proof:

$$
x=\frac{p}{q},p,q,k\in \mathbb{Z},q\ne 0
$$

$$
\Rightarrow {p}^{2}=2{q}^{2},q<p
$$

$$
\mathrm{if}\ \mathrm{p}=2\mathrm{k}+1
$$

$$
\Rightarrow 4{\mathrm{k}}^{2}+4\mathrm{k}+1=2\mathrm{q}\Rightarrow \mathrm{q}=2{\mathrm{k}}^{2}+2\mathrm{k}+\frac{1}{2}\notin \mathbb{Z}
$$

$$
\mathrm{if}\ \mathrm{p}=2\mathrm{k}
$$

$$
\Rightarrow {\mathrm{q}}^{2}=2{\mathrm{k}}^{2}\Rightarrow {\left({\mathrm{p}}_{1}\right)}^{2}=2{\left({\mathrm{q}}_{1}\right)}^{2},{\mathrm{q}}_{1}<{\mathrm{p}}_{1}=\mathrm{q}<\mathrm{p}
$$

$$
\dots 
$$

$$
\mathrm{p}={\mathrm{p}}_{0}>{p}_{1}>\dots >{p}_{n}>{p}_{n+1},n\in \mathbb{N}
$$

  But a sequence infinitely decreasing is not exist, since we can always have

$$
\forall n\in \mathbb{N},\exists \mathrm{M}\in \mathbb{Z},M\le {p}_{n}
$$

  We can only get a proportional number infinitely approximate to $\sqrt{2}$, that will yields a sequence of proportional numbers

$$
\forall \mathit{\epsilon}>0,d\left(x,\sqrt{2}\right)\le \mathit{\epsilon}
$$

  So we have two proportional numbers separated by $\sqrt{2}$

$$
{x}^{2}<2<{\left(x+\mathit{\epsilon}\right)}^{2}\Rightarrow x<\sqrt{2}<x+\mathit{\epsilon}
$$


## Real Number Set
  
**An instance of complete measure space, the idea behind generalization from Proportional Number to Real Number will be useful when defining a Hilbert Space**  
Real Number is a generalization of Proportional Number, as a limit of a **Cauchy sequence **on Proportional Number
Sequence

$$
{\left({a}_{n}\right)}_{n=m}^{\infty}:\left\{n,m\in \mathbb{Z}:n\ge m\right\}\to \mathbb{Q},{a}_{n}\in \mathbb{Q}\Rightarrow {a}_{m},{a}_{m+1},\dots 
$$

Bounded Sequence

$$
\exists M\in \mathbb{Q},M\ge 0,\forall i\in \left\{n,m\in \mathbb{Z}:n\ge m\right\},\left|{a}_{i}\right|\le M
$$

ultimate-$\bm{\epsilon}$**\-approximate**

$$
\exists N\ge 0,\forall j,k\ge N,d\left({a}_{j},{a}_{k}\right)\le \mathit{\epsilon}
$$

Cauchy Sequence = Sequence + ultimate-$\bm{\epsilon}$**\-approximate**

$$
for\ {\left({a}_{n}\right)}_{n=0}^{\infty},\forall \mathit{\epsilon}>0,\exists N\ge 0,\forall j,k\ge N,d\left({a}_{j},{a}_{k}\right)\le \mathit{\epsilon}
$$

  Obviously, Cauchy Sequence is also a Bounded Sequence
Limit of Cauchy Sequence

$$
for\ {\left({a}_{n}\right)}_{n=0}^{\infty},\exists L\in \mathbb{R},L=\underset{n\to \infty}{\mathrm{LIM}}{a}_{n},\forall \mathit{\epsilon}>0,\exists N\ge 0,\forall n\ge N,d\left({a}_{n},A\right)\le \mathit{\epsilon}
$$

  LIM will be our placeholder to define **limit, **for now, $\mathit{\epsilon}\in \mathbb{Q}$
  And we can not define Limit of real number without firstly declaring it, which is limit of a real number sequence. In case of recurrent definition, a placeholder is needed.
Now our simple idea is to define Real Number as an analogy to Proportional one with all the axioms and operations we've been already testified

$$
x=\underset{n\to \infty}{\mathrm{LIM}}{a}_{n},\ \ y=\underset{n\to \infty}{\mathrm{LIM}}{b}_{n}
$$

(1) identity (equality) of Cauchy Sequence, follow substitutive

$$
{\left({a}_{n}\right)}_{n=1}^{\infty}={\left({b}_{n}\right)}_{n=1}^{\infty}\iff {\left({a}_{n}-{b}_{n}\right)}_{n=1}^{\infty}\ is\ Cauchy\ Sequence
$$

$$
for\ {\left({a}_{n}-{b}_{n}\right)}_{n=1}^{\infty},\forall \mathit{\epsilon}>0,\exists N\ge 0,\forall n\ge N,d\left({a}_{n},{b}_{n}\right)\le \mathit{\epsilon}
$$

$$
{\left({a}_{n}\right)}_{n=1}^{\infty}={\left({b}_{n}\right)}_{n=1}^{\infty}\iff \underset{n\to \infty}{\mathrm{LIM}}{a}_{n}=\underset{n\to \infty}{\mathrm{LIM}}{b}_{n}
$$

(2) addition, follow substitutive

$$
{\left({a}_{n}+{b}_{n}\right)}_{n=1}^{\infty}\ is\ Cauchy\ Sequence\iff x+y=\underset{n\to \infty}{\mathrm{LIM}}\left({a}_{n}+{b}_{n}\right)\in \mathbb{R}
$$

(3) multiplication, follow substitutive

$$
{\left({a}_{n}{b}_{n}\right)}_{n=1}^{\infty}\ is\ Cauchy\ Sequence\iff xy=\underset{n\to \infty}{\mathrm{LIM}}\left({a}_{n}{b}_{n}\right)\in \mathbb{R}
$$

(4) negative, follow substitutive

$$
-x=\underset{n\to \infty}{\mathrm{LIM}}\left(-{a}_{n}\right)\in \mathbb{R}
$$

(5) subtraction, follow substitutive

$$
{\left({a}_{n}-{b}_{n}\right)}_{n=1}^{\infty}\ is\ Cauchy\ Sequence\iff x-y=x+\left(-y\right)=\underset{n\to \infty}{\mathrm{LIM}}\left({a}_{n}-{b}_{n}\right)\in \mathbb{R}
$$

(5) inverse, follow substitutive
  Constraint away from 0

$$
x\ne 0\iff {\left({a}_{n}\right)}_{n=1}^{\infty}\ne {\left(0\right)}_{n=1}^{\infty}:\forall \mathit{\epsilon}\in \mathbb{Q},\mathit{\epsilon}>0,\forall \mathrm{n}\ge 1,\frac{\epsilon}{2}\le \left|{a}_{n}-0\right|<\mathit{\epsilon}
$$

  i.e. we remove any 0 element in sub sequence by setting their distances with $\epsilon /2$
  For detailed proof please refer to** "Tao Real Analysis" 5.3.14**

$$
{\left({a}_{n}^{-1}\right)}_{n=1}^{\infty}\ is\ Cauchy\ Sequence\iff {x}^{-1}=\underset{n\to \infty}{\mathrm{LIM}}\left({a}_{n}^{-1}\right)\in \mathbb{R}
$$

(6) division, follow substitutive

$$
{\left({a}_{n}{b}_{n}^{-1}\right)}_{n=1}^{\infty}\ is\ Cauchy\ Sequence\iff \frac{x}{y}=x{y}^{-1}=\underset{n\to \infty}{\mathrm{LIM}}\left({a}_{n}{b}_{n}^{-1}\right)\in \mathbb{R}
$$

(7) trichofomy, if and only one holds
  But first, we need to constraint sequence positive or negative away from 0
  We can always extract sub sequence constraint away from 0

$$
\forall x\in \mathbb{R}
$$

$$
x\left\{\begin{array}{c}=0,{\left({a}_{n}\right)}_{n=1}^{\infty}={\left(0\right)}_{n=1}^{\infty}\\ >0,\forall \mathrm{n}\ge 1,{a}_{n}\ge c\\ <0,\forall \mathrm{n}\ge 1,{a}_{n}\le -c\end{array}\right.,\exists c\in \mathbb{Q},c>0
$$

  Now we can inherent the rest of operations and properties from proportional number without changes
(8\*) **completeness**
  A complete closed set has its Cauchy sequence and limits inside the set
  e.g.
  positive real number set is an uncomplete open set

$$
\exists {\left({a}_{n}\right)}_{n=1}^{\infty},\underset{n\to \infty}{\mathrm{LIM}}{a}_{n},\forall \mathit{\epsilon}>0,{a}_{n}>0,{a}_{n}\in {\mathbb{R}}^{+},{a}_{n}<\mathit{\epsilon}\Rightarrow \underset{n\to \infty}{\mathrm{LIM}}{a}_{n}=0\notin {\mathbb{R}}^{+}
$$

  Non-Negative real number set is an complete closed set

$$
0\in {~\mathbb{R}}^{+}
$$

  Inference
     $\forall n\ge 1,{a}_{n}\ge {b}_{n}\Rightarrow {a}_{n}-{b}_{n}\ge 0,$ which belong to non-negative real number set

$$
\Rightarrow \underset{n\to \infty}{\mathrm{LIM}}\left({a}_{n}-{b}_{n}\right)\ge 0\Rightarrow \underset{n\to \infty}{\mathrm{LIM}}{a}_{n}\ge \underset{n\to \infty}{\mathrm{LIM}}{b}_{n}
$$

  While if $\forall n\ge 1,{a}_{n}>{b}_{n}\Rightarrow {a}_{n}-{b}_{n}>0,$ which belong to positive real number set

$$
\Rightarrow \underset{n\to \infty}{\mathrm{LIM}}\left({a}_{n}-{b}_{n}\right)\ may\ equal\ to\ 0
$$

$$
\mathrm{e}.\mathrm{g}.\ \ {a}_{n}=1+\frac{1}{n},{b}_{n}=1-\frac{1}{n}
$$

(9) order
  Real number can be bounded with proportional numbers(proof???)

$$
\forall x\in {\mathbb{R}}^{++},\exists q\in {\mathbb{Q}}^{++},\exists N\in {\mathbb{Z}}^{++}\Rightarrow q\le x\le N
$$

  Inference : archimedean property, order between real numbers

$$
\forall x,\mathit{\epsilon}\in {\mathbb{R}}^{++},\exists M\in {\mathbb{Z}}^{++}\Rightarrow M\mathit{\epsilon}>x
$$

  For now, we can confidently say that any type of number in axis can be bounded with arbitrary types of number.
  i.e. any number in the axis can be bounded by any type of number in axis, so they all can be ordered.
(10) supremum&infmum

$$
uniquely\ \exists M\in \mathbb{R},M=\mathrm{sup}\left(E\right),E\subseteq \mathbb{R},if
$$

  (1) $\forall x\in E,x\le M$
  (2) $\forall {M}^{\prime}:x\le {M}^{\prime},\ M\le {M}^{\prime}$
  For proof please refer to **"Tao. Real Analysis 5.5.9" **base on archimedean property
  Now we can prove that only real number than proportional number can be solution of

$$
{x}^{2}=2\Rightarrow x\in \mathbb{R}
$$

$$
E=\left\{y\in R:y\ge 0\ and\ {y}^{2}<2\right\}\ne \varnothing 
$$

$$
\forall y\in E,y<2\Rightarrow \exists x=\mathrm{sup}\left(E\right),x\le 2
$$

  Assume ${x}^{2}<2$*, *$0<\epsilon <1$

$$
{\left(x+\epsilon \right)}^{2}={x}^{2}+2\epsilon x+{\epsilon}^{2}\le {x}^{2}+5\epsilon <2,for\ some\ \epsilon 
$$

$$
\Rightarrow {\left(x+\epsilon \right)}^{2}<2\Rightarrow x+\mathit{\epsilon}\in E,\ while\ x+\mathit{\epsilon}>x=\mathrm{sup}\left(E\right),\ contradict
$$

  Assume ${x}^{2}>2$*, *$0<\epsilon <1$

$$
{\left(x-\epsilon \right)}^{2}={x}^{2}-2\epsilon x+{\epsilon}^{2}\ge {x}^{2}-4\epsilon >2,for\ some\ \epsilon 
$$

$$
\Rightarrow {\left(x-\epsilon \right)}^{2}>2\Rightarrow x-\mathit{\epsilon}\notin E\Rightarrow x-\mathit{\epsilon}>x,\ contradict
$$

  Finally, according to the trichofomy, ${x}^{2}=2,x\in \mathbb{R}$
  Generalization

$$
n\in {\mathbb{Z}}^{++}
$$

$$
{y}^{n}=x\Rightarrow {x}^{\frac{1}{n}}=\mathrm{sup}\left(E\right),E=\left\{y\in R:y\ge 0\ and\ {y}^{n}<x\right\}
$$

  Further

$$
q\in \mathbb{Q},m\in \mathbb{Z}
$$

$$
{y}^{n}={x}^{m}\Rightarrow {x}^{q}={x}^{\frac{m}{n}}=\mathrm{sup}\left(E\right),E=\left\{y\in R:y\ge 0\ and\ {y}^{n}<{x}^{m}\right\}
$$

(11) base on definition of **supremum&infmum**, now we can define **limit **of real number sequence
  Cauchy Sequence on real number

$$
{a}_{n},\mathit{\epsilon}\in \mathbb{R}
$$

$$
for\ {\left({a}_{n}\right)}_{n=m}^{\infty},\forall \mathit{\epsilon}>0,\exists N\ge m,\forall j,k\ge N,d\left({a}_{j},{a}_{k}\right)\le \mathit{\epsilon}
$$

  Since any real number is bounded by proportional numbers, so it is compatible with Cauchy Sequence on proportional number
  The equality between real limit and symbolic limit, if ${a}_{n=m}^{\infty}$ is a Cauchy Sequence

$$
\exists L\in \mathbb{R},L=\underset{n\to \infty}{\mathrm{lim}}{a}_{n}=\underset{n\to \infty}{\mathrm{LIM}}{a}_{n}
$$

$$
L=\underset{n\to \infty}{\mathrm{lim}}{a}_{n}:\forall \mathit{\epsilon}>0,\exists N\in \mathbb{N},\forall n>N,\left|{a}_{n}-L\right|<\mathit{\epsilon}
$$

  Proof: assume that

$$
\underset{n\to \infty}{\mathrm{lim}}{a}_{n}\ne L\ when\ \underset{n\to \infty}{\mathrm{LIM}}{a}_{n}=L
$$

$$
{a}_{n=m}^{\infty}\ \mathrm{is}\ \mathrm{a}\ \mathrm{Cauchy}\ \mathrm{Sequence}:\ \exists {N}^{\prime}\in \mathbb{N},\forall n,m>{N}^{\prime}\Rightarrow \left|{a}_{n}-{a}_{m}\right|<\frac{\mathit{\epsilon}}{2}
$$

$$
\underset{n\to \infty}{\mathrm{lim}}{a}_{n}\ne L:\ \exists {N}^{\prime}\in \mathbb{N},\exists N>{N}^{\prime}\Rightarrow \left|{a}_{N}-L\right|\ge \mathit{\epsilon}
$$

  Use both inequalities, we can induce relationship between ${a}_{n}$ and $L$

$$
\left|{a}_{N}-L\right|=\left|{a}_{N}-{a}_{n}+{a}_{n}-L\right|\le \left|{a}_{N}-{a}_{n}\right|+\left|{a}_{n}-L\right|,n\ge N
$$

$$
\Rightarrow \left|{a}_{n}-L\right|\ge \left|{a}_{N}-L\right|-\left|{a}_{N}-{a}_{n}\right|\ge \frac{\mathit{\epsilon}}{2}
$$

According to

$$
x\in \mathbb{R},{a}_{n}\ge x\Rightarrow \underset{n\to \infty}{\mathrm{LIM}}{a}_{n}\ge x
$$

$$
\Rightarrow {a}_{n}\ge L+\frac{\mathit{\epsilon}}{2}\Rightarrow \underset{n\to \infty}{\mathrm{LIM}}{a}_{n}\ge L+\frac{\mathit{\epsilon}}{2}\Rightarrow L\ge L+\frac{\mathit{\epsilon}}{2},\ contradict
$$

$$
\Rightarrow \underset{n\to \infty}{\mathrm{lim}}{a}_{n}=\underset{n\to \infty}{\mathrm{LIM}}{a}_{n}=L
$$

Now any property of proportional number is compatible with real number, so any proportional number is a real number, we complete the construction of real number(added with limit operation)
