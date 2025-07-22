---
title: Contrastive learning
published: 2023-10-13
description: "Learning from negative samples"
tags: ["Negative Sampling", "Contrastive"]
category: Learning
draft: false
---

**Issue & Target**
Representation learning from supervised work always hard to transfer to downstream task, especially to different domain, and the result representation is weak at robustness or generalization, what's worse, domain adaptation requires lots domain-specific data, which is always unavailable.
So a task-agnostic way of learning is the answer for robust and generic representation which can easily transfer to any domain with highly data efficiency.

But how can we find such perfect way of learning ?
Actually, task-specific learning always involve specific labels, take classification for example, the induced features focus on conception related features, which are embedded into high-level latent space discarding low-level information that are irrelevant for classification but relevant for, e.g. image captioning.
In more general way, any label can be treated as a feature of data, but a task-specific one, so in turn, the data itself can be a kind of label, but a task-agnostic one. In that sense, representation learning from data itself can fully embed data into a compact property-invariant latent space. And when transferred to downstream task, small amount of task-specific labels are enough to extract or transform appropriate properties for domain adaption

So the basic idea is to learn **Consistent Identity Mapping**
i.e. we are trying to learn a mapping from (sparse/discrete) local representation to (dense/continuous) distributed representation embedded in latent space while keeping consistent identity.
![image1](resources/4225675b00234a168e5f6eda57171274.png)
\(1\) distance between similar samples' embedding are small, large for dissimilar one.
![image2](resources/ae9a5e6b465e48808b97e93138166342.png)

Contrastive learning: Incorporated with probability(optimization on probabilistic distance), this may lead to NCE, GAN
\(2\) Any transformations applied on samples have their homogeneous effects on samples' embedding but distinguishability is not change
![image3](resources/d35e9e1994ea4e9a8e6d0136a3a484c3.png)

Augment learning: like STM
![image4](resources/a5fd70cf76fc4bd5b53a968b0f52d65f.png)
![image5](resources/ba5d10ab0db944519b7e3fa6cf09ff90.png)

Predictive learning: Incorporated with probability, this may lead to generative model, like, VAE, Diffusion
**Cornerstone**
"The selection of appropriate positive and negative samples are the cornerstone of contrastive learning" from paper "SEMPPL"
There's a framework we can borrow from **Chapter 2 of "Machine Learning Tom. Mitchell"** to make a good explanation.
The learning process is to find hypothesis that maximally matches given samples, following the similar procedure of Candidate-elimination algorithm, contrastive learning is equivalent to process gradually narrowing down search space of hypotheses by keeping those success on positives while discarding failed on negatives.
Provided with hypotheses space containing the target hypothesis and infinite samples, optima is guaranteed. But it's elusive in practical condition where a local optima is best we can get, so the bottleneck is shed on the selection of positive and negative samples.
Now Let's specialize hypotheses as feature representation
Good positive samples:
Can guide to more significant feature(related to positives) representation learning

Can help models learn semantic positive representation where similar samples have

their embedding similarity maximized .

Can accelerate process of learning
Good negative samples(similar to positive one):
Can guide to more robust feature(for all) representation learning

Can help models learn semantic negative representation where dissimilar samples

have their embedding similarity minimized.

Also, can accelerate process of learning
Relate works: SEMPPL, hard mining, CLIP, NCE, triple loss, negative sampling
Actually, many works with contrastive objectives can be seen as a special case of contrastive learning.

**Inspiration in design of objective**
Actually, you will find out that terms in most effective objective functions always against each other, e.g. increase of one term results decrease of the other, the both may confine to a constant constraint, or some relationship(functional) constraint. Softmax is the former, score matching is the latter.
This property sometimes may quite throughout the model, e.g. GAN
The effectiveness of such methodology lies in its fight against laziness of neural network, as we all known, neural network is good at finding shortcut resulting chance-level performance, to avoid such degenerate case, adversarial or contrastive way of learning is introducing in the guidance of training process, by measuring model's representation capability from multiple angles that against with each other.
What's more, the idea also plays vital role in evaluation where indicators always try to catch model's performance from angles with subtle adversarial relation

**NCE**
[NCE bridges the gap between generative models and discriminative models, rather than simply speedup the softmax layer. With NCE, you can turn almost anything into posterior with less effort](https://github.com/Stonesjtu/Pytorch-NCE)

More detail introduction please refer to paper "**Noise-Contrastive Estimation of Unnormalized Statistical Models, with Applications to Natural Image Statistics**"

**How did NCE was designed ?**
actually, it didn't jump out of blank, it follows some good properties of MLE, like, consistency and Asymptotic normality, in other words, MLE is a blueprint, and NCE adapted it to its own need, which is easing the trouble of calculating normalization constant. it figures out a way that can embed the normalization constraint as an intrinsic property in objective where normalization can be automatically performed instead by hard constraint.

![image6](resources/8df338c2bfe3443ebb17e6fee7ebcfd0.png)
![image7](resources/5ebcea05c95e46ff8344d908118fd0c8.png)
![image8](resources/ef06041a98194733a753e62c3ca31591.png)
![image9](resources/4443dd6c24c947309632241e3b878881.png)

![image10](resources/027cd32b10354a05bb74787f7355bce7.png)
![image11](resources/2bb56a84639f4c52bcb6206dc7850c28.png)

![image12](resources/0b4227134b4a49c6a7765293598cbf5e.png)
Proof:
Using (1), ignore 1/2 for simplicity

![image13](resources/99394ca4326f4c3c88d65ae818e00987.png)

![image14](resources/9e3ec50b47f14be3ada1fd95f2e4ae4f.png)

![image15](resources/4da622b8775c49c4be89d1589d30cde9.png)

That means

![image16](resources/d06fdc2e31514b5a9bc870f4207f7782.png)

![image17](resources/9189d720f49546198935eb16ec7a9fc3.png)

![image18](resources/6243a082527e482c9211daa308c96b5c.png)
provided
![image11](resources/2bb56a84639f4c52bcb6206dc7850c28.png)

![image19](resources/e7ebd2642cb5479a9e105cb8bf601f56.png)

![image20](resources/0bea6e018e8d464086f2ebc0596c8828.png)

![image21](resources/57cc886adac044199020e16b81804681.png)

![image22](resources/3e95c320d80f4073b7e0e6b686155b83.png)

![image23](resources/35e86e5717ff41b096893adcdeca4ff0.png)
Proof of (3):
![image24](resources/74938ff76f054c3ea6e0f91d55c3f2e2.png)

![image25](resources/1f955058ecd247fab690fe876e2b6493.png)

![image26](resources/2de3c02fad8b4874af81f824809abb79.png)

![image27](resources/36e276b155dd4156a38cf5f930ace068.png)

![image28](resources/e2de15ccb76847088c87b75ca599c987.png)

![image29](resources/cd260d96c6d146cfbf8c2d48558796b7.png)

![image30](resources/ffcf3cc32a4341538966be2365d39b25.png)

![image31](resources/15a4c34b2eac4b4f81f989d0acecc9f5.png)

![image32](resources/2d74e6b5fb5f49a9abbd4fb613f1512d.png)

![image33](resources/dd9f07689806409c8920a8b5b1515ab1.png)

![image34](resources/95446faf8a5848e3a0914e122fc38ad0.png)

![image35](resources/7a3eb53cf18447029bba11470787dd95.png)

![image36](resources/e86c7f16954f440c8f9eab16dc4f25ab.png)

![image37](resources/dfd2130ec44a4d44a7c0746b1bbcd93a.png)

![image38](resources/e82dcf6cfab045c8bf7d6b8e49536f2a.png)

![image39](resources/b8d01b98c3914200aaed49512059054f.png)

![image40](resources/d6e5869449224c3fb40e12e0ffd63dab.png)
Proof:
That equivalent to prove

![image41](resources/5fec8af6ad15476494931ceb3a59728f.png)

The basic idea is to prove its upper bound convergent to 0 in probability too

In order to make (2) come into handy, we also need to transform the predicate into similar form

**Application on Logistic Regression**
![image42](resources/57da45e5448742928b6fd2eae57607a6.png)

![image43](resources/57d25f6ea4ae465ab8cdac20fec2ffb5.png)

**Sampling process**
![image44](resources/8a3e20fdcedf4c5f8eb7e15ba8adbd0b.png)

Joint distribution conditioned on label
![image45](resources/40a03ceed6a84074933a9cc6641f4a33.png)
Objective: log-likelihood
![image46](resources/01d94ea142024731a07dce5516572046.png)
According to Monte Carlo
![image47](resources/e9fc4ebc5cbc467cb4d1894db763fa8b.png)
where
![image48](resources/1a1cb947042b43f69be35aa0c0054545.png)

![image49](resources/b667874d758d4765ac3c2c815158c009.png)

where

![image50](resources/aa611146670d4fff850960c7f34419aa.png)
Normalization factor can be automatically learned though optimization
![image51](resources/eeaa738c35624b85930726e2575b0824.png)
[Since auto-normalize is assured by NCE, there is no need of introduction of normalization factor, i.e. normalization will be automatically fulfilled by weights](https://www.ruder.io/word-embeddings-softmax/#noisecontrastiveestimation)
![image52](resources/ea3924c800ad41a99f2938ac268544de.png)
![image53](resources/b3d29c5593b042c483127bb2390e843d.png)
![image54](resources/e6bdf6ebceb849c1b72a9ddd9eefd283.png)
Gradient of NCE will converge to Softmax, as k approaching to size of vocabulary

![image55](resources/2720445ce4514883b5783bb055593e05.png)
![image56](resources/2e4e30f08d4e49b89efd670703dd3599.png)
![image57](resources/29e4301c2cdd4d6f976dc03b704469b1.png)
![image58](resources/f78ec147f62d411ca0a2c353e7572263.png)
![image59](resources/da561784b8aa4c1dad44ab1c3ec5e659.png)

**Comparison between NCE and GAN**
From paper "ON DISTINGUISHABILITY CRITERIA FOR ESTIMATING GENERATIVE MODELS"
1.  A modified version of NCE with dynamic generator is equivalent to MLE
That was proved by considering extreme case where the model is copied as new noise distribution at each step of learning, which was called SCE, and results show that SCE has same expected gradient as MLE

2.  The existing theoretical work on GANs does not guarantee convergence on practical applications
That is mainly a results from optimizing in non-convex case

\(i\) mechanism of min-max optimization fails in [non-convex case](onenote:#Convex%20Optimization&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={EC2F328D-F4C1-4EE8-B893-8EE9ACD0103F}&object-id={05C97FFE-A206-0ED5-2623-1BE375DBAAEE}&D&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one) where minimizing lower bound is not guarantee minimization of its supreme.

\(ii\) Non-convergence of gradient-based learning (waiting for more testify)

3.  Because GANs do the model estimation in the generator network, they cannot recover maximum likelihood using same objective of NCE
MLE form of gradient

![image60](resources/312a16bd068a4764a657705e906cc66b.png)

![image61](resources/4b1a027091234f00b7c896ce19605ccd.png)

Adjust GAN gradient into MLE form

![image62](resources/313a11ae658b4e06a45e217cb773695b.png)

Turn into maximum likelihood derivatives

![image63](resources/c51113bb56eb43578793c2590172b189.png)

The discriminator can provide necessary information for computing maximum likelihood derivatives

![image64](resources/b15887ae8f244c0ba5113af601c54033.png)

![image65](resources/ee8d2b12aef24c8f9fe18a649b8568a7.png)

But this is different from the value given by distinguishability game

![image66](resources/d2f62f0acb844302b7247e9d5bdf837e.png)

![image67](resources/2abb09b6555c44ceb60400661b35e0cd.png)

![image68](resources/c40b157197184a398f8f73feae6e925f.png)
Preliminary:
![image69](resources/d86a2f0578994cc39e3779e85903345a.png)

![image70](resources/3129f2d8950e469eaa24834db3a5faf4.png)

![image71](resources/a2ef3e2d2ff64a53a6bd7f05f3eb48f2.png)

Both method are primarily driven by *distinguishability game value function:*
![image72](resources/672f56d9278c4bd89af1f0782040d30c.png)

Where

![image73](resources/d6fdc47768a94b8ca14df893f2477bc0.png)

But they have different learning targets
For NCE:
![image74](resources/fe95ab9090b747ee8ddfedd2d8ee7cdc.png)

Convergent on optimal where

![image75](resources/4d7e57a8819c46c2a5469570be2218a8.png)

i.e. NCE works by learning in the discriminator(via a generative model that is used to implicitly define the generator), maximizing acceptance rate of samples sampled from target distribution
For GAN:
![image76](resources/fff2f7bb6aad40f78e7e5597dda75e11.png)

![image77](resources/954605cf576b47a7ae1b82cf379a841f.png)

Convergent on optimal where

![image78](resources/a891492186724b008bc81809c138e92e.png)

i.e. GAN works by learning in the generator, minimizing rejection rate of samples generated from generator
