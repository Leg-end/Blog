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
![image1](resources/02030eb153de4a088e0d76ac30abafd5.png)
If basis is function, then the vector in space represents a function, since it's a combination of basis functions, e.g. polynomial function, triangle function  
**An informal connection between real number space and function space: discrete to continuous**  
![image2](resources/efffdc8a6e7e49468bbea59f6e7e130c.png)
![image3](resources/325c7e16d1b748a5aa9b42b2d2a12807.png)
That brings summation of its inner product
![image4](resources/7d8f944735cb42d4a72ed23f505cc293.png)
So the continuous function is generally what we so called function vector
![image5](resources/1f426e18be6e4f3a9afceb74ec180cbf.png)
That brings integration of its inner product
![image6](resources/3e58652e03f64f84bfd9e5263393e86c.png)
![image7](resources/cbd0bfd55be94ddebb78daeff4163004.png)

![image8](resources/45c67502756e403680cb358f9bf21c3a.png)
The most important one is inner product, it's the building block of metric and orthogonality
In the process of generalization, the consistent rules a property(operation) should follow weight more than the exact form of property(operation)

**Relationship between inner product and orthogonality**  
Definition of perpendicular:
![image9](resources/45af9abb2b0d4bf08076feea6d215bae.png)
![image10](resources/156dceebdcfd4c12947ff543d4fe6637.png)

The second one is orthogonal basis vectors, which is the fundamental bricks building any vector in the vector space. All can be derived from a simple equation
![image11](resources/6780bbfd9f3a4fd6aa2b8c93c3dda172.png)
Cauchy-Schwarz Inequality
![image12](resources/fca0e0977d3e4408a7e03c7d6f696115.png)
![image13](resources/94014f4c95df49b58086f1b588a4fb1c.png)
General form: Holder Inequality (with weighted norm)
![image14](resources/7a196dbb5f064c658cd467b532c7eb8a.png)
*Weighted inner product \<= weighted norm \* weighted norm*

**Definition of Inner Product Space**  
Any vector in a vector space follows the rule of inner product
Inner Product Space = vector space + inner product applied

**What is Norm**  
![image15](resources/b56f59d3f8d44e65ac4961f7bd6dcbd6.png)

we can see that definition of norm always involve sup, such a norm defines a constraint on a set
e.g. for a vector, its norm defines its length, we can turn it into a sup-form (rough)
![image16](resources/ca52b540fe2d47fe85ecf516bc929df9.png)
if we treat x as a set of point forming the x line, then the sup achieved exactly at x

from the unit ball case, we can also find that the definition is searching the max ratio number t from origin to C's edge, e.g.
if C is a ellipisoid, then t must define on the longest line from C's edge to origin, then this sup gives a bound for the set

and the following cases with sup definition, all define a constriant or bound for set that all element in the set satisfy, or in a more abstract way, we can say:

norm define a constraint(constantly, \<=) on a set so that this set can be a convex set w.r.t the constraint, i.e. all elements in conv(set) are satisfied. and this constraint follows as least three basic properties.

**Distinguishment between close set and fully bounded set**  
![image17](resources/dcd255ab74a1412d916a6fec1dfb9321.png)

**Equivalence between quadratic norm and weighted inner product**  
![image18](resources/aa3470387c7044dfafa5fbb5fadcad6b.png)
![image19](resources/00162005cbc744cba0fac3cfa783f82d.png)
![image20](resources/60b0c4baa6194012a85658df4b1de75d.png)
![image21](resources/8a673558b6b246ae94b65b237fc551be.png)
![image22](resources/b95560affd314be1bc012f34bc788bd9.png)
![image23](resources/a3f2efc6a6c4446b9650291194a3650d.png)
![image24](resources/69c789a61b2144ccaaaec3fb464bedad.png)

**Norm of matrix**  
A matrix represents relationship between two vector spaces, or a mapping from one vector space to another, so it would make more sense when defining its norm with objects it is operating on, that's exactly the operator norm where matrix is taken as a operator: operator norm
![image25](resources/7b68661ebd7d4613a16e893aacfd23c1.png)
It simply tells the maximum transformation that a matrix can apply on the element from b-norm ball. That can attach to the behavior of an operator
There is another norm for matrix called kernel norm which is the summation of all non-zero singular values
![image26](resources/b4fe21bbfe1b43af82aa8dc92b914aa9.png)
Such definition strongly tells the sparsity of structure(magnitude and direction of axis) of basis space that forms the matrix

**Analog from real number to matrix**  
Lots definition of matrix can be seen as an extent version of its counterpart in real number system, e.g.
Positive defined matrix to positive real number(that can also give inspiration for definition of general inequality)

Gradient w.r.t matrix has similar rules as gradient for real variable

Hessian matrix describes similar property for the **curvature** of specific point as second order derivative did, instead the former is in multi-dimension case where the **curvature** extents to a super ball or super ellipse that has its border plane **perpendicular** to gradient.
So a Hessian matrix has its curvature approximates to a ball tells that we can pick any gradient as the optimization direction since they are all good enough, a elliptic case will be a bit of thorny since different gradients are diverse in magnitudes where a good enough gradient can be hard to choose.
Such a property can be defined by **conditional number** of Hessian matrix, which carves the gap between largest singular value and the smallest one. A ball case, obviously, will have same singular value in all direction

**Equivalence of norms**  
![image27](resources/f559c45717274bdcb4611354b5f3a3de.png)
They define the same set of open sets, i.e. in the form of [metric space](https://byjus.com/maths/metric-spaces/)(set + metric, e.g. norm space)
![image28](resources/0122da8db77f4791b3f6b66ab0ff9f50.png)
![image29](resources/e6726b6b38c14edd856f50a3a4343eb1.png)
![image30](resources/3f7ba296e9d34fb1b21e3fd56e48352c.png)
e.g. Imagine that we can always find a pair of stretching coefficients for L1 norm to enclose L2 norm, so as L2 norm
Since their open set includes each other, so they define same set of open sets.
![image31](resources/f8dac9c475704b73817f5ac5d33e9ba2.png)
Equivalent norms(metric spaces) induce same topology(set of open sets)
![image32](resources/fec1dcd567cb4c40832b3d72d03f03e5.png)
1.  ![image33](resources/286f6dcb548f4f0ea5c29929a837a210.png)
2.  ![image34](resources/0f3ee2d08328455897baeee521755e5b.png)
3.  ![image35](resources/2aea3fe71689495793fc65827d6a26ca.png)
![image36](resources/46941a36f25c483d9f7063342179c4ee.png)
![image37](resources/a1cd15e83ee4407da431600316408c1b.png)

**Definition of Banach Space**  
Complete norm vector space or complete metric space
![image38](resources/6cc2f02b72314658b42d0b716fa27bd4.png)
Norm, a function, applied on vector space has its Cauchy sequence limit still in the same space
[Example of non-complete norm](https://math.stackexchange.com/questions/1948207/example-of-a-non-complete-normed-vector-space)
![image39](resources/ea9c38c90225494a8a979806a3a3b978.png)
![image40](resources/353b8395387a49ccbbf0d097285f30ca.png)
![image41](resources/4942f8c4d9754baba8797b6ca8dac604.png)

**General Clue**  
**Optimization target: Mathematical optimization problem**  
![image42](resources/fc8177a4b8694f1b9945bdb4cc8d7735.png)
![image43](resources/c568c23a7c864b9db315d4d0a57c0919.png)

![image44](resources/4b9de22737a44ae4be07b41b9dcfd5be.png)
![image45](resources/8474a6ed282146738275bd9fdc36f6b2.png)

![image46](resources/13c0a53b2ecf497db62e8f1dab77c63a.png)

![image47](resources/dc4cf8b5025d4b11baa1b151afe29a44.png)

![image48](resources/d40856526e494184ba650046c600714d.png)

![image49](resources/3915cf003ebb4f12846b6a6d0ec884df.png)

![image50](resources/2ec3b9de94164bd8af4b745e68788a76.png)

![image51](resources/deca64b59dfd447faa0cc75309bd75e4.png)
![image52](resources/4fec9ee5fb0c4cfabbbc910fe9cdf182.png)

![image53](resources/2b70bd52cdb2400cbafb30cf8180c146.png)

Application [SVM](onenote:#SVM&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={11A9696D-1BFF-4700-8B1D-CF78A9E2CCFA}&end&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one)

![image54](resources/3bfff081f4b843198d0d3c4046de8828.png)

![image55](resources/a1cb29b284c84590a95b90ce6327d934.png)

![image56](resources/cdf79625b6674e5da10e39794794ce82.png)

![image57](resources/a55abe4f0ab84805a53524a20039e357.png)

![image58](resources/779470c2f2aa4ca3841d7af0a530ef9c.png)

![image59](resources/7429f554dc9b4121bb0f3a5037c11766.png)

![image60](resources/f55e75dc291b42b6a3f865207daefeec.png)

![image61](resources/f74ab0674aa34285805e8f3ef6647b81.png)

![image62](resources/8a7271fa6f4c4336a388d0fa8df85b3f.png)

![image63](resources/05564e5459034cd8b5436d36aae1b4a4.png)

![image64](resources/f663ceffa0494087b2d709e24b3cdd59.png)

![image65](resources/dd931b2f081b41b6a82e6e7c6521200c.png)

![image66](resources/d191e07f799c4818aceb7b9935ad7d2d.png)

![image67](resources/39e0a10c12cf4dbf841998160715450e.png)

Properties to mark out function's convexity
![image68](resources/0b30a5e6976648679ad3d4a67620608c.png)

![image69](resources/4f791eec2ba8481dafd72bd5e0bbe6c5.png)

Relationship between convex set and function

![image70](resources/70977866a04b41448c8dfd11a15f0918.png)

Gradient conditions

![image71](resources/c220027e217c4716866bf814fd543837.png)

![image72](resources/ce42566efcb0449eaa45a568195fe504.png)

![image73](resources/f9a213acdcea4f5c8f4964e57bf1c7e1.png)

![image74](resources/05c64161b36043f6bebc70cf1100e5b4.png)

Operation that gain convexity
![image75](resources/76eb0d1fff634f90a09c681543d36c3a.png)

![image76](resources/54470deaa08c4d73b60572a0671ab40a.png)

![image77](resources/58aab7f66d274b47adfd12537dfc4255.png)

![image78](resources/82fded0587434fb68ed6d087be86da43.png)

Operation that preserve convexity
![image79](resources/55bed2e4e69b49f9b427d9d9403cd7e1.png)

Affine function;

![image80](resources/43b3cac93c504b2b8a284f771ea597c8.png)

![image81](resources/3d8dd77cee44411fb0694062b70d4eb7.png)

[Conjugate](https://math.stackexchange.com/questions/2700835/understanding-the-conjugate-of-a-function)

![image82](resources/29be0a43ba0f48f9b0f13bda0529767d.png)

Note: Using these ops as unit to construct powerful function that can approximate lots intractable functions, e.g. neural network is the repetition of Affine function +nonlinear activation

Brick to build optimization target
Norm is a generalization of physical length, it's a function that

![image83](resources/8946e784f1954478834989deb8323839.png)

Lots definition involving norm contains "**sup**", so it can be informally treated as a bound that an operation can obtain, in other words, all consequence of the operation are bounded inside this norm.

Generalized inequalities
Think in a programming way that comparison between instance of custom class requires partial order definition, so we can compare them as we did with real numbers. Generalized inequality is a bit taste of it.
![image84](resources/69570692146f49f0b2583c968c1fca7c.png)
By introducing generalized inequality, we define the behavior of optimization, since optimization problem is equivalent to finding a partial ordering sequence base on specific rule of inequality.
![image85](resources/05e5b73995984cc3a24a31456ee95afb.png)
![image86](resources/c134fd48a2e749b6b294fefe7f1d2d21.png)

![image87](resources/9f20a21017884a12b404a961848b2948.png)

![image88](resources/9cda128fbae742bf8ba077cc85612d68.png)

![image89](resources/9dbdec7f65494aaf8a9e6200508447d6.png)

![image90](resources/38f9675959074234ad9c6dde2dc20b57.png)

![image91](resources/646bc79c3944434cb955a025876391e4.png)

![image92](resources/cf1a27ede141471db870b6be22b7018f.png)

![image93](resources/11aab0d9499e4718adcd4ad8ba3e741c.png)
![image94](resources/600891afa5a34ec9a7d5680d6928cd2b.png)
![image95](resources/8a33279da488487abb3d5fa7b3eaf9a2.png)

\[1\]: with smaller cone, the more hyperplane can enclose this cone

\[2\]: if K has empty interior

![image96](resources/4bf02bb5dfa14102bae14a59ac837704.png)

![image97](resources/c7ddddd8ae11479bb3a0c9b5125832ec.png)

![image98](resources/29da665907f64e8c902765f4076ec9cb.png)

![image99](resources/b54c05438e984a028c863bbbbcddb77d.png)

![image100](resources/62e52202727246e0a67d178ab3ed05e5.png)

![image101](resources/6138b7180e4b4313b9f53f2415f2d2c9.png)

![image102](resources/d13107e6ce6341e5b21dfed98324a472.png)

![image103](resources/da3f36b3a3db471990f128ee7c55835b.png)

Note :if K is closed convex(proper cone), then dual cone on dual cone return to original cone

![image104](resources/21577b71664f4d43b463de539b20e8a5.png)
![image105](resources/667790adb95c4be89aed958378aa02f1.png)

![image106](resources/a74490e2941c4349b56e47e374e0083c.png)

![image107](resources/1d2d1d6af8994505ad9f467fc2547a87.png)

![image108](resources/c436680e895843e59d28369f45d4a00d.png)

![image109](resources/45f2531390664ae69d7673a95dafbe65.png)

![image110](resources/4b07ff5af8884c5db6cd737e79cd0d27.png)

![image111](resources/933dfb4c89934e80adbf3ea243aa0b55.png)

![image112](resources/bcb222e4d3c4466a91bb71782ca13868.png)

![image113](resources/2ca538744d464fa8b5b268495f3d4ffe.png)

![image114](resources/fa0894c9941c452781fd69c6333cff76.png)

![image115](resources/0f9226bcc6854ca5a9eedf6de060c8e5.png)

Proof:

![image116](resources/c16afc4cf18f4a11b3a075b22a2c23a8.png)

![image117](resources/418742998f5f45b391ba50851b666f39.png)

![image118](resources/6aab293ea6dd49a7b6d92446fcb693b8.png)

![image119](resources/984d31a23c7a49d09d063d1487652e4a.png)

![image120](resources/0b3d403eef9a41fe8ed434a32ecc98d2.png)

![image121](resources/06e2bf64fb684dbba7b7012536aa9c92.png)

![image122](resources/55f8bdd69edc4c06a5da0630d4c76b3e.png)

![image123](resources/cc6bc2fa2d034e269e79d473a5c0f039.png)

![image124](resources/13c2c11be1cd4166802dd2b26e4803c6.png)

![image125](resources/6cfb776849c94b32a5fe370c9b5a8aa5.png)

![image126](resources/93b2256b639641d8b02e62fad32861bb.png)

**The importance of convexity in optimization**  
Convexity means global optimal and convergence to it, since a convex function satisfies
![image127](resources/02f9c3d0d3f4421183dc9145816b9f66.png)
![image128](resources/958288b53835498599ba38ff4e352939.png)
![image129](resources/a1c54f48db86460b88a8e12ce3f7f94c.png)
![image130](resources/db530aa46370470693873fa161e1dcb7.png)

The optimization of a target function maybe hard to achieve, e.g. there may lack of analytical solution, like objective in Variational Inference
![image131](resources/92bba4169b2f4c3eb70bd3f4667e4320.png)
Instead, the optimization can be equivalently be done by a lower bound of the target objective, given they are convex functions.
![image132](resources/46b3750f7ab44e309e0309aa71ede283.png)
![image133](resources/c558f5c7b242481e8d79a42dff6684c2.png)
Why ?
Imagine that in convex case, both lower bound and its supreme are convex, so a point in lower bound has lower value, so is it in supreme.

But in non-convex case, the same point may has higher value in supreme, since supreme is not convex function, so there may be lots peaks in it

**Lagrange Multiplier & KKT: Chapter 5.4**  

![image134](resources/d4077934d0bb4b4296d426f090505f41.png)
![image135](resources/d8ce5e1ebf774196bf36d727e9d27634.png)
![image136](resources/0f8ddc17b25b4c88985e8eee0d6d02c3.png)
![image137](resources/18984794bf3d418e9c114b0b61564742.png)
We map a minimization problem in original space into its bounded problem, in here bounding it above, in dual space, which is a convex function with respect to original space and can be solved easier if provided with appropriate Lagrange multipliers.
In general
1.  Find assistant function that below target function over its domain
2.  Maximize assistant function so that it bounds target function tightest by adjusting Lagrange multipliers
![image138](resources/f2990c6d43474c25a7df580beb5cc052.png)
![image139](resources/d2ed5cc4ab20414f90f4444d3bf04225.png)
![image140](resources/1303aae954be4eb4951ddc26762ed5e0.png)
since we are trying to find its maximum that bounds target function tightest, i.e.
![image141](resources/dff411ef8b7e4ce9990059d6c34bab7d.png)
Informal explanation for the sign of Lagrange multiplier is that for a minimization function, its Lagrange function always bound it above, Lagrange multipliers must be chosen so that:
![image142](resources/8409dccf24af46c3b1fb627105c7db87.png)
Which implies the sign of Lagrange multiplier
![image143](resources/79a28e048f0844309196655f32eca0eb.png)

But a deeper inspection can relate to gradients
The core question is when do we reach optimal ? That is when we cannot find a feasible direction that can reach to smaller or bigger function value.
For constraint-free problem, optimal reaches when gradient is 0.
![image144](resources/f14ac3249ac84b3eae11391c33384258.png)
![image145](resources/9eddd5bc612541f1884f86694abd19ac.png)
![image146](resources/264f8e3ca8be4b72972a688e3e9071c6.png)
![image147](resources/b398dd45d762436fa0d802a7fc452118.png)
![image148](resources/10b05aad414a4f5f99a07827fa4c0eea.png)

![image149](resources/c94692aed4394845bf5b11b705f511a5.png)
![image150](resources/97fac17778284bceb2d255a75ffad4e2.png)
![image151](resources/f1a332d9a34a43bf851e10592d63476c.png)
And a feasible direction satisfies(for minimization)
![image152](resources/4566ede7c10042dca05c0a852ec1d9db.png)
![image153](resources/bc73d9d1c59742aab0ec4f6e2b7ffa44.png)
![image154](resources/fc0e954f294448a69d56ab092795688f.png)

Or equivalently

![image155](resources/47e3129e5d7840418ce63ed29da22429.png)
Tangent cone defines on geometric properties, which is unanalytical, we use its linear approximation as replacement
![image156](resources/de213c507bf34e00b7b8e94de2a9bbda.png)

![image157](resources/18b9357e20af4ba6a9b89c973eca9d40.png)
![image158](resources/2fb9208f88b141bcbf1eff338b727726.png)
![image159](resources/295cd32a01b248249a62d76dce0c24c0.png)
![image160](resources/789d3d9eaba84f01a16179397534e3ca.png)

For equalities constraint, available field is made of points satisfy
![image161](resources/6454e4e55dce4c6aa9897ac615d3f0eb.png)
![image162](resources/8ca067a1aa41491998174ef1ca01bbbb.png)
Which means all tangent vectors in tangent cone also perpendicular to gradients
![image163](resources/73d33d19444c4a488df99ceebfdd2400.png)
And optimization along such direction won't violate the equalities constraint, i.e.
![image164](resources/e88a7adbcf954902a218d69b23f6c7f4.png)

Proof:

![image165](resources/df8a07b22a724254b47e44f137aa3eef.png)

For inequalities constraint, available field is made of points satisfy
![image166](resources/2f9acd1895214afa8693821a78ae485c.png)
Which is solid region with equalities as edge, so we need to analyze points at border and internal respectively
Tangent cone of points at border were bounded by their tangents along the surface, which is perpendicular to gradients, so angles between any tangent vectors and gradients are greater or equal to 90, since a feasible direction must stay in constraint region.
![image167](resources/fce25e1f367243f1a5c83abdaf26409a.png)
And optimization along such direction won't violate the inequalities constraint, i.e.
![image168](resources/709740002ac94dcb980835358c147ff7.png)

Proof:

![image169](resources/9e39a68c0ac54726ab5865f40c43039b.png)
Now we apply the same scheme to internal points
![image170](resources/b84210dcc51a4b4db12fd3cbe93daff3.png)
Actually, such point has its feasible direction any vector in real space, since we are in internal available field, an appropriate movement will still stay in available field. And we can always find a feasible direction that can lead us to better function value.
![image171](resources/2aeb4b405a3d45f39b8439514ca7095a.png)

![image172](resources/8a12c996eccb4e4691b33fdda4a81a05.png)

Proof:

![image173](resources/5379e5d2a3964f7ba545326d75b57ad6.png)
We find out that a feasible direction for target function requires
![image174](resources/431a0bf43feb4baea9955b3208b531e9.png)
And allowed directions provided by available field are
![image175](resources/136a589541ca4f0ba727f21e612c9f18.png)
![image176](resources/081b880e5aad4083aefe2ee20d6943a9.png)
![image177](resources/fdd787ad7e0b4b04bdfe39c00495a1bd.png)
![image178](resources/de3346a8d1aa4de39c232321992a6e8c.png)
![image179](resources/2553f4da32fd4d5bbe7dee15bafc7fb5.png)
Equivalently, it can transform to
![image180](resources/9095e346bcf745a296be87325e4cc499.png)
Yielding two infinitesimal half spaces
![image181](resources/3e39dbdfb05b49a49e235f4dfe06d969.png)

![image182](resources/223ebf060ec940f89116deb4dfe810a4.png)

![image183](resources/97fe43bcd27c4339a43f4cec084e987e.png)
According to strict hyperplane separating theorem
![image184](resources/4873e251200a4469b25d8c35b9b902dc.png)
So optimal reaches only when the two half spaces share parallel norms
![image185](resources/82e3cfd2a74e4e0e80480b0810f4926b.png)
That's exactly the extended form of solving optimal with constraint in 1-d case
![image186](resources/6fd03e8977ac44ab99706bfc3709b538.png)
![image187](resources/144f56c7571043f9a6612d74e107ec3b.png)

![image188](resources/20e8628cf0c64911aa2dd19574f17dcc.png)

![image189](resources/4c3ce2fb3bdd41448e946c7bb55b5a8d.png)

![image190](resources/b73ce33a87b34d46acbf5cfe57a854aa.png)
![image191](resources/66ea90295ea44fb7be760225051119a0.png)
![image192](resources/3fb129c117004eb7a78d0f945f04191f.png)
So in conclusion, a stationary points reaches when
![image193](resources/97b39cf2d0a94f35922e353a050a6b4b.png)
![image194](resources/d89df923888a41419ad8798f10c35edf.png)
![image195](resources/57512ff8be744c59b72fb62cc0edc183.png)

![image196](resources/fd758c50fd584de68bfae810440f3307.png)

![image197](resources/84dbf622e09c4d81ac6164c9c8171f9e.png)

![image198](resources/94c0c2ef298b4421938abb5df23e0f9f.png)
Note that the KKT conditions only states that no existence of descent direction, but not equivalent to solution of local optimal  

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
![image346](resources/51eb8bd18b90487396b15e2258b0507a.png)
![image347](resources/9212e219bbb3488ab9a78bdf452fb6f1.png)
Now if we extent it to elements of unknown vector space
![image348](resources/ff16cc74ebc546ef8a2e946b18eeb12f.png)
Base on generalized inequalities, we can define partial order relationship, e.g.
How can we compare between matrixes ?
Follow the frame provided from Generalized inequalities, we need to find a cone of matrix to satisfy the inequality
![image349](resources/350d3bf3454b40db93a5e8ed03aba47a.png)
![image350](resources/577bac86b7d54509a25ce99fbbcc82df.png)

Generalized inequalities is a fundamental and essential definition for defining good optimization problem, since the essence of best solution is that it is bigger or smaller than other solution in some measurable space, which means a partial must exist between these solutions, that in turn depends on the definition of generalized inequalities

Operation that preserve convexity
Max function
![image351](resources/13e757fa9b1646428d58cd73ec494e08.png)

Application for max function can be related to alternating optimization problem, e.g. EM algorithm

We fix one component of parameters, then optimize the other, and then switch them while doing same process.
Conjugate
![image352](resources/34c27a7407724e7b9aaeb21c5cbe36a1.png)

![image353](resources/00cd3583fb2b4a1bba573eb852798d9e.png)

![image354](resources/20d2ab712be5420ebf6e82227a4ee4b2.png)

The most familiar application is regularization for cost function.

**Gradient-descent-based methods**  

![image355](resources/7c8d931996224735be97a8c010239e6f.png)
![image356](resources/864db81cd33648ee9c767574ec246743.png)
![image357](resources/92dd6f6c804c4594af381e38d2f1f19e.png)
1.  ![image358](resources/bbeafbe58a8c40b3ae306206236f76ca.png)
2.  Search step size according to some principle
3.  Accept or reject updated state according to belief field
![image359](resources/fa2e13779d7646989e6abba84243f26a.png)

![image360](resources/73e2854f332f46e88d21f0abede8be87.png)

![image361](resources/e856fab2d65f47799904c2dc14da18f5.png)

![image362](resources/8c200bf21dae4058a98b63ab1ff5ca92.png)

![image363](resources/507bc245fd2f4398bf795532ba6837a9.png)

![image364](resources/754ba2914c5147de816a577443020c88.png)

Classical gradient descent
Large magnitude gap in different directions of gradient =\> "Z" descent trajectory(with optimal step size)

Proof:

![image365](resources/8eb47c1453344ad19cd9029200bfa303.png)

Assume the step size is optimal

![image366](resources/d2d1589d917d44ac9a4c86d419a8f312.png)

So gradients from current step and next step are perpendicular, results in "Z" descent trajectory

Newton method
Rectify the magnitude of gradients by using second order information

Using taylor expansion (to 2-ord) to get new function has gradient = 0

![image367](resources/78d5f13c4d564ae5b3c4900f91a4aee4.png)

![image368](resources/3fca544a0d434bb8b89d8cba5a5f43f8.png)

![image369](resources/141bdd728dcc40088b0e8acde79c70e9.png)

![image370](resources/fbfbdaabd1344ba6aeeaf35f34c79c55.png)

![image371](resources/da6ccdaa86a6453c86df2e947b1b26e9.png)

![image372](resources/83f14bb3a7734cd3b9588029ed4742cd.png)

Simulated-Newton method
![image373](resources/d2de6d29bfda485f8125d76096bb7478.png)

![image374](resources/04386281b03640af8b253bebc0fb7ca5.png)

![image375](resources/16b03479625147a3a439db4dc0217fd3.png)

![image376](resources/4cdb966b20cc4147867fbd49cc146cab.png)

![image377](resources/bf0a977a6d854e8ab963b7b50682ca07.png)

![image378](resources/2b7383af4eaa4489b61e2bdcbfbae009.png)

![image379](resources/e7456153be154a7d88c42872d8d7b433.png)

Cannot guarantee positive definite

![image380](resources/1f6d4e8fe9424163a5126b78598af8dd.png)

Sub gradient
![image381](resources/6ca758a9d24b4ed9abcaa42b92e29bce.png)

Any gradient in sub-gradients may not be the descent direction

![image382](resources/1fc5d014e04c498e994e11c9a9b211f1.png)

![image383](resources/ed3fd335f62b4ecf8e83c08bba486ffd.png)

Search of step size
Assistant function

![image384](resources/9bd46fa7fc964d03aee7660cb3090a27.png)

![image385](resources/3bc541af18074eeeb7c24092b0092fd2.png)

![image386](resources/456f8ba1ae5442eeb9a8205f1a778c0e.png)

Brute-force

![image387](resources/38fae08fed124e869cbea629e512426e.png)

Armijo principle:

![image388](resources/57f80cf9c7134052bf35b811a0e665cd.png)

![image389](resources/9ef3a0ad03a7421ca43893ca2be6026b.png)

![image390](resources/6ba07b54747b4f018cb03347b54a8175.png)

![image391](resources/37f7ae0675b74ceaadfc36d283cf51d0.png)
1.  Require descent each step motonomically, or
2.  Require descent after M steps, to jump out of local optimal
![image392](resources/88e748b7d37349438d017ce5355e77ea.png)

Goldstein principle

![image393](resources/76d0e8cec4ca4e8daabd881b4c56378f.png)

![image394](resources/54dc0ab957f24401b2690704089d4152.png)

![image395](resources/e9f04faba8e04d4b9ab981374442edf3.png)

May result missing local optima

Wolfe principle

![image396](resources/e5f2591b75ab434b9b2888b85669f05f.png)

![image397](resources/b8cc8bb84025455486d4e291a6c9c1d1.png)

![image398](resources/4764a13762c740cea447a4f42f95da7b.png)

Convergence premise
Gradient satisfies Lipsic continuous

![image399](resources/cbf739b21dc64562beadeed0b18b1e7a.png)

![image400](resources/a555ef5b70fb4cc88ea5bb1757ce20d1.png)

![image401](resources/20d33ef0ec0b43aeb5785eaa3e3c4075.png)

![image402](resources/f6b0f292edad48b6a12e215adcafe3b6.png)

Approximate
Low frequent information -\> high frequent information (by high-ord derivative)

Vicinity gradient for solving non-smooth part, e.g. regularization part
Vicinity operator
![image403](resources/224129ed2b3c4d7eb39ae3e95923de22.png)

![image404](resources/25dce945e3324fe5ae93181eade83324.png)

![image405](resources/cfe6a2cf7c22413db4dcf3cfc4d63751.png)

![image406](resources/f9cb5866e8fc47c9936de2d1109ba656.png)

Approximate gradient

![image407](resources/3bc92949922b4040b93c3b493731300d.png)

![image408](resources/66a8ad498e0f486590ff173ce7021e2f.png)
1.  Gradient descent on smooth part
2.  Vicinity operator on non-smooth part after updating smooth part

Composed optimization
Split descent and constraint
1.  Do descent without constraint
2.  Project back into constrint space (by updating parameters in control of constrint)

Augmented Lagrange
![image409](resources/301062e94c2c467898d4625fca5fb536.png)

For optimal

![image410](resources/fd5874e6c7154e8ab13041270339ca9c.png)

Should be consistent with Lagrange solution, for large k

![image411](resources/5e882666efd14722914fb8cf82e29bf8.png)

![image412](resources/9784a76cb6474112a95ecb5b4b4cdf51.png)

![image413](resources/e94059fbce8e4e62b47841ae7fa79993.png)

ADMM
![image414](resources/2c2ac4b9d70e40f798af37c9eb9cd973.png)

Non constraint to constraint

![image415](resources/738a57c2267b4415a4017d8e4513613b.png)

Lagrange to augmented Lagrange with panty function

![image416](resources/f1f94999e76c4e2d973925d6c57651a5.png)

Update target arguments and Lagrange multipliers

![image417](resources/0c771c79840b4062b46f0f52440b6a81.png)

![image418](resources/1177195309c94603add647ee802ac27d.png)

Update alternatively

![image419](resources/a43fbf4e55084a279dc80809d3cc0c92.png)

![image420](resources/3fbc80f510874460b9f489e60a1f65bf.png)

![image418](resources/1177195309c94603add647ee802ac27d.png)

