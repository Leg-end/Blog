---
title: Statistical Inference
published: 2023-09-10
description: "Probality foundation of sampling method"
tags: ["Statistic", "Estimation"]
category: Top-Design
draft: false
---

**Problem & Analysis**  
The target of Statistical Inference is to estimate parameters (or model) of interest according to relevant observable samples. By applying specific metric on the approximation between estimator to desired one, this problem can transform to an optimization problem.

**The role of Statistical Inference in Pattern Recognition**  
Statistical Inference tells us whether a pattern is a good estimator that can generalize to out-of-distribution case
e.g. modeling pattern a relationship between gender and phone number is not a good choice than gender and height, but how can we measure the quality of pattern ?
By constructing estimator base on observation, and how good is the estimator concentrate to its expectation, how stable is the estimator against infinitesimal perturbation applied on observation.
We know that model equipped with bad pattern maybe chance level when practicing even though it 100% fit on training data(overfit)
In that perspective, Statistical Inference is a useful tool to design a good estimator which can help us find good pattern

**Fisher Information**  
From [Wikipedia](https://en.wikipedia.org/wiki/Fisher_information):
The Fisher information is a way of measuring the amount of information that an observable[random variable](https://en.wikipedia.org/wiki/Random_variable)carries about an unknown[parameter](https://en.wikipedia.org/wiki/Parameter)upon which the probability ofdepends.
[Low Fisher information therefore indicates that the maximum appears "blunt", that is, the maximum is shallow and there are many nearby values with a similar log-likelihood. Conversely, high Fisher information indicates that the maximum is sharp.](https://en.wikipedia.org/wiki/Fisher_information#Definition)

![image1](resources/d13f026fb81b4a6bab885b034b319950.png)
![image2](resources/d70cd603b10b434e87cc316e7f3d592a.png)
![image3](resources/0adccd71d4294abfb757c77b25b3ff5b.png)
![image4](resources/4185f37b6922406995bee93e29c9ebf8.png)
![image5](resources/474b6bfa7a68465cb55d567f52fa0fc6.png)
![image6](resources/c7d1b38d536b4b5facf6333c4fc9e924.png)  
Since  
![image7](resources/866751357951478dba7232c4a5dc1859.png)

**Converge in probability & almost surely**  
**Converge in probability: law of weak large number**  
![image8](resources/0505b4a4e4e3457d8c43cc89ac6039e3.png)  
It would be more easy to understand by making an analog to converge of series
![image9](resources/0743bae2444645a6a1f28ee56b319fc7.png)
![image10](resources/bedf9cca81e240b8b521b2fd65ab4786.png)

**Converge almost surely: law of strong large number**  
![image11](resources/d2230a2398ee4e07be0c2d08cfcefcbd.png)
![image12](resources/09e33bef757241b3b4b0bebcca0ce3a8.png)
![image13](resources/9c58ab17bcac4716a15d74c155314b60.png)
![image14](resources/0eee0fd96deb4209b8456d6e3f0251e6.png)  
Proof(see 5.8.4):  
If we make an informal analogy to converge of series, it's similar to
![image15](resources/83cd1ef3379543afa4fafa38cd20085e.png)  
We can reach limit value from any where

Note: in large number form
![image16](resources/d8de9268216f425fa235eebeb1eae3f7.png)

**Connection**  
Converge almost surely implies Converge in probability, actually, sequence of CIP implies sub sequence of CAS, this is also similar to series

**Data Simplification : Statistics**  
What is statistics ?  
It's a mapping from sample space to a real number

![image17](resources/1fa0ec6ad1fd42bbb5c08c89459d89dd.png)

![image18](resources/7b90e7eda4b54264998aa630e90b6d13.png)

So it's a division on sample space

![image19](resources/b76fb1366bd140bbb5ac1af438537aba.png)

In that sense

![image20](resources/f7f0443c2c5a4531929fb2e1e7f06617.png)

![image21](resources/744fe3f2f5bd47c5b8483fd04e5f2897.png)

In more general way, any regression and classification(learning from data) is a process of finding corresponding statistic
![image22](resources/4e02cc88f87a45bbba2c15f4e587fd16.png)
![image23](resources/7f67e5af9bb14111883188cc3cdabdd4.png)

![image24](resources/470fc73a05b04cdcb55e6491b8012f4c.png)

![image25](resources/7bdfbaec336d43a9b7bdc6c20564df46.png)

How to find it ? By factorizing the joint distribution (**proof 6.2.6**)

![image26](resources/050482ec628b45158c14e2e8a150a56a.png)

![image27](resources/c08f67b15767471982dc69af6dde00fc.png)

(Bijective)Function of sufficient statistic is still a sufficient statistic

![image28](resources/15616e187369424795ed0056a9f0461a.png)
![image29](resources/ef27fa60a08445ceb56af695d06e83a7.png)
![image30](resources/bde9d06babcf403cb299a9056c88aa9c.png)

![image31](resources/3fc8262ed2d143d795e09a3f8d325193.png)

How to find it ?

![image26](resources/050482ec628b45158c14e2e8a150a56a.png)

![image32](resources/99dd13ce936d4b0580a3af1aa73c6ae9.png)

![image33](resources/34c745a15f5149659c037b05661edaac.png)

![image34](resources/94ba0986e8214869b94c047c048272f7.png)

![image35](resources/e011a9a6e9c646b2886135d07a9e7e42.png)

![image36](resources/a3312d466106456b9b52e3ca0e3a24a4.png)

![image37](resources/029450a6840643a3add40324a0f9054a.png)

Proof:

![image38](resources/0781a2ba3b914a9da6878b04fda8cb2e.png)

![image39](resources/41cb8d712a3c468f9da787376d380791.png)
![image40](resources/b375c517a4ac4c1a83c8d66de58b5ece.png)
![image41](resources/be739658f4a54d79866bf01d6f712f20.png)

![image42](resources/6e11574b750243bea993bdf01fbba420.png)  
[**Complete Statistic**](https://stats.stackexchange.com/questions/196601/what-is-the-intuition-behind-defining-completeness-in-a-statistic-as-being-impos):
![image43](resources/1616c0a0e33e40bead8ea792b72fe46d.png)

![image44](resources/998b68d4ebbf4c9bae5d29b0812a3903.png)

![image45](resources/299e9ceccbf048439bf612380345bc8f.png)

![image46](resources/9c7997d11e33476ea4eba0a1ca9f574d.png)

![image47](resources/b969482675724211962f819942356048.png)

What's it for ?

"[WhenTis in addition complete, there can only be one unbiased estimator based onT](https://stats.stackexchange.com/questions/44086/intuition-behind-completeness/44135#44135)"

Recall that a unbiased estimator satisfies:

![image48](resources/68fda001d0f94cf4b1b22e3bdc2d5a6c.png)

![image49](resources/687c42d89c1d48ebb40e008c38bc3815.png)

Proof for uniqueness:

![image50](resources/bba2767767f649df8f6362f87054ce66.png)

![image51](resources/8ad91f665b614e24898f2b1a913a8acf.png)

![image52](resources/22c74edf2e5347528d9df3bdf16e1594.png)

![image53](resources/0f76cdcb6574465fbd23beb43e5bd6d3.png)

Also, any complete statistic is minimal sufficient statistic if there exist one
Basu Theorem: Ancillary statistic is independent to Complete statistic  
![image54](resources/e3c861fb6490463ea00b34ee1fc7688a.png)

![image55](resources/f2e6e745cce445adb0bd5988a74b6a53.png)

e.g. [Order Statistic](https://en.wikipedia.org/wiki/Order_statistic#Notation_and_examples)
![image56](resources/e31112a67d834935a05f751f142371fe.png)

It's a **sufficient statistic**

![image57](resources/1673159379d84cb4b145189957e99300.png)

![image58](resources/10e763e05428481d84ffe712116d0bb8.png)

![image59](resources/25516d74b48e4ba49c5095b1a8429b2a.png)

![image60](resources/a5874387f7224de4a381e19ee2f106df.png)

Joint Density Distribution

![image61](resources/b5098840f3fe40d0977f37f8a17436a7.png)

![image62](resources/ed46ed1b1c8841d6b167ec8393890780.png)

![image63](resources/fd47d63ddc98407ab1fb27ac3f320a43.png)

![image64](resources/c14eeb9cd1f44faba4c5de2b38f8eb0e.png)

![image65](resources/d99019dc0f2e42088da32342b58d3850.png)

![image66](resources/5174bfcd565c4dfbac856213ee2cb7aa.png)

Replaced with

![image67](resources/a2d8fa5c8eb24e1db98342c0ca882c61.png)

![image68](resources/b61c4c615dab43e39219c7e6e02216d4.png)

![image69](resources/e88bf9a2b1c745d89953806da10c3c26.png)

(R,M) is **minimal sufficient statistic**.

![image70](resources/944e3c6050fe4bdfbaa9bea47fc256a8.png)

![image71](resources/501d0221433142abba942b7480304d32.png)

![image72](resources/aafcc3ba9a85484f83425ddb1cb083dc.png)

![image73](resources/8cd0cc2378564685acf631e81911932e.png)

![image74](resources/23e849d7b4924c9fb0a1378c4dec92ed.png)

![image75](resources/efa2feccc7a64b83b717d2f7da0f3539.png)

Also, we can find that function of minimal sufficient statistic is still a minimal sufficient statistic

![image76](resources/1aa5ae0a81164541871beeddbe963f44.png)

![image77](resources/981fd15ab8a449579ab4028e337fdf2a.png)

![image78](resources/aec0018b969742b3ae0eb1a4b3f4c3f2.png)

Further, we can test its completeness

![image79](resources/8e74caed10bd4144afaa2b025c6f0cb1.png)

Which is a unbiased estimator of zero

But it is not identically zero

![image80](resources/c55a761161704f7193e9cd45a2b253ae.png)

So it's **not a complete statistic**

**Connection between Statistic and Estimate**  
If a statistic is a sufficient one, which means it contains all the information for inference of parameters of interest, then it's statistical form, a function of observation random variables, can be acted as an estimator of the parameters we cared. When real values were observed, an estimate or estimation can be evaluated from estimator.
In more general way, statistic is more like an estimator and estimate is a statistic for specific samples

**Estimator & Estimation / Estimate**  
Estimator: a random variable that we are interested at has its form as a function of observable random variable, different functions(rules) result in different estimator
![image81](resources/3815cfef0c494a089f3332f49d87fbbd.png)

It's a way of simplifying data where we can extract key features of samples
![image82](resources/b3cff2e5927d45658431eb198bccbd77.png)
![image83](resources/a4aa16f1d99244fcaa0ad820d06b63cd.png)

There exists two perspectives solving this problem.  
**(1) Bayesian Perspective**  
Treating parameters of desired as random variable, all estimation work is basing on posterior probability distribution
Given
![image84](resources/6562c42bdd9e4b1ebfe5fd699fbfd154.png)

![image85](resources/cba25b05fc8c407b99b2f820f208d0b5.png)  
Yield  
![image86](resources/3ae16cd622af45f48bd73c781ff14296.png)  
[The procedure of finding posterior can be an iterative process](onenote:#Regression&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={15B84857-BF9F-44AC-822C-CD1C7CABB718}&object-id={1B433145-811F-4084-9CB0-2ED0EA324946}&65&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one)
Estimator under Bayesian  
![image87](resources/7202747139e54362aaafe2c4b5979103.png)

"""Informally, the max posterior rule can be seen as max rule, while LMS as average

So we can have max posterior estimator and conditional expectation estimator"""

![image88](resources/164a2a0b1eda49f997fd2491f9a6c269.png)

![image89](resources/9b63b54815a64c798d3163bdf3991aaa.png)

![image90](resources/2bf317a8216e42cbbd562db040a819d9.png)

![image91](resources/f1d6d2da63f74bdb830782e6c9fc9a47.png)

![image92](resources/7ee4506e707042e89ce5a093e0167721.png)
![image93](resources/207477f5b96a4256980d13b10ef384e6.png)  
Respectively, we can have max posterior estimation and conditional expectation estimation

![image94](resources/87b44b4118f444b28144ce921f1b5feb.png)

![image95](resources/5a5c7c44d693488480ac24146dd879e9.png)

**Special case: linear regression(least square method)**

![image96](resources/4a962b05f05b48a89b56e195f774ebb9.png)

![image97](resources/99a1829367444300a6b84c051409c3df.png)

![image98](resources/8e2dc87ee31c46fd98d936e65efeaf5b.png)

![image99](resources/9387e305cda147aea980ec671b02f4b0.png)

![image100](resources/04ea2b1be14346ac9fd788385c5c16ec.png)

![image101](resources/46e7e566e92a47feb667493f25e36b67.png)

![image102](resources/135720f64a424d369453c97a257a6395.png)

![image103](resources/caed1a9ba96e4ec8806227b0a183cfae.png)

**Special case: linear regression(least square method)**

![image104](resources/650ea5f2cc964524870f3b8ce8ea7f3d.png)

![image105](resources/18cf972aa85e4ac0b401c889b1da1ac9.png)

![image106](resources/32ed2e09de7b4d2ba89cd39a5a633caa.png)

![image107](resources/812428165c374e0e81648440a0042b17.png)

![image108](resources/f17ca961655644aca4b1bc58396d50db.png)

This will link to [our discussion on regression](onenote:#Regression&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={15B84857-BF9F-44AC-822C-CD1C7CABB718}&object-id={E7CD12D4-253C-4FF9-9030-43CEB80DE0CC}&2B&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one)
![image109](resources/3241581e0ced435799c3a4bf82caa94b.png)
![image110](resources/ca9c92cf380c428ca0ee9ecb53bcce80.png)  
Actually, we can make an analogy to classification accuracy metric
![image111](resources/d22d131f96924f75b799d37439746429.png)
|  | True | False |
|----|----|----|
| Positive | ![image112](resources/d9735ac4640545c6b8da4a7d93f2ca53.png) | ![image113](resources/2999c6f3d6044830916a16b455b106ab.png) |
| Negative | ![image114](resources/70417a1fd8cd4f9e9e4d6f70c68f8140.png) | ![image115](resources/d22457b65207488b8a59587b068a5f7d.png) |
![image116](resources/b97a6a3f0fae43c6b0fd695767b02715.png)  
What we interest :
How good is our decision

![image117](resources/a5cd7e33d4124e05a02f373ba5730f73.png)

![image118](resources/620b4f48ac6c4b038baa239787e79c6b.png)
e.g. for binomial case
![image119](resources/cdd06ca32b5b4fddbe1f55b231ccfaa8.png)
![image120](resources/a35737880cd04dd893f9d582f1f795aa.png)
![image121](resources/c7740d75b79348afba796c9fe00d0b88.png)

**(2) Classical Perspective**  
Treating parameters of fix constant, we can make an analogy from Bayesian
![image122](resources/6f8b073813f14c69a006fe4d81334aa4.png)

**Transformation from MAP to ML**  
![image123](resources/4a7085bfd7174584af97110126d0a975.png)
![image124](resources/f81b0a9d620840afbe690f6d0f351477.png)
![image125](resources/7744e7206c2649618e65293cdbc9951b.png)

Estimator under Classical  
![image126](resources/35cae7bcab7f478b8f951a507318e0e6.png)

![image127](resources/8cc4204a5f8840a59a744d46262e2d70.png)

**Special case: linear regression(least square method)**

![image128](resources/f3343323852345c0a12c0f1baa70d9f1.png)

![image129](resources/c291178748834baea4c6a52c7007120b.png)

![image130](resources/67767d898acd4547b43491e81bdfe42d.png)

![image131](resources/d7103525fee74e54b2278c3fe2f4a860.png)

This is equivalent to no prior case of Bayesian linear regression
Error Estimator  
![image132](resources/1c882a7eb2354b898a529056e6b2d0a7.png)  
Bias Estimator  
![image133](resources/c580d3d9c13341b087348cd0941064e5.png)

![image134](resources/ac86ec55d2254ca488effc5a35284ba0.png)  
An important property of ML Estimator ---- approximately close to Normal
Provided  
![image135](resources/22ce619e015a452da77d6f07aae29ef5.png)  
Yield  
![image136](resources/293047dc344b43bba4820b93bb65e256.png)  
This property plays an crucial role in finding **Confidence Interval** and **Rejection threshold**

![image137](resources/37b0c7af15544f52b7aa592bb0edf0be.png)
![image138](resources/6ecf3de41c304f37bbcf9a391fac9505.png)  
e.g. Confidence Interval  
![image139](resources/3dbe270d00594a4c956efc1069aaabf9.png)
![image140](resources/833a37a2afa1418aac30f506d826db78.png)
![image141](resources/3def4e721c004cab99b93585d90aa083.png)
![image142](resources/5fa4c0aa346d41339f7697c2b5b509ec.png)  
e.g. Hypothesis Test  
![image143](resources/9a5abcf749f34d8b973a16957e0021a1.png)  
e.g. Significant Test  
![image144](resources/feab9726980c419a976f0b2a9742abbb.png)

**Classical simple hypothesis test can make analogy from Bayesian's one**  
We now only consider binomial case, as an example shown in Bayesian  
![image145](resources/9fd2ec587c56424380664184f6f02d3d.png)
![image146](resources/35f95b45dd8443248a86de3d0ae2241e.png)
![image147](resources/67465921d146482f815e67140d09629f.png)  
Base on ML code, we want to know how confidence is our decision  
![image148](resources/15a6671afdb94696a5113d18f4838d74.png)
![image149](resources/14e5ab9099bf459a8596e48580d5da91.png)
![image150](resources/5312f1d4efaf4975a9573242e6caf5d1.png)
![image151](resources/c5f51d90d8174317948e35ac7a8c81fe.png)

![image152](resources/67a5f6d609424e44b691bdb8b6d64ce6.png)
![image153](resources/95147e4e18ff4fac867616294da899e9.png)
![image154](resources/69da4429567a45b09962d406fd4fb806.png)

![image155](resources/ca256e26d0384480a4beca2a163d7c7c.png)

![image156](resources/6ebee11ea41e48e99e07ac479ec919bf.png)
![image157](resources/1f27c0f9c92d4245a19a9b727998036d.png)
![image158](resources/e37a5b0101764eb1a47e99b6ac60f54f.png)

**More general adaption: significant test (with complex alternative hypothesis)**  
Definition of significance  
With lower significant level a un-support observation shows up, the higher significant confidence that the hypothesis should be rejected, i.e. when such case of test shows up, we are confident enough to reject the null hypothesis.  
Now we only care **when** should we reject null hypothesis, and with **how possible(significance)** such case will happen
![image159](resources/f32355b580834c599d5d8708874bfcd2.png)
![image160](resources/cbaefe92ff334e40884f3de802365916.png)  
Observe  
![image161](resources/9b53f665d0374421b9bf640cc57a4849.png)  
Estimator  
![image162](resources/91c3778782004f1586f9e8c05dc1c492.png)
![image163](resources/e1fa7a866db44dec869cbea139d5adbc.png)
![image164](resources/3ec24fddbd204dda8c936b838d20d08f.png)  
Significant level of rejection(p-value)  
![image165](resources/50cb1a3cadaf4a4db49c37089be79001.png)

i.e. the frequency of when test fall in rejection area

![image166](resources/022dfba05f084a31b8f0f7b21095b71a.png)  
Find threshold value to match significant level
Recall the estimator's property of approximately close to Normal in Confidence Interval, which comes into handy to find the matching threshold

![image167](resources/d520e790869a40c88b168d4979a2474b.png)

So the key is to design estimator with such excellent property

e.g. set estimator as ratio of likelihoods

![image168](resources/bcfa389dfcea4391b6e273332bd45be1.png)

![image169](resources/0c79c145313c4406b43f2bfa0f82088e.png)

![image170](resources/dfce02aec44b43d19f53bf51eae1c404.png)

![image171](resources/344dac0ca7224f1db9edc4d507bae8cc.png)

![image172](resources/e562ba62023d49f599d172fd75a2e173.png)

Note: we can think back to the case in simple hypothesis test

Since maximum likelihood has minimum significant level, i.e. has minimum rate of making error rejection, according to Neyman-Pearson lemma.

Assume that we use other estimate

![image173](resources/72a5789c6f3b428ca478811828b30966.png)

![image174](resources/eff18c20dbf645e39dc1ef99bcdeab1a.png)

![image175](resources/283fafe8f09d47269ce533865c52adf5.png)

![image176](resources/57c0e9acefc346f6b464127cbf8b267f.png)

That means when a rejection happened under ML case, it must happen in other cases

So it gives us the most tight rejection area matching the required significant level
