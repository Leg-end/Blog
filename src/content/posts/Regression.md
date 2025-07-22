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
![image1](resources/5a49419c0f134686a4d8cdf70a7f6c40.png)  
Estimate (Hypothesis Space)  
![image2](resources/81e67f695c1c4e5e9fab25c6b0be694f.png)  
Assumption
![image3](resources/f3635806003942829776f34d0fb96b20.png)
![image4](resources/ec8f6a1c894249498e69204b3fc40334.png)
![image5](resources/8d1508f0f7514d6194be9c678c72b3cf.png)  
base on maxilikelihood assumption  
![image6](resources/e6dc747d0971497a88ffd41a076e8ed0.png)
![image7](resources/15ab0975674742d2b8a43fcb6f967b6c.png)
![image8](resources/d2a368513cdd457293e38c8a3837d431.png)
![image9](resources/77404e7c666c4f059cef5937cb38fbf8.png)

*Question: The idea behind the target form?*
*In classification, loss is a evaluation of decision, i.e a cost of specific behave*  
![image10](resources/65a1468577a342428fa504e5b584d933.png)  
*The cost when x belong to class k, while was distributed to class j*  
![image11](resources/f46b0608fdbf471e92e7ea85c87a037e.png)

![image12](resources/908583c54600427e865d35f0c3257b25.png)  
*why L2 loss? It's a assumption of Gaussian Distribution*  
![image13](resources/53f40b79a30842aa8e67958a2a68ddab.png)
![image14](resources/4e82a05b90c1468aa8fcf3a424920a8b.png)
![image15](resources/422ecfeb9fa64c859377b6dff3bacd1a.png)
![image16](resources/5b3e99b1a7fe4a32a0c240f074c8e1ad.png)
![image17](resources/6f174b6ffe8443c2ab8c9013162ab203.png)
![image18](resources/86cec136042e4e85873f81648a4002d2.png)

*we can see the component of error*  
![image19](resources/3818459c850a43d393c0404e99157655.png)
![image20](resources/7183817dd7d441c8a9ffe8b8faa4b78e.png)
![image21](resources/fdce707568294ed48c8f8b6e30ebacce.png)  
*bias: the distance between predicted model and desired model*  
|  | *model complexity* | *data storage* |
|----|----|----|
| *bias* | ![image22](resources/4237f506ee474bcc8e99b7eb17ebdaab.png) | ![image23](resources/01f3c81c7d7141c9929a858204b3f738.png) |
| *variance* | ![image24](resources/4bad7766971d4634aa286f5a8b2c1e96.png) | ![image25](resources/9e0e1c70bd694c2e894f470ef4e20d85.png) |
| *bias -variance* | ![image24](resources/4bad7766971d4634aa286f5a8b2c1e96.png) | ![image25](resources/9e0e1c70bd694c2e894f470ef4e20d85.png) |
*(1)control by number of basis functions*

![image26](resources/143d3755caf342b5b2d64d847a87a465.png)
![image27](resources/fa08241083b64dbd8f3617203299e236.png)
![image28](resources/f7b11a955dcc4d809e020906a1b70ac1.png)  
***But a perfect model, always contains large number of basis function with matched regularization***  

***Linear function(Linear Hypothesis Space)***  
![image29](resources/dcc3aa157e8847038da966e341f5074a.png)  
Assumption:genration of data  
![image30](resources/310648f41d51450d9d15ed61f46b01f8.png)
![image31](resources/f06f3db00be74a43a0da856b6eb43685.png)
![image32](resources/e224087e4bff49ae9a06fa839baff879.png)  
*a threshold controling convergence.*  
![image33](resources/7646d77e5b5547cf90fae45eadfb8951.png)
![image34](resources/467f41f9ebeb4b2fb1db72bb78a6ea6f.png)

*under log-maxlikelihood*
![image35](resources/babf06409ad84bf78e6c0f2b6866ac82.png)
![image36](resources/461714652be34852839d55b2671f8b2b.png)
![image37](resources/257682dbf1344cf58f9df54603a9645e.png)  
*(1) batch techniques : least square method*  
![image38](resources/a6a678eaeccd4513a71afa89e4d1f6ed.png)
![image39](resources/0927b2faf61246b786843779dfe935ec.png)
![image40](resources/35013e6543a840b098202bddcad612de.png)
![image41](resources/2a0e5e8129904950a4cba78c3362f1b6.png)
![image42](resources/816885b3f28242ffbe8926f73b5b77af.png)
![image43](resources/03d0219cc6c5474ead17977472412f0d.png)
*a [regularization](onenote:#Regularization&section-id={206D0DBC-E353-4C40-ABB7-20922DEC5824}&page-id={74105814-BC3B-473C-908D-0AEB72711C85}&object-id={5DB304C5-ED6B-07BD-3264-4A7AC3D63882}&12&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/机器学习.one) term was added*  
*Note: In words co-occurence matrix, a assumption that each word at least appear once*
*was introduced, in case of dividing by zero*

*(2) sequential learning : gradient descent for each data point*  
![image44](resources/fd9d9ff6286a4d7ca60e68721c1ad291.png)
![image45](resources/b3eea00fe59e44b3b0b0b5efe7d32221.png)
![image46](resources/ad6cbefc408a4143b6dd31c454191211.png)
![image47](resources/a88e35dd2a0445f0a519ee218697aa3a.png)  
*convert to a sequential way*  
![image48](resources/aa4a45c61d534540840364f25433cde3.png)

*Stochastic approximation*
*Robbins-Monro Algorithm (todo): a generalization of sequential way aforementioned*
*a sequential estimation to find root point for unknown function*  
![image49](resources/0a8f19860ec041d6981f671373dc80d8.png)
![image50](resources/78e405b053694871843d94099b4162a8.png)  
*provide a support for convergence with probability one*

***Bayesian Linear Regression***  
![image51](resources/53664b9a43964a1588ef6636bc9429bf.png)
![image52](resources/7d9c2ca0262c486b852f08250de95c6c.png)

Support idea: If two sets of variables are jointly Gaussian——[conjugate prior](https://towardsdatascience.com/conjugate-prior-explained-75957dc80bfb)  
1.  then the conditional distribution of one set conditioned on the other is again Gaussian, and **it's mean is a linear function of prior's mean**  
2.  the marginal distribution of either set is also Gaussian

Key-representation of proof:  
![image53](resources/9e6ce63323074cd08c7c6a3756da4698.png)
![image54](resources/51f6d82000c34e3cad9a2a1129d6518b.png)
![image55](resources/e75ec3603e734ac69628a6920a3330af.png)

*Result:*  
*Given a marginal Gaussian distribution and a conditional one*  
![image56](resources/4fbaa3dcf7034717892eed6abac869dc.png)
![image57](resources/77ededec5c2649c38bbd114a0ac2ff5b.png)  
*Yield the one switching on random variables*  
![image58](resources/67cb1650c2df46008499a02e9ffd7d14.png)
![image59](resources/bf5ae513a4f348f9ab69ef441592d8af.png)
![image60](resources/246b1b18cc6049a886ce354d74d062dc.png)

![image61](resources/f5b7a7a2fa51484c8be62234fb64ba01.png)  
*Given*  
![image62](resources/28253f9a66f14102877183598d20d6d9.png)  
*Yield*  
![image63](resources/0f249da36f23484a87614e274e2edb07.png)
![image64](resources/d179b239a43549aebd340ba4b82a66c1.png)

![image65](resources/126282a7504844dfaa085cc38c9eabce.png)  
*Relation to Maximum Likelihood estimation*  
![image66](resources/146e87adb730499e8ccd43d058fae075.png)
![image67](resources/49618a06c115422480302582095571e9.png)

![image68](resources/37874b3ede5d4f4d8100cd90ac3cd0df.png)
![image69](resources/ac73e4c40fe44464a526ce07051d5d0b.png)  
*proof: analogyous of*

![image70](resources/038609d20613415e8b8e6c567c2ca9bb.png)

![image71](resources/18b6a008646f49269e005ef5ef6daf31.png)

*variance = noise + uncertainty of **w***

*which means, provided enough data, the prediction's variance will be*

*converged as the variance of noise imposed on generation of data*

*proof:*

![image72](resources/385b101ad8cd493ca102e656a9afc56b.png)

![image73](resources/3ec9d9bbf7cb4d108ed332e6f5e799d0.png)

![image74](resources/26008afd91f84503baac52aa145c5c2b.png)

*Training procedure*  
1.  ![image75](resources/ecffbb23f6104ffa92ad404abf04cdab.png)
![image76](resources/49e3708bf5e54829b43c6c833145abc6.png)
2.  ![image77](resources/9afdb21852954ff68dac0f2b9959125d.png)
![image78](resources/71e2857de6c640a584f9c94de972ed49.png)

*Note: it works in the same way with dozen data points*

![image79](resources/2bea169648af43099862dc8e2cb1c0db.png)
3.  ![image80](resources/a79294d3ebb2404ba9c7f7b1d9b7f4d0.png)
![image81](resources/2d5a74a4a1754ce1b2083a866baf32ee.png)

*Note : Complex calculation can be eased by using conjugate prior*

![image82](resources/09d0dd5861ec48fcbd446c88034a4a67.png)

![image83](resources/66d07de9402a4cf9b038724c2bf77841.png)

*And use it as prior on **w** on next iteration*

![image84](resources/27265429e0974e59a36a6bb9714e3a12.png)

*go to step 1*
