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
First let's start from our familiar standard calculus, i.e. [Riemannian integral](https://en.wikipedia.org/wiki/Riemann_integral), but do it more precisely
![image1](resources/0e8600205a0b4679b241f1330ee75149.png)

![image2](resources/20fde0f42e4e45f78ccbbacd70851a6b.png)
![image3](resources/6a5f477068854e55847d142d87d227b5.png)
![image4](resources/14ec45c1a349425895a75ab95efa3e75.png)
![image5](resources/06e189ce999f42269b7e05069d640b2b.png)
![image6](resources/103794ead21648f5ac976803a30266da.png)

We know that

![image7](resources/391cd3ba4267493db9b3136f35a9b1f8.png)

![image8](resources/e180ec2b20da43d8b7e9bff71901053f.png)  
And that's exactly matches the rules of Riemannian integral, except we need to prove that the **Quadratic variation** is 0  
![image9](resources/2c1fbcb1b7c84a89a4af12d5292b2cb5.png)
![image10](resources/b8737c761c7d4c8b92e3fd02aa98435e.png)
![image11](resources/1041ae3611ef4126a6e203001d97d64f.png)  
And we can have same form of Quadratic variation  
![image12](resources/b600898a74de4d06b0b9ad635d3c8967.png)  
So in case of derivable integrator, we can just use the standard rules of calculus that we all know and love. But what happen if the integrator is not derivable.  
The rules of Riemannian integral will collide on different integrant, that is  
![image13](resources/03e2fdfb4ae74fdd8d14f67b66bbb9dd.png)
![image14](resources/7d9011fb8ffa48fba8e1835cacb69954.png)

So informal way stochastic calculus can be seen as calculus over stochastic process, which is collection of random variables(a function over sample space) indexed by continuous time.  
![image15](resources/9b3b9346df6147c68b2b6be7e3e6e3bb.png)

![image16](resources/52be234fab3c4d0a9e505a4cb4e62e0b.png)  
The slight differences to Riemannian integral is how to deal with integrator of stochastic process, which is indeterministic and so its underivable.  
Why it's underivable w.r.t time ?  
![image17](resources/828673e65dc34e039782860a83b358b0.png)

![image18](resources/02007a2b3c87420ca468504690bddbb1.png)

It means the increment, or path, between infinitesimal time interval is deterministic, but which is not true for a stochastic process, since the variation over infinitesimal time is randomly distributed

So without existence of deterministic description for variation, nor stochastic process is derivable

Further, such property, later we’ll see, is inherited from symmetric random walk.
Underivable stochastic process leads to non-zero quadratic variation, which results in divergent integral limits due to different integrant. That’s why the standard rules of calculus fails over it.
Note that Riemannian integral works out only when we have convergent integral limits regardless of different integrant.

To figure out what stochastic calculus is doing, we can make an comparison between regular integral and stochastic integral
![image19](resources/b8e1df514be344df96eb4ccfaa7a0496.png)

![image20](resources/24c365844b7146a89ee2d97ea2cd5cf8.png)
![image21](resources/7d36f871f921433589ce5a8254508fba.png)  
So the output from stochastic calculus is accumulation of random increments, which is also a stochastic process.
That is a stochastic process can be a function of another one, and so is its statistics (mean, variance).
Provided statistics of its "x-stochastic-process" are known, so is its distribution, from which state at specific time can be determined.

Actually, there is **idea** works beneath the conversion from randomness to determinist or consistency between them.
Recall that stochastic process is underivable, but that is only established in deterministic space, can it be derivable in random space ?  
First let's take a look at the definition of the regular derivative  
![image22](resources/1638db08d7ba45d8a5652ffcdeb7ad5f.png)  
But such limit does not exist for stochastic process, since it's also a random variable following some distribution
![image23](resources/12e053158334412098fc1adc43787aab.png)  
Note that a random variable converges to its mean almost surely if its variance converges to 0  
![image24](resources/87367964c32e4aeea6230038c7fb346b.png)
![image25](resources/ac21ccd8c72745abb9b0ca71f900f36e.png)

Or equivalently

![image26](resources/a6ffe405cd8c453388e16ea6093cbb0d.png)  
Under the support of probabilistic tools, the definition in deterministic space can also be established in stochastic space and so is the conversion from indeterminist to determinist

**Stochastic Process**  
Let's start from a simple instance of **one dimensional symmetric random walk**, which is a discrete value, discrete time stochastic process.  
Here is the deal:  
An easy way to think of it is: starting at 0, at each time step, flip a fair coin and move up (+1) if heads, otherwise move down (-1).
![image27](resources/19c8a12020c041f9a29fc6c8f6b57f73.png)
![image28](resources/aa9ac04632534b6fbd148b156b9479d2.png)
![image29](resources/259451eb34704eada9105370e8a8ddd6.png)
![image30](resources/6f1419e74c444ca78a5efbc2782c53b0.png)  
Increment between any pairs of time step are independent, since any increment can be summation of independent Bernoulli random variable within.  
![image31](resources/c85e5cdf180a4b97a98b7c4384750632.png)  
So the state at any time step may have expectation stay at origin, but with deviation (variance) accumulating at a rate of one unit per time step.

The next is to consider a **scaled symmetric random walk** extended from its simple sibling  
![image32](resources/d74fedf0ce8f48dcba44deb171c35fe4.png)
![image33](resources/5cb3fe1b05b4404cb7cd20b09306870f.png)
And it follows the same properties as simple random walk
![image34](resources/dade61e4890842d2bd85f2b92fd5a3ba.png)

It has non-zero Quadratic variation  
![image35](resources/9a946a1f9f0e44b6bd72272c495d5c74.png)
![image36](resources/a55a57b4b9df4e32be866d760d68535f.png)

By taking the limit of scaled symmetric random walk, we can arrive at the definition of **Wiener process** , a continuous time real-valued stochastic process, which is inherited from the scaled symmetric random walk  
![image37](resources/0e22371620ae45fc9958972a7b89c346.png) 
All increments are identical independent distributed  
![image38](resources/7bf659f577e64c7aa42b606bd9dfc8b7.png)

![image39](resources/2ffdf798f7674b5bbd3cae6902fe3df5.png)
![image40](resources/8d7c9d4622e64991be17ad3367cb2adc.png)  
Most importantly, quadratic variation follows consistently  
![image41](resources/6bb06d2cebf5441987ff5a2b40bccbb0.png)  
This is at the core of stochastic calculus so that we can describe stochastic integral with its statistics  
![image42](resources/ae029d3930634ea9b3651844f1fd38c5.png)

![image43](resources/8c1c83a7ee444f81a28709ea8e662f1c.png)

Due to some special properties(independent increment) of Weier process, any continuous time stochastic process can be written as function of it:  
![image44](resources/8cc419a87bfc44749c21cfb686d84d21.png)
![image45](resources/3b4433dc26c64cdfb078bf0a3b740d73.png)

**Relationship between Gaussian white noise and Wiener process**  
Using the [definition of derivative in probabilistic space](onenote:#Stochastic%20Calculus&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={B902F5EC-F124-4DA3-A095-4D81332902CE}&object-id={AE9D6B8B-1D99-0A05-0AA7-DE6ECE92FC4B}&C8&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one), white noise is the derivative of Wiener process  
![image46](resources/7c8e2eef8085414d8373a48e64ed6f1e.png)  
Note that Gaussian white noise(also a stochastic process) has zero mean and Dirac delta time correlation, it can be proved that derivative of Wiener process possesses same properties  
![image47](resources/b2d909f2f8024679a415f7020b333c69.png)

![image48](resources/a73f866f22a94c5d991a31ea7a8fb728.png)
So we have
![image49](resources/58ede5b4a1a04ce49f675e1b23ccd9eb.png)

**Solving Stochastic Calculus**  
It's quite a tangent from where we start, but with a depth diving into Wiener process, the building block for any continuous real-valued stochastic process, now we can move on.  
Replace back into stochastic calculus  
![image50](resources/5895ffb42b7a47cb988c0517ee435544.png)
![image51](resources/a4f1ebe6406a45d2b5dfa172686b0801.png)

![image52](resources/b59dc99e8b2d444aab09496748624985.png)
![image53](resources/50e4fc5c8b594a24a0b2e5a12235db81.png)
![image54](resources/282a0fd9aeff487fafea57b31eee4498.png)
![image55](resources/611ae9d8636c4676a039fde37923977e.png)

![image56](resources/92649d10bd2e47788da782beff2e53f9.png)
![image57](resources/f1b86b26da42436a913f8ae0eb4d31b7.png)
![image58](resources/29aa8df7f7e24de197254e6d596560fa.png)

![image59](resources/827ea10d28f24c56ab950b174fb00984.png)  
This is the subtle difference from regular integral that a biased integrant will result in biased stochastic process. So the solution for stochastic calculus dependents on the assumption on practical problems.
e.g. when modeling stock price at time, it will be inappropriate to pick integrant in the time interval, since the information from future is unreachable, so we can only use information at current time.

![image60](resources/ac968c78f1a1484bb49cf843a2aa6d7d.png)
![image61](resources/82babb5de19e4e7b8b09cd11861f2a37.png)  
Replace back into stochastic calculus  
![image62](resources/7ce682a406714922832255d6569ea550.png)  
Which has same form as function of Wiener process  
![image63](resources/dd3ec63edfb247938e5040462c3ef187.png)  
[An instance of applicaiton](https://bjlkeng.io/posts/an-introduction-to-stochastic-calculus/#id20)

**Stochastic Differential Equations**  
Differential form of stochastic calculus  
![image64](resources/4bb58bfaa1984835951e1c672c570653.png)
![image65](resources/99d74a25f5084d2da85d6f8d29c73749.png)
![image66](resources/3dfc16b338514c97827c285c1ce92e82.png)
![image67](resources/47f697d01ae2417489b6f03b5937cd74.png)
![image68](resources/02766e3cea95431abe0c4bd9b2f66258.png)
![image69](resources/54ba81b1b5444cd190546aad8184b94b.png)
![image70](resources/831acfc25fd246d69da87665ff2d63b8.png)  
Note that Gaussian white noise is derivative of Wiener process almost surely
![image71](resources/fd91e944e5974612b5ca39db0c69feda.png)  
This will leads to its SDE  
![image72](resources/6e0916940f044694a170e85e3f79c079.png)  
In paper "SCORE-BASED GENERATIVE MODELING THROUGH STOCHASTIC DIFFERENTIAL EQUATIONS", SGLD and DDPM can be described by corresponding SDEs where the integral form all involving addition with Normal noise.
This is resulted from integral property of Dirac delta function  
![image73](resources/f0af9f7e09e04414b160f24ea565a22b.png)

![image74](resources/802f57c8c2774fd28113aecfd906f783.png)

When analytical solution exists, stochastic calculus can work, otherwise, numerical method had to be used to solve them out
e.g. Monte Carlo Simulation and Partial Differential Equation

When stochastic process has form  
![image75](resources/b11457a7ed494a469f16990ba3d5d284.png)  
It can get back to similar form by using Taylor second-order expansion  
![image76](resources/403a8637045e460184e1bfa7e706a0f4.png)

![image77](resources/118d879111d946f69a9637e2e8acdc93.png)

**Dynamics, a stochastic process too**  
From a birds fly view, we can roughly split a stochastic process into deterministic and non-deterministic parts, similar to [HMC](onenote:#Sampling%20Method&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={4F341C3A-CF66-4855-B9B3-DA4571AC8699}&object-id={8918F406-FA6B-0184-0AFC-EF8E34924A96}&B&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one), which simulates a Hamiltonian Dynamics to make sampling process converge to target distribution.
![image78](resources/346ca8f4f6584d5aba865bf2a803fe4f.png)
