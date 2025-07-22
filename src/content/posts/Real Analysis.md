---
title: Real Analysis
published: 2023-10-05
description: "Build Real space from scratch"
tags: ["Set", "Natural Number", "Ratio Number", "Real Number"]
category: Top-Design
draft: false
---

**Start Over: Redefinition of Number System**  
It's important to axiomatically define Number System, instead of constructing them.
i.e. we don’t create their physical image or any essence they should connect to the real world, like, what are they made of? are they attachment to physical conception ?
We extract them from the natural world and generalize them to an abstract form by only describing properties and operations related.
As the old quote goes: one is the child of the divine law, after one come two, after two come three, after three come all things. So we can define any complex derivative from its simple origin
The process of redefinition of number system is to slowly fill every spot on the number axis

![image1](resources/4e05b9e3dfa64cf787874d4bfd56d0c6.png)
![image2](resources/81876968cfed419782a96e4b35d38305.png)
![image3](resources/a6e5fc32ca6e4875b35f96806602ea57.png)
![image4](resources/edf3f40c54b7429c836120999d6c20d7.png)
![image5](resources/a254571799bd4884bef88fee27b8d034.png)

![image6](resources/323f617d99164bf195f1ead01368f22c.png)  
n is result after recursively applying increment on 0

![image7](resources/d86da7f1e1b74d9e9e5d4e9c03518dd4.png)

![image8](resources/e438d478161e440bb38d2ef909c5abec.png)
![image9](resources/fead556b7b1f4d2ba191d9cad855c82a.png)

![image10](resources/46822310fad24fd7b0cf54b2c97fe9fc.png)
![image11](resources/c8558ecd358e4c349b51fa607b0807e4.png)

![image12](resources/de696ea460824fc99a368479f6f17231.png)
![image13](resources/f850b43ad9d74ae394f65df208dd431a.png)
![image14](resources/d37b0cddd1bf4889817654c3b8593532.png)  
So we need to exclude numbers violating properties of natural numbers

![image15](resources/2a7f3a326e5a43ccb98a025ca739a9f7.png)  
All natural numbers have their properties **consistently followed** with 0(its predecessor)

![image16](resources/a21f4be285dc465380fe3dbc0456d5d3.png)

![image17](resources/7144fd8d0dc84d9e900f509f1c304efc.png)

![image18](resources/d3714aa42c30477a8a256960bbec7d95.png)

![image19](resources/c3bc726075a04e9b8deb2c7c2bb7917f.png)

**Addition of Natural Number**  
Base on axioms 1 to 5, we now can recursively define sequence
![image20](resources/ded9f7b6fee140e4a7e487457d2a5a93.png)

![image21](resources/69f7384eddca471696b705c73396be8e.png)

![image22](resources/092c56cfa80d436184f93a9538559fcc.png)  
Definition of addition has same form as induction (Peano axiom 5)
![image23](resources/9f5f636da05b4c439b217e1d62dff7a5.png)  
Properties : All can be proved by following the same pattern as Induction
\(1\) commutative law
![image24](resources/ca1e3f5f976244cb812e4c4cf70622a0.png)

Informal Proof

![image25](resources/5d8c4b81935140eb8310e795f26bdb54.png)

![image26](resources/79f08d0d4e6e40c38869c080b6dff239.png)

![image27](resources/cd1877f8115740fb86c913ad8da32dff.png)

![image28](resources/3f8505dab8e94be8bb592c46c851b962.png)

![image29](resources/75997a68895740d69704dcf8b01b09e7.png)  
\(2\) associative law
![image30](resources/b2300c999ea14c5fb9136d2e6b44104b.png)  
\(3\) elimination law
![image31](resources/2bc37de1d5d5447ebe2250989ab02ec8.png)  
Order built on addition
![image32](resources/0e1032979e5b4c93b8612c64de8c2e61.png)

![image33](resources/9d26a3b5de8743a2ad513a6a0be49028.png)  
Note that order is a shared property among entities
i.e. an entity can be ordered only when it can be bounded by other entities
For Natural Number, we can find that:
![image34](resources/59bfe8952d5c48a18cc7c6eb61ebd327.png)
![image35](resources/022471fa096b4d67a69915741b90825c.png)  
So it is for the order definition in Integer, proportional number and real number, their order all build on in such way.

Order + Peano axiom 5 = Strong Induction
![image36](resources/51fb0dcde3c047bd896619c9d996e9f6.png)  
e.g. converge of series
![image37](resources/d41e7ec7ac4b4cff904eb6066efac4d8.png)
![image38](resources/7e1c1a7c018a4b8da231c84112391631.png)

**Multiplication of Natural Number**  
Follow the same thoughts as did in defining addition, we can define multiplication
![image39](resources/35243eb8860e4e59b95c7e4c9084ee48.png)
Properties :
\(1\) commutative law
![image40](resources/1aacbae926cc49f6adc239b2ab270836.png)

Informal Proof

![image41](resources/6f2dda278ffc42f8afb9099c6f426d6f.png)

![image42](resources/833687aac6944fa9a0923abc7e8caeb8.png)

![image43](resources/cf86fa1e844241b08d6572d7ab0eb435.png)

![image44](resources/653ef1e740584b9d822a56b9cb5fae5f.png)

![image45](resources/846941c474c0431aa451f39e19ed2630.png)  
\(2\) distributive law
![image46](resources/bee47e509bb543e4925183752710a168.png)  
\(3\) associative law
![image47](resources/30706e01050843bf805f5bd73d7baf4c.png)  
\(4\) order preservation
![image48](resources/aa71d92a3fd34508b8834504581dcfc7.png)  
\(5\) elimination law
![image49](resources/6e57b0845f234a79aaa0c00e7c47c9c4.png)  
**Euclidean Algorithm**: represent number with combination of addition and multiplication  
![image50](resources/8ff8b0f729cb47509c8dcc57852d25b0.png)

![image51](resources/3050cec55ab2459ebb4fb3aaf151b4c4.png)  
**Exponential Operation** of Natural Number  
![image52](resources/e6fdf76ed57e498388e813961ca2dff5.png)

**Set**  
We now can generalize the **natural number set** into more abstract one  
![image53](resources/f86678fbd00f4bfc806a01912aebd3d8.png)  
Axioms of equality on class T
\(1\) reflexive
![image54](resources/bdd1eab94c664132a37712528c8aed5a.png)  
\(2\) symmetric
![image55](resources/c2ef847a632b4489a8afd4e56577f44f.png)  
\(3\) transitive
![image56](resources/2d14a6500b0e4332aa44a748843988dd.png)  
\(4\) substitutive
![image57](resources/552da467bd3c41ed9a23f6eee867f673.png)

![image58](resources/7e5a0fec9e8a44a0a44f3351e393862f.png)  
**Zermelo-Fraenkel axiom 1**: identity of set  
![image59](resources/53be641e0d4c4b699d71279a2238bcea.png)

![image60](resources/ae07e4ba64fd402f9c89692c1e5c1e6f.png)

Note: That means set itself can be an element of another set

![image61](resources/c9a1a27232344aa2bbfc9b54dcd21b6f.png)

![image62](resources/b5d1540a18234c41ad5102dd62e360d6.png)

![image63](resources/3bb5b6ffbc32477bad2ce867c7074091.png)  
**Why? Operation following substitutive is a successfully defined one**  

**Zermelo-Fraenkel axiom 2**: origin of a set, empty set  
Any set exist at the contrast to empty set

![image64](resources/52e2195f3ba743c7830b472db71cb4af.png)

**Zermelo-Fraenkel axiom 3**: basic unique sets, for constructing bigger set  
![image65](resources/f38528d54f3849618508b23ec83d0aba.png)

![image66](resources/2581f624074f42bbbcc7c1932d55695d.png)

**Zermelo-Fraenkel axiom 4**: Dual Union operation, method for constructing bigger set
![image67](resources/298a549129cc4b60b2b9eada9745bf98.png)

![image68](resources/2f32acd05d704b0ca1d2c58a542af986.png)

**And it follows substitutive**  

![image69](resources/8523a727733c4d49b7f7ece0ce9b0d84.png)

![image70](resources/d838878d477d44cbb5e8aac9816ebb2b.png)

\(1\) commutative ; (2) associative ;

**Subset** can be derived from Dual Union operation  

![image71](resources/188f6f9da1f64fcd82ccdd4a7de4aac5.png)

![image72](resources/b291098e24fc45c38f7411d85bd19f0a.png)

Subset implicates relationship of **order**  

![image73](resources/531f3dd7d8ad48cc94e7723b6686eb12.png)

**Zermelo-Fraenkel axiom 5: Separation axiom,** constructing subset from a big set  
![image74](resources/15b1907b6b7f48a6b6939a129f61fb15.png)

![image75](resources/c5dcd138a1594c5ba4363074cf61264a.png)

![image76](resources/7f2662c935534afd97a41ce7ddd7268e.png)

We can use it to define **Intersection** and **Difference**  

![image77](resources/6e7fd235f22b43caacf406553f154c2c.png)

![image78](resources/7bfaa95842364ef593e8d6755b10d3d9.png)

![image79](resources/e7c1a37241c54cb5aa8cc891c895e599.png)

![image80](resources/9de3c4c389e340cf9487194158a1bb36.png)

![image81](resources/7d25f83fa1c0486181b5d55f300f8be7.png)

![image82](resources/8b0a04cab4454d88ae69682fa65d193e.png)

![image83](resources/d9c8a8784b99426bb773ebca62731e62.png)

But for now, we are only circle around inside a set, to jump out of a set into another form of set, we need more powerful axiom

**Zermelo-Fraenkel axiom 6: Replacement axiom**  
![image84](resources/45bbc073cf3b46ab9b64057b63e4b505.png)

![image85](resources/f83e7dd3971e42feaad85cb10adb7690.png)

We use **Separation axiom** to tease out subset and transform its elements into new form by **Replacement axiom**  

Connection between Replacement and Separation

**Replacement axiom** can be seen as **Separation axiom** of Set y belong to

![image86](resources/be8024035b32429fb2186bcfa79d09d0.png)

**Zermelo-Fraenkel axiom 7: Infinite Set, Specialize to Natural Number Set**  
![image87](resources/9ec88a5e2e5142d89b88279551097210.png)

Actually, axiom 1 to 7 can generalize to a generalization of Separation Axiom

**Zermelo-Fraenkel axiom 8: axiom comprehension, Universal Separation axiom**  
![image88](resources/7bc7718181f64aa3a833df2f0ea86e3d.png)
Russell Paradox: Axiom 8 failed under such property
![image89](resources/16b17c6f1dd74b7c995ac4823927b183.png)

Proof:

![image90](resources/a7b99ff4bdfd42d5a3536fad95232450.png)

![image91](resources/077bc9152acd4b18987e8796f853662c.png)

![image92](resources/78a9db2015134524bf580ce9c20267a0.png)

![image93](resources/55fc56a4c93e4265bba5f2288d4f3d45.png)

**Zermelo-Fraenkel axiom 9: foundation axiom, regularity, patch for axiom 8**  
![image94](resources/3c02efdae66240b4a4736ad01756c98e.png)

Now function can be defined as mapping between sets
![image95](resources/559ed1e3cc1e4380a7e59102bcfc8294.png)
And Again!, it has to follow the **law of substitutive**  
![image96](resources/4cec54b0d16e41d780e35aa8618f3b46.png)

![image97](resources/44e81b58fee44c9bb94aa8374d2e8da6.png)

![image98](resources/7f3b5d46da67443998a05054958f3d73.png)
Properties of function can be derived from axioms of set
\(1\) equality
![image99](resources/745482b3d1334c7882904a60cf894057.png)
\(2\) compound
![image100](resources/3a2397ee950b4ebe827e06af26f52be8.png)

![image101](resources/ea22fbbc8a5943db9f0ef15d416c87f1.png)
\(3\) injective
![image102](resources/a89d313863e646dcb9a54d7c639ed105.png)
\(4\) surjective
![image103](resources/3fa651fbb49e4820ac93bdbc7ad031c6.png)
\(5\) bijective = injective & surjective
![image104](resources/d9e6d3b3ac084f94ad4bc81d0b437dcd.png)

**How big is a Set**:  
Cardinal of set is defined by a bijective function(it's similar to count number from 1 to n)
![image105](resources/5a1120160e8145e69cd9752b08af0ae7.png)

![image106](resources/5dcaab7fce054deb80dd8281adcca29a.png)

![image107](resources/ed228f9b6f7643d6b595fc81ced34030.png)

![image108](resources/5e74d6c0190d4a55918a97b0c3f9914d.png)

![image109](resources/64ff45091f40424889b5c08bf1b9f684.png)
Equality of Cardinal
![image110](resources/8283ee1efadd4ad69260717e82944aa2.png)

![image111](resources/07191f25c1ef47d7986ed1a99ebfda59.png)

![image112](resources/26566ffd34494662b30177d14cbc1568.png)

**Zermelo-Fraenkel axiom 10: power set, set of functions**  
![image113](resources/6923702b2ac04ff091d413e68fcb72f8.png)

![image114](resources/0fe54cd94f57477ebde6a74cd7e2b27f.png)

**Zermelo-Fraenkel axiom 11: Union, for constructing way larger set**  
![image115](resources/049f9558e4234a2884047c6a6d17b033.png)

![image116](resources/c1c7f4eb174942b287b9d12ecbe2ece6.png)

**Integer Set**  
Integer is a generalization of Natural Number, as subtraction result between two natural numbers  
![image117](resources/3f4b5af3dcd144e8b2e465def5368db4.png)

— is a placeholder for subtraction, since subtraction result directly on natural number is problematic--they can not represent as natural number, so it can only be defined on integer.

And we can not define subtraction between integers without firstly declaring it, which is subtraction result between natural numbers. In case of recurrent definition, a placeholder is needed.

Now our simple idea is to define Integer as an analogy to natural number with all the axioms and operations we already testified
\(1\) identity (equality), follow substitutive  
![image118](resources/11d4768a716e40ffb19e17eda3c76d90.png)  
\(2\) addition, follow substitutive  
![image119](resources/df65ed426eab465f853e5461fc6fc3f4.png)  
\(3\) multiplication, follow substitutive  
![image120](resources/e004a6ab066d4dafaf5f291796f81091.png)  
\(4\) negative, follow substitutive  
![image121](resources/102650c1a1674217a13b561024d6b5c2.png)  
\(5\) trichofomy, if and only one holds  
![image122](resources/33a6daddae60401eba038c896ab01a36.png)

![image123](resources/6b57082e406d4655a6c61dd43d456ba5.png)  
\(6\) base on definition of **negative**, now we can define subtraction between integers  
![image124](resources/2b40d5f2a743401891d472129da83dfd.png)  

![image125](resources/71c626c590d0498bbb4c4bb4c406dabb.png)

Generalization of Natural Number  
Order, we can redefine order with subtraction

![image126](resources/73d9740e3c504b4abf40e86b90e9af28.png)

order preservation with negative operation

![image127](resources/009e52e42d5541fd9c18a2246a4f5c25.png)

Integer fill symmetric part for Natural Number on the left side of 0 by subtraction
Now any property of natural number is compatible with integer, so any natural number is a integer, we complete the construction of integer(added with subtraction)

**Proportional Number Set**  
Proportional Number is a generalization of Integer, as division result between two Integers  
![image128](resources/691371a85e124e0d80108734ffb1d5a6.png)

// is a placeholder for division, since definition of division base on definition of Proportional number.

And we can not define division between proportional numbers without firstly declaring it, which is division result between integers. In case of recurrent definition, a placeholder is needed.
Now our simple idea is to define Proportional number as an analogy to Integer with all the axioms and operations we already testified
\(1\) identity (equality), follow substitutive  
![image129](resources/96f3598b4d4c4a13b0454a537e2fafde.png)  
\(2\) addition, follow substitutive  
![image130](resources/e0a84b43c2e44996a793a82963848e9d.png)  
\(3\) multiplication, follow substitutive  
![image131](resources/6b1ee9e3cb134a56b977458645fe37a0.png)  
\(4\) negative, follow substitutive  
![image132](resources/794c8cc80f8e4ba7bf35f5b8b9cd4e17.png)  
\(5\) inverse, follow substitutive  
![image133](resources/be6b2509ec0e4c34821b8f88b251bfed.png)

![image134](resources/6a430e8e60494ed68620a6b7a1e3245e.png)  
\(6\) base on definition of **inverse**, now we can define division between proportional numbers  
![image135](resources/fa67d72e49884e57ac7ed31b7c54632e.png)

![image136](resources/8d19a3029bf34537b82c0060b97e3e5b.png)

![image137](resources/55d1f65627244cddb55e42eb2d334d1b.png)  
\(7\) trichofomy, if and only one holds  
![image138](resources/b496adb498584ad9b9ebecb8b80a6db4.png)

![image139](resources/76b8ddda936248fab2951775a9481b54.png)  
\(8\) absolute value can be built upon negative operation  
![image140](resources/285fc271e8144a138b86354699150a85.png)

![image141](resources/407dc18c569149bfb275005bfe86cb53.png)  
Distance can be built upon absolute operation and subtraction  
![image142](resources/6e878ec5666344fea2c413a249c0ec0a.png)  
It can be used to measure how close are two proportional numbers  
![image143](resources/ac06a8aee2e041e5a1380747be77f6d0.png)
![image144](resources/585610895a334cfc94483690f477177d.png)

Generalization of Integer  
![image145](resources/2fb3c087792949f88d2e1fa5f8086a88.png)

exponential operation

![image146](resources/7b1751241534437a8b14b909c2a124e5.png)

order preservation with exponential operation

![image147](resources/b9b353bb271f42b395b88875d2f4d4f1.png)  
Now any property of integer is compatible with proportional number, so any integer is a proportional number, we complete the construction of proportional number(added with division and absolute operation)

Any two Integers are separated by a proportional number

![image148](resources/ed5d4a230ab44e0b83abbe4eddef5caf.png)

There's huge empty space between two integers, proportional number fill it by division

Any two proportional numbers are separated by a proportional number

![image149](resources/3a8fa9cd0e83487b8c160f07acc8d23e.png)

**Is there exist empty space between two proportional numbers** ?  

Void between proportional numbers  
![image150](resources/330c6e406449456b85816295682a51d3.png)
Proof:
![image151](resources/d6631b38a9c4451abadd22d87bdc11a9.png)

![image152](resources/dded1144dd044c67868d33e648ddd4a9.png)

![image153](resources/231c7bd062d7408eb60256f4de90e055.png)

But a sequence infinitely decreasing is not exist, since we can always have

![image154](resources/9018fe9485b54fa8b62399fd6e30ec97.png)

![image155](resources/26bae547d922414abf2bafc8ce7ce82d.png)

![image156](resources/1c67f8b383f544bba98ac35d63cb2f4f.png)

![image157](resources/afed232a424a4ff8b7e00f12212d1b1c.png)

![image158](resources/9c85445bf62a4988a819b5a79b25923a.png)

**Real Number Set**  
**An instance of complete measure space, the idea behind generalization from Proportional Number to Real Number will be useful when defining a Hilbert Space**  
Real Number is a generalization of Proportional Number, as a limit of a **Cauchy sequence** on Proportional Number
Sequence  
![image159](resources/b98a9616ecc94d85849e31a636172f86.png)  
Bounded Sequence  
![image160](resources/965cdeb5c3ef474c8d10270e41186704.png)
![image161](resources/6a3a7c0583ef40a3a58f39d98f925ee8.png)
![image162](resources/dd5232697efc433a9ef1d4ea23e54501.png)
![image163](resources/4483fc68cdab4073a0270cefadef0c06.png)
![image164](resources/fd2f03836f9c4ebd86bfbd70f7841f9e.png)

Obviously, Cauchy Sequence is also a Bounded Sequence
Limit of Cauchy Sequence
![image165](resources/933dc61f455d46b695fc4b1170bd4111.png)

![image166](resources/7af11521e81a4ec7ad173ba5b816160a.png)

And we can not define Limit of real number without firstly declaring it, which is limit of a real number sequence. In case of recurrent definition, a placeholder is needed.  
Now our simple idea is to define Real Number as an analogy to Proportional one with all the axioms and operations we've been already testified  
![image167](resources/32c159d943c348e8b23158c23c8d45f9.png)  
\(1\) identity (equality) of Cauchy Sequence, follow substitutive  
![image168](resources/d5e6ef7d7bb6443c931492c15db7fb7a.png)

![image169](resources/908810fb9cfa478ca2725b27d5734078.png)

![image170](resources/7265570becd84808852be67b1b687d9e.png)  
\(2\) addition, follow substitutive  
![image171](resources/0aff8698d06f45ada82f57cc752e2f82.png)  
\(3\) multiplication, follow substitutive  
![image172](resources/e466db707779497988b41226badb2e4b.png)  
\(4\) negative, follow substitutive  
![image173](resources/496222c913d3483c9d785041d490a2c1.png)  
\(5\) subtraction, follow substitutive  
![image174](resources/14fa759c9473414699a93a5f6dff748a.png)  
\(5\) inverse, follow substitutive  
Constraint away from 0

![image175](resources/71b2246bb9e5452fa58b0d224c9b341f.png)

![image176](resources/9e7069dc4bbf4a6499a2abfc1f97d1cc.png)

For detailed proof please refer to **"Tao Real Analysis" 5.3.14**  

![image177](resources/205558307c11438e874db83554865d45.png)  
\(6\) division, follow substitutive  
![image178](resources/403bdaf595fb491195cb3f7d2049bed1.png)  
\(7\) trichofomy, if and only one holds  
But first, we need to constraint sequence positive or negative away from 0

We can always extract sub sequence constraint away from 0

![image179](resources/883d7c4b1d7c4d2ab94d5e7101776c10.png)

![image180](resources/ab4fc0a2ba694c4bbf744d88b04834d7.png)

Now we can inherent the rest of operations and properties from proportional number without changes  
(8\*) **completeness**  
A complete closed set has its Cauchy sequence and limits inside the set

e.g.

positive real number set is an uncomplete open set

![image181](resources/438a6f7aaac74d80bf3f909f97b8d636.png)

Non-Negative real number set is an complete closed set

![image182](resources/7dea651041214bd9a092730ed08c2770.png)

Inference

![image183](resources/341624bb783340a2b987e66dd5439bea.png)

![image184](resources/6b5b9fece59f470ab2de81b2d418507c.png)

![image185](resources/ad4ee5e970fd424ba5663cf65e914f98.png)

![image186](resources/6b2a69989cfa4e6e959d154a6b3ad0cd.png)

![image187](resources/5b797887919f4e99a81f04a30107c0d4.png)  
\(9\) order  
Real number can be bounded with proportional numbers(proof???)

![image188](resources/6b299ac9b4a748189fbaaeb546616379.png)

Inference : archimedean property, order between real numbers

![image189](resources/b0113cf1099b4b64931df1dd5ea80cfc.png)

For now, we can confidently say that any type of number in axis can be bounded with arbitrary types of number.

i.e. any number in the axis can be bounded by any type of number in axis, so they all can be ordered.  
\(10\) supremum&infmum  
![image190](resources/10cd5c9cb7ab4c12b338d27a74501084.png)

![image191](resources/d0842793d6dc4226aaf6a870e2a76f47.png)

![image192](resources/312081b1aede431bb3dd24d37ac9adb9.png)

For proof please refer to **"Tao. Real Analysis 5.5.9"** base on archimedean property

Now we can prove that only real number than proportional number can be solution of

![image193](resources/3f362dbbc07140be80d2b9fa24a67901.png)

![image194](resources/698232bd6597462c876f12a1075dd089.png)

![image195](resources/e610fd58377d461cb49263aa3831ca59.png)

![image196](resources/64a7a224e6f64ef988b33d8ad82e0518.png)

![image197](resources/07bb0b8aeb374002b9c2231662ca25ee.png)

![image198](resources/b43f9d6a01a342e398321a0208f7d813.png)

![image199](resources/094b4a000cdc4ec18bf4f731486c106d.png)

![image200](resources/7adf3736b39a45768b42246f7d951909.png)

Generalization

![image201](resources/4a4b1d80476e4044a1ea8e0fb5cd050f.png)

![image202](resources/08988ecf724043e99939e4a0f501a496.png)

Further

![image203](resources/52c82cd0181d48f5b3ff3a2e628f7c6e.png)

![image204](resources/9046e619cea441cf9adf69a4be041fcd.png)  
\(11\) base on definition of **supremum&infmum**, now we can define **limit** of real number sequence
Cauchy Sequence on real number

![image205](resources/a7085aa72f874af1a87b2458a8e5443d.png)

![image206](resources/fbe15e34e57548a9aadacc193c803e02.png)

Since any real number is bounded by proportional numbers, so it is compatible with Cauchy Sequence on proportional number

![image207](resources/7a53de80d6004955915e6b5b0b00e0db.png)

![image208](resources/cab5b5181c3f4b65bea4633df0fdbc0a.png)

![image209](resources/c33dcfd500c840cba036d9c4a85c98e1.png)

Proof: assume that

![image210](resources/d4fb9c37e6b54501801eca35e4d6c5dd.png)

![image211](resources/812951983f8146c39dc13233b9558cb0.png)

![image212](resources/844608da39e94f869189cdd671b8bb16.png)

![image213](resources/84f09c7334b14668b3a117c91c6be5db.png)

![image214](resources/158fc6760bba44dd81911caa7ee570a0.png)

![image215](resources/53072d875e75418a8aecfa6e05646fb9.png)

![image216](resources/9812491756514d488deadd924c73afe3.png)

![image217](resources/fee9925fbe1b418592ddeefbe1c1a2b3.png)

Now any property of proportional number is compatible with real number, so any proportional number is a real number, we complete the construction of real number(added with limit operation)
