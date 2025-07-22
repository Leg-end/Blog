---
title: HMM&CTC
published: 2023-03-12
description: "Learning to predict sequentially"
tags: ["Markov Models"]
category: Generative-Models
draft: false
---

**Introduction**  

Real world processes -\> observable output -\> signal -\> characterized&modeled by signal models {Deterministic Model, Statistic Model(Parameteric Random Process)} determined by the properties and the way of describing properties of signal
Three fundamental problems for HMM design:
1.  Evaluation of probability of a sequence of observation given a specific HMM
2.  Determination of a best sequence of model (hidden)states
3.  Adjustment of model parameters so as to best account for the observed signal

Markov Models -\> Hidden Markov Models by extending observation(state in Markov Models) to a probabilistic function of state, from single stochastic process of state to double embed stochastic process of observation and underlying hidden state, the stochastic process of hidden state can only be observed through stochastic process of observation which is observable to outside world

Elements of HMM:
1.  ![image1](resources/5760927f6f7549818563d272a11ee475.png)
2.  ![image2](resources/6912bc0b06854aaa942dce5239e1f7da.png)
3.  ![image3](resources/9121f407ecdc423d951b73ba73735541.png)
4.  ![image4](resources/652466ef13964aab8bd9715760f8f97a.png)
5.  ![image5](resources/99056184c2374be2a4d78e170e63d000.png)
Notice! when N=M and each state uniquely associated with observation, then HMM degenerate to MM

Procedure of HMM:How observation sequence was generated
![image6](resources/1f78641aede24c819b2fd122d35f9615.png)
1.  ![image7](resources/4b22fdda21a44eeca39de807d858df0c.png)
2.  Set time t = 1
3.  ![image8](resources/6a38be5ec9a14e1793045df2b41a51aa.png)
4.  ![image9](resources/c8998223a9df4e25b28d76133bf3c505.png)
5.  Set time t += 1, return to step 3 if t \< T else end, T is length of observation sequence and total time passed
6.  ![image10](resources/9bd37398a6e6402eae93171a2cf0e163.png)

3 Basic problems for HMM:
![image11](resources/10ece1d5c2984dcc8975c8414ef7c768.png)
1.  ![image12](resources/f4a241067b2c41e6a50b5306c940df13.png)
2.  ![image13](resources/3f41ca24e0fc46af8c2103077ef99f21.png)
3.  ![image14](resources/ad801c1b6bb04711ac8bc86bc70b830b.png)

e.g. Speech Recognizer
When given training observation sequence set
1.  Segment each of the word training sequences into states according to Problem 2
2.  Find best model fit training set according to Problem 3
3.  Test new unknown observation sequence according to Problem 1

Solutions for 3 basic problems:
![image15](resources/d93bf0025e2c4d5eb1bfee9e22981783.png)
![image16](resources/c451b70195e64360bfcbdd4ad1a2d22c.png)

Solution for problem 1: sequence score
![image17](resources/f99f113f802b4c609c7f61bca00a8859.png)
![image18](resources/673b19d28b0a409e9dd1caaa56fcbad6.png)

Forward-Backward Algorithm
![image19](resources/90dd451e08224a97b0c3f1dbd5856847.png)
![image20](resources/263a5926135f4666b722b718ee17d99b.png)
![image21](resources/18cb6e45bdf949bc9e7a86d4fe379d22.png)
![image22](resources/4261e140f71f43e8b89bb7d1deea31ac.png)
Matrix form:
![image23](resources/eaf1461594eb44748b80adf8175b0ebf.png)

**By induction**  
Forward:
![image24](resources/4bc56aca70a24d629336a18758c37747.png)
![image25](resources/1455f40f890742d388aaf3fb8615c6cb.png)
![image26](resources/61c5ff8e94aa419b8d68e8a2ac6e4467.png)
![image27](resources/65958e1b598e4deb8b75e0a35ee1b988.png)
![image28](resources/6544f4e2e02443118f39e4dfc02cb163.png)
![image29](resources/5d9e20cade404e4abb34e9428cc1fa2f.png)
![image30](resources/4de4965790e04a7b9acd57890ed06bb9.png)
![image31](resources/0f385998bffc4d119e70cf77d602c53c.png)
![image32](resources/f715a89fcd14495393d74f3ee24cfa27.png)
Matrix form:
![image33](resources/8948514c77dc4265aeb2c79f1a8d1296.png)
![image34](resources/04107417ec144e75a5492a093e222748.png)
![image35](resources/cad6210058c64410953df86cfaa80797.png)

Backward:
![image36](resources/8fddef545a414c439d9d85c809087dcc.png)
![image37](resources/3682bf879e2d4d98b39b177bff96c2f8.png)
![image38](resources/0fa7c52a8d8d4eec9352819227e684b3.png)
![image39](resources/6a7c7930cbce41b1959f55e49059483c.png)
![image40](resources/ccf6bbb8172640b0bf3db99622a8df3a.png)
![image41](resources/ad02f091bbf142c79d5a91fc5632792a.png)
![image42](resources/026c15bda776491d81b34bd3f0f65a49.png)
![image43](resources/4bc5e846545f4f678dcb96282afb0b0e.png)
Matrix form:
![image44](resources/333ac1d4d70f4d5e9d823e6446d1e5d9.png)

Solution for problem 2:  
**Maxlikelihood**  
![image45](resources/d220c4f4763c4db5a24e38ac0c76d3ac.png)
![image46](resources/d17ac83a22d147c286f279b7630544d4.png)
![image47](resources/0d10ff4eabdb421faf5052b0d4270711.png)
According to solution of problem 1
![image48](resources/2d2c3b0d47a943b6906d26123ad266b7.png)
![image49](resources/41f690dae13c4921b4477fe11f69f57a.png)
![image50](resources/7773bd28b8ca46558ebe40ec367003c3.png)
![image51](resources/564c1f12ee2c475aabc674c22c931395.png)
![image52](resources/247458e4f2ad42c688c2bbdad1e530be.png)
![image53](resources/27a8fde2559a43659edee88babf13a7c.png)
![image54](resources/de8f4c0755dd4706b046301022d19be8.png)

![image55](resources/9ed46ff57b6b48e389d659420ad95ad5.png)
![image56](resources/bc623d5a093f4b1b93f0df92ef650eb6.png)
If we take such greedy strategy at each t, the resulting state path may not be the optimal state sequence,
![image57](resources/5856534672ee434daee002f65d7f2b84.png)
Since it misses the detail: (1) global structure, is it a resonable generation process ?
\(2\) condition on neighbor state

\(3\) the length of observable sequence may not always be T

To get most likely states sequence, we need to find out the desired state path that
![image58](resources/656783fffc9a45828b2826cd5f354884.png)
![image59](resources/ff828ec824df4934bf3ecf8fb27785f6.png)
![image60](resources/9ca61a428b654c89bd911dd626681d05.png)

**Viterbi Algorithm**  
Base on the simple idea: state at t condition on maxlikeli state at t - 1, similar to forward algorithm
![image61](resources/3e3c9f485e0b419b8d136d72d63483bc.png)
**By Induction**  
![image62](resources/8dcb32b2ff9d468fb17ab753f9bc6fdb.png)
![image63](resources/6cda6099373b40369ec1dfebd5b6a865.png)
![image64](resources/0e42226132fe4cbcb8ee89745f734e7c.png)
![image65](resources/cbae7e7fb2d243829d67bac909a5b9eb.png)

![image66](resources/51dc4a46d2d24c0b94b610bdd2b9c063.png)
![image28](resources/6544f4e2e02443118f39e4dfc02cb163.png)
![image67](resources/4f9cec5c24b3461986f907c752fdae31.png)

![image68](resources/eddc0ad738fd4947b1834460652cbeec.png)
*…*
![image69](resources/b1db3d128763469aaf30c457b2a4f893.png)
![image70](resources/10286c57d7df451093a74e89b35de8e9.png)

![image71](resources/7ad66b30faff4b5c9c26aa170b2845ac.png)
![image72](resources/085ec1d920c1432a98c7b9c26cd30763.png)
![image73](resources/144953fbd4de4e82ac4892b9ce780da7.png)

Solution for problem 3:
![image74](resources/d99169122d96405b948954f7309fc1c9.png)
![image75](resources/0049698535a14bb284f88a6671aadc21.png)
![image76](resources/f6b0d0f3f7ec4d94bfe220e0ec1214f0.png)
![image77](resources/3c4024d6719847608eb256725e70a0ba.png)
![image78](resources/e4ad6d8886cd4981869587a49c8aae06.png)
![image79](resources/3cfaf030eae5401a8f43ce47c1d27ace.png)
![image80](resources/0e249b432c464e2d9c05bff4929bfa9c.png)
![image81](resources/ace3abff1b394dc386d7b480c0abb798.png)

![image82](resources/885fdc90a0704d4d87f89808f446f0de.png)

![image83](resources/5392b9771dec4ecf94b0b0aff85b4b77.png)
![image84](resources/7942ec9c71ff418790ec0b554f711dc7.png)
![image85](resources/86b4b4fbf51c47b9b26cf8113ee7d7b1.png)

![image86](resources/61fc3b7ff3b54b698be2999dde331d7b.png)

![image87](resources/457f4ab38cbb4db7954189f72f0063ee.png)
![image88](resources/3f31250f0330496cbdddee8b8f9d1064.png)
![image89](resources/bd2ef088614248769fcb75da222b8886.png)

![image90](resources/12890f68c0e44120a4f52d6e0bee345f.png)

![image91](resources/e6cf0050239949369c99aca0c5d61291.png)

![image92](resources/747f8051346e4f1bbb66b4289d2b7a86.png)

[CTC](https://distill.pub/2017/ctc/)  
**Introduction**  
Fundamental problems for CTC
1.  How to align input sequence with label sequence (auto-segment and repeat)
2.  How to find the most likely label sequence
3.  How to train CTC networks(calculation of gradient)

Basic idea: Interpret the network outputs as a probability distribution over all label sequences, conditioned on a given input sequence

Definition:
![image93](resources/60e5f89ca4b645ce8ba37f2af3686d1f.png)
![image94](resources/4f65b0a08a534f34a6a2388fcedac0e7.png)
![image95](resources/f3ea6cabef9f44b18a5c6b3437a12d56.png)
![image96](resources/860cb2e7953a428aacf2c959e74547a2.png)
![image97](resources/f8ca5a4c565546dfa0fe5d71f9e6d0e1.png)

[Solution to problem 1](https://distill.pub/2017/ctc/):
By introducing the prediction for "blank", model can automatically segment label sequence
![image98](resources/38e9493a35c44113958f9ad9005e1044.png)
Also, alignment can be done by combining repetition of character at the same time, but only same characters with blank in middle will be kept when inference, those without it will be deduplicated
![image99](resources/bb4bb16e25834566a400d1e47d953ed0.png)

![image100](resources/41269bcecd764a57807e89f3f54a0a03.png)
![image101](resources/2bd3f3c8cdf04545874e731d7a2be9a5.png)
![image102](resources/acad48e8f0474a4b905e4f4104a04a49.png)
![image103](resources/59bf4430c8834e9eb4a1d42d12d5f24a.png)
![image104](resources/6c7cf3d4b99d44df8c349b837c51e2c1.png)

![image105](resources/1528cd074e734f9bacff2a78a64cd611.png)

![image106](resources/5300bc20d8fc4455a14007c95e15b49f.png)

Solution to problem 2(decoding):
Base on solution 1, each label sequences may corresponding to multiple aligning sequences
aligning sequences → original label sequence
![image107](resources/4fd29385599948978f31d0e0fd8c6f7b.png)
![image108](resources/5bd782cd96a8494b8fe3d9a02232adaf.png)  
We want to find the **desired temporal classifier**  
![image109](resources/df6cc0ecb4f244a9b580a4a657930a3d.png)
![image110](resources/dfb9e33df96c4dc2a4640a1f7604d9a5.png)
Method 1:
Assume that the most probable path will correspond to most probable labelling
![image111](resources/7f78ea199f9f4ece90e9aa3db26be469.png)
Since there are multiple alignments equivalent to target label, it is not guaranteed to find the most probable labelling
![image112](resources/bf051916d2d3414cb4c20bb356dcee32.png)
![image113](resources/7101cd2e256348748162ea0467cad1d9.png)
Luckily, most of the probability mass is alloted to single alignment, so method 1 is works well at most cases.
Method 2:
Prefix Search Decoding
The total probability is split recursively depth by depth
![image114](resources/9f31009af4814d08873a843a351bfbfa.png)
Modifying forward-backward algorithm
Our target is to maximize probability of target label sequence which is equal to maximize summation of probabilities of all its aligned path.
![image115](resources/4f0b48491de0490d9c9d225b63bff321.png)
At each time step, merging path with same output, that yieds the following graph
![image116](resources/319e41ae34aa4e93970feb5caab768ab.png)
Actually, it is a modification of network outputs
![image117](resources/cac0dee020844bf9b161d5da1115de0d.png)
Initialization
![image118](resources/e9509fa55406428296660d1e35ed5797.png)
![image119](resources/d8593e319c5940a8acf34da1b74817dc.png)
![image120](resources/a9119f58dc6a463db8c85452fb26d7bc.png)
![image121](resources/690062f3ad834f69ae3a33258560faf9.png)
![image122](resources/a310acd30f2a4881b1e25361e84de5bf.png)
By induction
![image64](resources/0e42226132fe4cbcb8ee89745f734e7c.png)
![image123](resources/b452cfe32a31463b84fe8f2f76bb1d3a.png)

![image124](resources/03bcea662ba94878bbdc84b7db33de29.png)

![image125](resources/c3fdc20bd01242269678cb045bea2b6c.png)
![image28](resources/6544f4e2e02443118f39e4dfc02cb163.png)
![image126](resources/969a6c498c3e411c85cf040a4e492521.png)

![image127](resources/6e229b158950438abe5a735c475796c3.png)

![image128](resources/b2290acd1c044509b4c23f6dccafc290.png)

![image129](resources/4d91b0327e2744e790285c374e7e40fa.png)
*…*
![image130](resources/d41d024894434c61a7daa812fdbea0f8.png)
![image131](resources/5168817a4ce04b4b8eb2d1619b164727.png)

![image132](resources/f7076c4a691d4e11998077e048bc0116.png)
*that yields*
![image133](resources/2f23645449e44e4b9a04d025ba5663a4.png)

*where*

![image134](resources/847d246798a64bf0a7cf7c8ee8a8f894.png)
![image135](resources/93a6ea73909d49b29ae1c5acb43f33c8.png)

In case of underflow problem, normalization is applied at each time step
![image136](resources/4212837042a44c68aef2ad9c9db9e0a1.png)
![image137](resources/708f179e8d4146ce9f1abcff9a696564.png)
![image138](resources/61af48715bf54835a0d280115a918e46.png)
![image139](resources/cc3854a1413d421aac711d0993c37490.png)
![image140](resources/05701957722f4571942b87e45661db3f.png)
![image141](resources/a5bd594a511f49689013a562d5051e55.png)
*…*
![image142](resources/84d78054b4d148b5bf79c7f20a77ab00.png)
![image143](resources/71f66e4186f444e4ad40dc9bbd2ad231.png)
![image130](resources/d41d024894434c61a7daa812fdbea0f8.png)
![image144](resources/712cc969e7a64a42aef77b298f781812.png)
*that yieds*
![image145](resources/2b4c24acc32843569c263a678833a55a.png)

![image146](resources/653393c2384c489f832784e260e87729.png)
![image147](resources/c0165e5e43cf47579368d747c3d2185a.png)
![image148](resources/be758aa2478a4deba00acc0ee6724ca1.png)
By induction
![image39](resources/6a7c7930cbce41b1959f55e49059483c.png)
![image149](resources/d3e51265bf6a4eb9b56931099a011dda.png)

![image150](resources/1860a4501f154cd48e2c1ff929cc85e5.png)

![image151](resources/d4efca3952b14f77abc1bc2196a3c327.png)
![image142](resources/84d78054b4d148b5bf79c7f20a77ab00.png)
![image152](resources/db4cc0f8eef04f2ab056966cdaa8d22e.png)

![image153](resources/e5cd705e921842e88de8a255f0eddcd7.png)

![image154](resources/630afa2931c941d7a04713da8b4fc15e.png)

![image155](resources/a9b04e921bb3498790d72742a07a7784.png)

![image156](resources/d35a6e04c0ea471a9fe4efa1b9811dc5.png)
*…*
![image138](resources/61af48715bf54835a0d280115a918e46.png)
![image157](resources/874df6800b70487483d5b0c182968ed9.png)

![image158](resources/cd6fc9c3e8974e3ea88c3fe3e46bd7bb.png)
*that yields*
![image159](resources/983cdd0107dc473b81eab506aa816d0e.png)

*where*

![image160](resources/a59af40814ee490981cb0c1dd02cdb65.png)

In case of underflow problem, normalization is applied at each time step
![image161](resources/8e47f9488168469387856bed9555f2c6.png)
![image130](resources/d41d024894434c61a7daa812fdbea0f8.png)
![image162](resources/3032062c2e9d435d893e88a5b3bc0f1f.png)
![image41](resources/ad02f091bbf142c79d5a91fc5632792a.png)
![image163](resources/ad645b1d06d74331b7046dd2370548d3.png)
*…*
![image140](resources/05701957722f4571942b87e45661db3f.png)
![image164](resources/c31cd0354f2a412aa64d0aca411e9334.png)
![image64](resources/0e42226132fe4cbcb8ee89745f734e7c.png)
![image165](resources/c15f25158c5e40dcb31352ade8366996.png)
*that yields*
![image166](resources/c2cae22dcfb8485c827aa5ce9c357c9e.png)

Solution to problem 3:
From the principle of maxium likelihood
![image167](resources/4edca1f3bc1741e9b1559a9624b29139.png)
![image168](resources/750cfa9aa2394d40bbd8075a315f158c.png)
![image169](resources/ec7b9e865ecb4e5a96bcd71c3296caaa.png)
![image170](resources/9e427908a6534196afadae66ae7091f5.png)
![image171](resources/be7f3f63e3d14af6b7000c618e0cd211.png)
![image172](resources/bcb64d6dd6384eb3ae525d1d4245f6e0.png)

![image173](resources/b3116d07b26f4731a7286a1336d91eb4.png)
![image174](resources/9be56fbe4ba44b0791df451f7d70f006.png)
![image175](resources/0466ed215ae2420eb28a70f56e581252.png)
![image176](resources/b5a3c8c3e9c94034a877777097e47397.png)
replaced with normalized forward backward
![image177](resources/1392eb76ba9445ee8cf73fbd3ebbddfc.png)
![image178](resources/be980b6fc9464493bcc88b13d9b179e3.png)
