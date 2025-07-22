---
title: Preliminary
published: 2023-06-26
description: "Something you should know before starting."
tags: ["Preliminary"]
category: Guides
draft: false
---

**Reflection-Ask more, Simbolic description, be more patient, be more fun**
1.  What is exactly we trying to solve and the ideal result ? or What is it look like, before solution and after solution ?
2.  How does the solution do to solve it ? (the general process, not the parsed detail)
3.  How does the solution come out ? (peel it out the simple core idea)
4.  How does the idea behind adapt on this problem ? Are there any generalized way ?
It's indeed hard to remember all the complex detail of the solution, also it's boring to do so, so why not just to figure out the simple idea or theorim behind it and its adaption on real problem, and further, how to generalize it to more universal conditions.

[**Set VS Space**](https://math.stackexchange.com/questions/4362803/set-vs-space-in-definitions)
In general, set is a concept with wider generalization than space, or we can say that space is equivalent to a set equipped with some operations.
![image1](resources/faa959d91d354de4855c64a246625969.png)

[**Probability Space**](https://bjlkeng.io/posts/an-introduction-to-stochastic-calculus/)
What support us to measure an event, a group of samples, with a quantity is the main story of measure theoretic definition of probability which can be extent to infinite sample space.
![image2](resources/f582778c76c7430a97a8de3609c77487.png)
![image3](resources/edf7dbd1e31348b4b8819324e13ecfaf.png)

![image4](resources/c51ae71ba7ec4f44bc221e09a48a6298.png)

![image5](resources/117073326da84204a82adc2f991c1aa0.png)

And event space defines a closed set that:
1.  ![image6](resources/d8c667e9bc5f41a5b43046f7dbbfdfe3.png)
2.  ![image7](resources/00374832ad554818a43b67724e9c5ea6.png)
3.  ![image8](resources/e7bf176d4343413f83745bd5640eec7d.png)
![image9](resources/0e1eb4797e3540f58c8e07b08eabfac5.png)
1.  ![image10](resources/2c4d88920856424883681d47ccc4c1e2.png)
2.  ![image11](resources/2de38030ebef40b394ba7b7b8ae6d670.png)
3.  ![image12](resources/4ec3cafd650d446fa62e2fae9b75205c.png)
![image13](resources/ce6dd0d702ee47568a8648dfbb1e2335.png)
It lists out the measurable events we can take as we do in finite sample space where measurable events are implicitly the power set of sample space.
Measurable space + measure rules
![image14](resources/04b9d84c51344305871dba575ffa7541.png)
1.  ![image15](resources/992c67e9e32d4ee787e243ba6d7c51ec.png)
2.  ![image16](resources/b168971e46df4030a23d8e61bce65976.png)
3.  ![image17](resources/31a4fcbc72c34ebca05b89e72a00bb39.png)
![image18](resources/24031050653544e8bb6fa75ffce5e4fb.png)
![image19](resources/21a22bb68943471aa7ec6c26cda4e3d4.png)
1.  It maps measurable space on sample space into that on real space
For finite sample space

![image20](resources/b0d13c1b75b947edac21df7df0ae4b7a.png)

For infinite sample space

![image21](resources/75da27a581f14266921abf6d980142d7.png)
2.  ![image22](resources/313be5f66a744fbfb4bba12e5fe2d03d.png)
![image23](resources/cd162e026da24227b77076b8618d7258.png)

![image24](resources/abcc8698aafe4c0c86bd95f0080939d0.png)

**Gradient&Derivative on Specific Direction**
**Basic thoughts:**
Multivariant
![image25](resources/1e74efdd6ce5499fb9f4564398c90ae6.png)
![image26](resources/bd774e16d69c48ea82ac9180a2be0ac2.png)
![image27](resources/14eb2957afa54e5fa74fb65983fde2d7.png)
![image28](resources/47d2ef572b594e48a915872146a3ec13.png)
![image29](resources/0a7a88fd83f7487c8f032d6c0a27fb74.png)
**Confusion between Gradient and Normal of plane**
![image30](resources/15ede2a5db2540b79aebca112741e808.png)
What's different is in multivariant case tangent line turns into tangent plane, and its normal is marked as
![image31](resources/75d5fb1e71b64bbb97c174bc7232b968.png)
![image32](resources/1eeede2647444b759c1b0a13e516ed74.png)
![image33](resources/d30b75fac47643b1817fb8061e7afd11.png)
This can be verified as an analog to a line in x-y coordinate system
![image34](resources/8de82f2017524728abe15918ca8fc521.png)
![image35](resources/28445725edac4a60aaa3cece7ba40362.png)
[Why gradient indicates the direction of increasing](https://math.stackexchange.com/questions/223252/why-is-gradient-the-direction-of-steepest-ascent) ?
![image36](resources/3398939403a847fc9e0a5d5d031603b9.png)
![image37](resources/17d5ef2c0bae4aabba1d78349a3cb2a8.png)

[**Calculus of Variations**](https://bjlkeng.io/posts/the-calculus-of-variations/)
![image38](resources/00fe0bfba1a449b0858f1d5019c8c364.png)
F is infinite-dimensional function space
![image39](resources/77ea20a8571747348dcf74ce969c228f.png)
![image40](resources/de9941d46db84dac83a053ab49f6d2fa.png)
![image41](resources/03d3d331e24a425aacc4f6d05eea8671.png)

To find stationary, a functional must satisfy
![image42](resources/c6237fb0bc0d4d9a88d47547424e6b2d.png)
Which is known as the Euler-Lagrange equations

[**Calculate vector's derivative w.r.t vector**](https://zhuanlan.zhihu.com/p/36448789)
![image43](resources/88f9a887d4d94ef48a83a9ff2080e575.png)
![image44](resources/c710e3af702d48bcbd7df12aacd6ce47.png)
![image45](resources/524b8658d42e466aa0045b746b70bac0.png)

**The Exponiential Family**
![image46](resources/c3d41644e2014d1d8094f3e292550d2a.png)
conjugate priors
![image47](resources/fd2e0148340c4dccbec505f33c1155b8.png)
![image48](resources/8a32138e41cd49f195bfa706e73fd3e8.png)

![image49](resources/ac37bf456aad42779340ab822ce67469.png)

![image50](resources/5d97ced5eb214faea6d765742c386f2e.png)
![image51](resources/e593914fbc9a4382b07f52bece646d99.png)
*The posterior has same form as its conjugate prior*

**Notes of Analysis \[Tenrece Tao\]**

Lemma 5.3.14
Prove keypoint: for a non-zero real number, its corresponding Cauchy sequence must exists an element having arbitray distance away from 0

Proposition 5.4.14
Prove idea: Usage of Archimedes property (Deduction 5.4.13) and Proposition 5.4.12(bounding real number by ratio number)

Theorem 5.5.9
Prove idea: prove that E has at most one supreme and at least one supreme
By definition of supreme, we find supreme by keeping looking smaller upper bound until the smallest one, that will generate a sequence of upper bound, which can be proved as a Cauchy sequence, then its limit number is supreme.
Archimedes property (Deduction 5.4.13) can be used to construct the desired upper bound sequence
The uniqueness is based on Proposition 4.4.1

