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
![image1](resources/ad5a68bc2dfe4fdc8e73264da45fec31.png)
![image2](resources/42a7834d8aab4c44bb62b37aedaf4d21.png)
These strict inequalities are not powerful enough in finding desired hyperplane, Since we can get infinity hyperplanes meet the requirements, but any local solution may not lead to good generalization, so we can turn to an equivalent easier one, this is equivalent to induce regularization.
Note that that also has an explanation from [Lagrange Method](onenote:#Preliminary&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={FC3FD93B-B8A9-4DAE-B196-0E6AE03017A3}&object-id={7A3C25D5-B74D-0EE0-39CF-E4E230C10B73}&68&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one), where strict inequality constraints are **inactive** in finding optimal, so we need **active** constraints, i.e. equality constraints.
according to **supporting hyperplane theorem**:  
![image3](resources/6f55eb1599fb4add95675e35bfce906d.png)
![image4](resources/869bf317ebad4c168f76976f0580f8b1.png)

![image5](resources/1c8a8367b3fe4905b72356b081fea8bc.png)

![image6](resources/bb3ed7e640ed437aa5d5f83df63fe8c1.png)
![image7](resources/51a9677cb9e4403b947673adcb6dec4c.png)
![image8](resources/293f4f057324472a886a777b19df5792.png)  
And margins from both sides reach maximum when they are equal  
![image9](resources/5d6498a897eb4393b34e3ca468ca429a.png)
![image10](resources/fb7aab25f80e4c71a7c11e1f67f7cdd7.png)
![image11](resources/86e9964bf7904e2aa7de4406ab7bf268.png)  
***Ideas behind***  
1.  ***Find equivalent easier problem***
2.  ***Meet the requirements that solve it***

**Analogy**  
It's bit of taste of KNN, which makes decision based on instances. While SVM only depends on support vectors to make decision.
They both use a **kernel function** to measure similarity between new data and support data, more specificly:
Note: you can take kernel function as a metric function, but in kernel-specific feature space. (In that way you can also treat it as a tranformation between feature spaces)
KNN, kernel function(new data, all data)
SVM, kernel function(new data, support vectors)
actually, when using radial basis function as kernel fucntion, the number of support vectors is in positive relevance with the value of sigma. And once sigma is small enough, SVM will degenerate to KNN

**Adaptation**  
![image12](resources/3abe56c518574626a30a547f4b5f02c7.png)
![image13](resources/56e5bf4559214ad48839eb6d1c025d87.png)

![image14](resources/8811b683bc5f4824b6a02cc2577a8acd.png)
![image15](resources/6eac881b3d3e4bbf81578f1fc2efa112.png)

![image16](resources/a983fc8f08064468b9e6d7a6fcf8949e.png)

**Optimization**  
![image17](resources/f39722ca6029405a95e30e845d751875.png)
1.  ![image18](resources/2f33540e012f4226b77720f50df02fe0.png)
![image19](resources/160c45ccd3374b86bf82123cc1b85965.png)

![image20](resources/5e39e517f78c4290bbae22744e862054.png)

![image21](resources/4357e908edb14ef19e5d689b244da38d.png)

![image22](resources/f307242e14514c96bed70967567ef6df.png)  
2.  ***Optimize it***  
![image23](resources/f196ce614f6646e6bcdb461a1bfc6e2b.png)

![image24](resources/d4c623bba8884c2caea70f3e50b7ecf5.png)

*Note:*  
1.  ![image25](resources/1cbfaaac81f24d34a43843d39f468833.png)
![image26](resources/d65b116ab67a4683b5fb0145f5fcb2aa.png)
2.  the formula tells that the norm of parameters will not be penalized when points far from plane, but they will be if their norm is huge or when points are close to the plane, which results in maximizing on margin.

![image27](resources/37e7dcb15772478b873c7253ba1c4536.png)

![image28](resources/c4598fd082da4769ada557da814506fb.png)

![image29](resources/aed43075df70452397d4f2d15b39d987.png)

![image30](resources/b1752719ecf044a49d9471e4cd106722.png)

![image31](resources/e9b3c53f4b4f40b69f6078db1397721b.png)

![image32](resources/9aa6eb7051dd47dc95b5ee0780e2d6b3.png)

![image33](resources/1c87ee813daa4b2196d9b195e0c5f99d.png)

![image34](resources/a65bf22a3078421281823a6e680277e0.png)

**Overlapping Class Distribution**  
**Problem&Analysis**  
Similar to Bayes classifier, class-conditional distribution may overlap,i.e. datasets are not 100% separable.
![image35](resources/d151ed86c86f494991590059434ce8e1.jpg)  
In that case, an exact separation on the training data may lead to poor generalization. Therefore behavior of misclassifying must be allowed.
![image36](resources/fbd2c7436e004cb18b50aa291df3662f.png)

If we still use a hyperplane to separate it, then will results each side has data points assign to its counter part.
![image37](resources/23bd77ee961f44c3a360cd7a37b0170a.png)
![image38](resources/cbc04a76ef964cd0bcd5a04e62dd2b2c.png)  
If we allow missclassification, then we can get new separable sets
![image39](resources/527eb495aa194c3faf156447d922ad37.png)
![image40](resources/76ce592913534e6e82979dbf5153c569.png)
![image41](resources/6e10a67343e74c7f997af277d930a8cd.png)  
and  
![image42](resources/6eccc15fd72348d5bffd89119288a4b6.png)  
Now we return to non-overlap case, but how can we find the support points?
We already know the support points can be simplify as
![image43](resources/43b47c40d2d14d9ca9503269b2bf3f73.png)
But for overlap condition, we have  
![image44](resources/dc35db62e697496aad5df675762adf65.png)  
*Note: for missclassified point, its y has opposite sign to its margin, leading to negative geometry margin*
They both have distance to supporting hyperplane  
![image45](resources/c818f17db699426e8bab870480a0f2f3.png)  
Inspired by the way that altering inequlity constraint into equlity one:  
![image46](resources/57a169c4561f425fa7575b12b0d7b4e6.png)
![image47](resources/663a0794efc5487a880b004d616e4725.png)  
By introducing a slack variables for each point, played as an offset so as to meet the support points constraint, i.e.
![image48](resources/4ec4c3de6b85492ba88fa6d55778c3a4.png)  
In other words, we pull all points on the wrong side of margin back to margin, and treat them as support points. Now we can solve it in the old way, plus with a new requirement that the separation must has as less missclassfied points as possible
![image49](resources/7abf355d43304c8580c5c0455bae0b8d.png)  
**Adaptation**  
![image50](resources/966ad7e4d6a64ad68acb7bb95f61e9f6.png)
![image51](resources/a6a3320e9f884f0889c599fae8f9ff8d.png)

![image52](resources/170fd254098240ea8a77f0bdd3de85fa.png)
![image53](resources/16bda5d3e54b4bfd940144271a3b3c43.png)

![image54](resources/f873e7ce0b934a738cae4df2aa5ec67f.png)
![image55](resources/590364e7deee4fd38049f3fc95c9cadd.png)
![image56](resources/ad12972e242748bc977dbad52ea9e6de.png)
![image57](resources/0c41af44bdbd4b8abb0d86d279336b87.png)
![image58](resources/67b09e6673de49d78e78272e4e8baf82.png)
![image59](resources/bc52d201165c4af8a5078f04d958f3a2.png)
![image60](resources/c656577fd7eb4a89bedb420cb9d10876.png)
![image61](resources/31d40714ed244bb88babed8c857a3d56.png)  
*data points satisfy the constraint forming support vectors*  
![image62](resources/21ee8afdf70c48b4a20cb5a06f04c848.png)

![image63](resources/33cb817832e046c7904ad5327288ab89.png)
![image64](resources/e7d01fe91f2e4d28b315934e23da5ec2.png)
![image65](resources/506862ba25934607affeafa27cc21851.png)
![image66](resources/cf7eac2a409145a2ab62a881f9dcf03b.png)
![image67](resources/784e9d0655bf4da9b59b1fb2d2fad217.png)
![image68](resources/b9853932e7024c9ba25d37df954b23e2.png)
![image69](resources/7448476e219343c5852ec6b935f6a32c.png)
![image70](resources/70c2f0e75072440a82588fe8ad8a3b4a.png)
![image71](resources/ca9be4b03f5b4e0fb2951c19740a5456.png)
![image72](resources/5c6b08583c064e08a09ad9cb801ebaf0.png)
![image73](resources/09f432c9319d49dfa9b5807dfd84eb41.png)

**Relation to logistic regression**  
1.  *Loss function*  
![image74](resources/ce53245452e246c79b4ec86faae004c0.png)
![image75](resources/47bf06f7141b43a1a6d09bf826134035.png)  
proof:  
![image76](resources/5f5974fc06a2481890f300e299ebed59.png)
![image77](resources/25e49ab886984557aeac43bf0df6410f.png)
![image78](resources/054f02070a4d481baebb09e4d77cd4fd.png)
![image79](resources/297abc8878274574b5370b8e830bcf8d.png)
![image80](resources/e28609e01b4147e6b91afb76894584ab.png)
![image81](resources/7ce9195c94d4452990a70e24f37c8f1c.png)
![image82](resources/df3277afa95941a3a4d31fd59f732da9.png)
![image83](resources/2b5f20d283a04bcf9505fdf6afb38f0e.png)  
*can be optimized by gradient descent*

*logistic regression's loss function*  
![image84](resources/da41802336bf47658cb2f9c9b40c5b80.png)
![image85](resources/74345651f0f8400681b0e517ce3f5c8e.png)
![image86](resources/25f0cfe7f60f4a339fa4062c8332e9f3.png)

![image87](resources/d240771721724680b22e71f440de31d5.png)  
*Both can be viewed as continuous approximations to the misclassification error.*
*And strongly weighted at points of misclassification, weighted less on points far*
*away from hyperplane.*
*Both has a similar form in draw line, but the former tends to give less loss when*
*correctly classified, and distribute 0 loss over margin bound, that's why it leads to*
*sparse solutions.*

**SVM for Regression**  
***Find Support Vectors : form a sparse solution***  
*Same as before, only a pile of data points on the margin (tube wrapping the predicted curve) will be at work when predicting new inputs*

![image88](resources/6ae39e3a416c44fcab5bd16bc5491abd.png)

*contribute nothing, only those points on the boundary of predicted curve's tube contribute to its adjustment (also, prediction for new inputs)*

*By introducing slack variables, support vectors will be formed by data points on the boundary of tube or outside the tube*

![image89](resources/3a1e32173bc84ebeb6729f88ff81ff45.png)
![image90](resources/8a93137f8a7f4d53b9646f724ff0aad6.png)
![image91](resources/752781472d0542a0ade1a60a0c9d82cf.png)

*add slack-variables for each data point*  
![image92](resources/1e202cba04434fe88173b574107f9595.png)
![image93](resources/bb0b20a258ff4984bdf5a1b103753261.png)
![image94](resources/d1222be341cd468aae22077589babdc8.png)
![image95](resources/9d3d9bfa49764ef1babfcc4a8e3c6297.png)
![image96](resources/6ec43b374e7f437397a0a4472aa1a77f.png)
![image97](resources/31bce237bbd8416aa730474049be369a.png)

*re-express error function*  
![image98](resources/c0cc8793dfd84440a56e560ebfeeeadb.png)

*by Lagrange multiplier*  
![image99](resources/78e1647ba27141859f2b6f53bc9c3e19.png)

*after derivativing*  
![image100](resources/f456723f6a1b4ab6a0cfc92382986058.png)
![image101](resources/c68d8b140179400ab18d33f26ff5c52a.png)

![image102](resources/607803eafccb4795978eda36e00665c2.png)
![image103](resources/7378d1b5bf974ef79759b1a767f41190.png)
![image104](resources/0872b5dbfe274acaa15efcc06c613ba8.png)
![image105](resources/b6e4c462fd044604bce615bf9ccb6879.png)  
*contribute nothing to prediction*  
![image106](resources/c29332980793470fba90c920b02f2642.png)
![image107](resources/7bc5ab445fd6490ca0fdafaa1a6e5e67.png)

data points lies above the upper boundary or lies in the upper

boundary contribute to prediction  
![image108](resources/a9292893f6074d56acfc97095f5d39a1.png)
![image109](resources/42de4482ead44f218584c0373bfb33ff.png)

data points lies above the lower boundary or lies in the lower

boundary contribute to prediction  
![image110](resources/f9b48950bfce4c07baf2ccd2a2850267.png)
![image111](resources/a17cbf6025c54561bab142b26f10fd17.png)
![image112](resources/368ecb6a59c540b0bc12d490a3e5d316.png)  
update b by data point on the boundary of tube.  
![image113](resources/a67a29a34ede488e8dc38257ee6575aa.png)
![image114](resources/d841c3a269084756a0d407cf30050160.png)
![image115](resources/d8448b1ef1e24bcfbf920b625eede876.png)
![image116](resources/284dae38a5774ab3a29f6dfcdf8533a7.png)
![image117](resources/aff6478326ec4f0a8826451e7ae97800.png)
![image118](resources/48d6150b41ba4896900120b0155cf5c5.png)  
So at every step, SMO choose two Lagrange multipliers to jointly optimize. After few rounds scan on data, all multipliers converge.

Note that two is the minimum number that fulfill the linear euality constraint.

3 components of SMO  
1.  an analytic method to solve for two Lagrange multipliers
• equality constraint in two multipliers

![image119](resources/ff0c3aab2ffa4e98abb59aa100740a8c.png)

![image120](resources/714a2b71386a4656b53881a4cdfab182.png)

*so one increase, the other one decrease*

*• objective function for two multipliers*

![image121](resources/2bb3249f3ab3417e8aecede566dbb070.png)

![image122](resources/c77582ef7beb43aa9efd81f1b6ba5149.png)

![image123](resources/153cbc905f78469e8f42a607536aaaa8.png)

![image124](resources/7b099581fb154e90b6c77407c35c7428.png)

![image125](resources/c0fe8ad3233f4421b2618b544406dac1.png)

• inequality constraint in two multipliers

after updating, multipler need do clip to fulfill inequality constraint

![image126](resources/6d62f3d4be2947ce8f9a82f794350f40.png)

![image127](resources/6e5464b1f6144607a97c06cf9d2b4000.png)

![image128](resources/342c5f61b55d4e9e902895895443a158.png)

![image129](resources/435a346281a148258fe70d08feb00c35.png)

![image130](resources/b5a0993435e0454c8fd5380b92c14b10.png)

![image131](resources/e62fa86540a046f48cf8ea7693cbdfb6.png)

![image132](resources/e75cf61323774e8897e69893efe6df95.png)

![image133](resources/403b4e167a1a439f974aad8aa29aa175.png)

![image134](resources/e0cf2fc139694094b1db0bdfccce0124.png)

2.  a heuristic for choosing which multipliers to optimize  
![image135](resources/6f669277bfc34b0cb45ed7c603bf4d35.png)

![image136](resources/2fa94f4f47d44d078ac6a6912db16093.png)

• first Lagrange multiplier

Data violates KKT condition prior to others for the first round

![image137](resources/46fd95089546455aaeef547f5ed6bc98.png)

• second Lagrange multiplier

![image138](resources/ff0cc495854a4a8789288f0d238e9872.png)

time consuming

![image139](resources/308033e755ce482bbf36408d03fbd642.png)

![image140](resources/8d7e524b9d5b4b79bef74e8847f0aa8d.png)

![image141](resources/1ab2a31b653e44bb8a9ea2f4e961fe60.png)

Hierarchical strategy for picking second multiplier when both multipliers share same input vector

3.  a method for computing b
select b such that the KKT conditions are satisfied for first and second examples

![image142](resources/bd57b4aa4ba845bfab8878a0ec69b39f.png)

under optimal value of two multipliers

![image143](resources/6f755d046df54131ba3e44bb5374b5ef.png)

![image144](resources/e2f8a38a42db473e912c72d74c889661.png)

![image145](resources/7d23d928a3024f7cbdcd1ab83a09f4c1.png)

![image146](resources/0d3f1118c58a4f99b6b19c665730d804.png)

![image147](resources/718d7522d6fd4c86a4b95241d8224653.png)

but now, we only have updated multipliers, not yet optimal, but we can have update share on b

![image148](resources/9ee5ba61a8b24b3ea47a210817f5f980.png)

![image149](resources/5c4dcccad5754eccb13323e5aa58d900.png)

![image150](resources/bf1097acadf443618a21124ce1135015.png)

![image151](resources/4b57c9fd0cae4c93ae2839a31a41867a.png)

![image152](resources/2dcef673655f45f38c3255000c4a3dd6.png)

![image153](resources/b8c7cbae54a748ee97ca67ee0ef3521f.png)

![image154](resources/8b958e36105746dea12d544e3e13a934.png)
