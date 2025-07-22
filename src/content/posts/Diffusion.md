---
title: Diffusion
published: 2023-08-08
description: "Generate Image by Learning denoising process"
tags: ["noisy", "denoise"]
category: Generative-Models
draft: false
---

**Problem&Analysis**  

![image1](resources/07b6c5d0d0bb425cb1ad3d1fe7c0c2e2.png)

Base on **Maximum Likelihood Assumption**, we may try some following **solutions**  

![image2](resources/f917c85c45ec425ebb8ace71ba80a5db.png)
1.  ![image3](resources/6510efa40ab243c7b1a46d9e3c40a3cd.png)
![image4](resources/ce2565532944472ab9fa181010bb849b.png)

![image5](resources/3c65148157d547ff882abab4ce3a898e.png)

![image6](resources/790085525ef6481391e7f1d9eb7e8fa2.png)

generation:

![image7](resources/f4c9e75da3c04ea8984a4f543bb5d0ed.png)

drawbacks&generalization:

![image8](resources/c5206ec5435a4421af81e4e561c51c64.png)

we may need more complicate hypothese on form of distribution
2.  ![image9](resources/201c1b5fe31d47878b11584c41b799ea.png)
There's two ways leading to its lower bound

\(1\) using Importance Sampling

![image10](resources/3a3bc33b0ddf4c1cb47dd1e262c93e12.png)

using Jensen's inequality

![image11](resources/202c9c14089a4318a9815b59d3037340.png)

![image12](resources/c7ad6d078916433bacb421a91921adec.png)

\(2\) *Using Bayesian rule*

![image13](resources/05debf7eeb2743d09958cc54f1650a71.png)

![image14](resources/d664b829c1cc40b2990e621bc01ab0ee.png)

![image15](resources/dc4934bcfa9b4279a736bd50c8144c89.png)

![image16](resources/fb115f54a9384789bab346703ff47e00.png)

![image12](resources/c7ad6d078916433bacb421a91921adec.png)

![image17](resources/ddcc1e59576240b3b4dabb257daa1338.png)

iteratively

![image18](resources/2b9faa9f51254eeab5fdc025d222fb19.png)

![image19](resources/42f5e9c95d904505afafcfcf77c32375.png)

generation:

![image20](resources/4ef037b04b6b41f3b0eb40404158d595.png)

![image21](resources/c41ce0b8d6a049e484d700238b49c3ba.png)

drawbacks&generalization:

![image22](resources/49e70b07d9ec49c3ad2ba57f17126c4a.png)

here we introduce a latent variable Z for our generative model, so we can extend it to more general case where data generation following a process on a directed probabilistic model

General view of EM algorithm:

![image23](resources/cf1b9966bc1e4852835086d86f14f81d.png)

![image24](resources/e540821feaab4b9a9306e0e309ff6804.png)

![image4](resources/ce2565532944472ab9fa181010bb849b.png)

iteratively

![image25](resources/6551837eb83b4d82ad0c204cd38d0101.png)

![image26](resources/c0d412b7750a4d3ca6cebed3aece630d.png)

generation:

![image27](resources/025f5672ccf744e0859e2efcc8c87dc9.png)

![image28](resources/76ec6eb1468f42bdb13ae37c83d5e769.png)

drawbacks&generalization:

![image29](resources/085bccbefc5a498199517305a5966c67.png)

![image30](resources/8a3f457ab58b4f20bd9dac26148c62b0.png)

![image31](resources/93343bb1048d4ac38216ebebea5c539a.png)

3.  ![image32](resources/42461cae600140e9b8b7b7d796b96276.png)
Note : there has another way to approximate posterior named stochastic approximation (e.g. MCEM, by using sampling method to draw samples z from posterior distribution Bishop 11.1.6)

![image33](resources/04009635ff2141a3848bd346e156a169.png)

![image34](resources/fba883f5801c420cb73934dfec4e753c.png)

![image35](resources/5d3b656b30704e3b9ad735177e056cd7.png)

That brings the basic structure of variational autoencoder

encoder

![image36](resources/3440c19f3e2346029307fbef69ffbcc6.png)

*decoder*

![image37](resources/5567f00a7e834841b58695f884a5a115.png)

Note that VI often [underestimate variance](https://www.quora.com/Why-and-when-does-mean-field-variational-Bayes-underestimate-variance), this can date back from forms of KL-divergence which has detailed explanation in "Pattern recognition and machine learning. Bishop"

4.  Diffusion probability model : sequential latent variable
![image38](resources/45cd860d14844e6f85601f17fbb6e715.png)

*That means we use Markov chain to extend the VAE structure into*

forward trajectory : diffusion process, slowly destroy data's distribution

![image39](resources/e535a68c27704b5fb47fd9200de299c8.png)

reversal trajectory : generation process, slowly recover data's distribution

![image40](resources/97853f3158a1471482342264346a7192.png)

*Training objective:*

![image41](resources/3c4b4621dca642969d4094519d35a13f.png)

Apply the same technique in VI

![image42](resources/e629e4990e8d4e29b326894e7e297a65.png)

![image43](resources/356e03a05a5046a39bf210653d4a23f3.png)

![image44](resources/a8ae391eb5b54637a69c277bacf7baf5.png)

Base on **Markov Assumption**, this objective can be decomposed into summation of multiplication of each time's objective

![image45](resources/b1a63fc7d1c94c3eb01ffb0d1108781f.png)

![image46](resources/1eba7573c9c84ba99cb3eae294334a7c.png)

![image47](resources/449e4ce94664427ba1e9f91c20d945e0.png)

![image48](resources/f12b5d8850294820baa5622f436ca959.png)

![image49](resources/731546c9f6b440b695c5ecb7f68b603a.png)

![image50](resources/133208005bd042dfbe2daa66ee1f0937.png)

![image51](resources/6d3098e20b5443f49346e766a51c62ec.png)

![image52](resources/d8e0e48bf23e4649a0c4dbcb50a57584.png)

![image53](resources/a88094ce70984be5b60fdf59ce999642.png)

![image54](resources/b0a2dc14d91d402ea56522a329b0ebf2.png)

[Calculation of KL divergence](https://stats.stackexchange.com/questions/7440/kl-divergence-between-two-univariate-gaussians)

![image55](resources/e44ad1bd58a448beb03aa74fa2dd7e2f.png)

![image56](resources/34310edd083545cd8243a1c6e9f0f1a8.png)

![image57](resources/1544b0a297284f5c9ad37744a0c8af56.png)

![image58](resources/d83fc327240c4c85a657d0c77ce4dbce.png)

![image59](resources/e0a898b185394319b70214469665c3e4.png)

![image60](resources/357ab8ff078947cebad057b72ab51bfa.png)

![image61](resources/211ebd5cde3643cbaebf24cd5b83185b.png)

Same as the last phase of VAE, we then do reconstruction error between generated one and data sample.

In such perspective, we can take the optimization at each step as a special VAE, resulting in total T mini VAEs, instead, they estimate probabilistic distributions rather than real value

![image62](resources/49c7f1c625224981a512005561c63ecc.png)

![image63](resources/fab2f3a8e7f246c09a0f6103bb075ae9.png)

![image64](resources/577bd96a41704ffbbb6e260c6576a7f3.png)

![image65](resources/dfc70476999d411e82a5d0148a798ace.png)

![image66](resources/f2097575036b4a528d58916f55ee7ec3.png)

![image67](resources/782af9bb5b604c189dc7095374d6261f.png)

![image68](resources/39cdfd37219e4b9f88089c25d1d6f202.png)

![image69](resources/b5f2f4e818524ba3b2ab960ae55174c2.png)

![image70](resources/ccca53192d4446d4b8e8ddd85c9697cd.png)

![image71](resources/303655fc254e4649ada55f3c319e3cfa.png)

By using same variance, we have

![image72](resources/d120a3ebc69a4e38b955feb0ccfa09c2.png)

![image73](resources/8915bb7d691c446dace242ac5132005a.png)

![image74](resources/f958f8735cd044aabf64e83d361b9131.png)

[Training](https://github.com/hojonathanho/diffusion/):

![image75](resources/2f7d2a12985340b1b940af7ceb807d6e.png)

![image76](resources/3c616447dede4d03a8a3b048c87ae739.png)

![image77](resources/740fc5a1c37d43d7af87a5d265314742.png)

![image78](resources/520c94e77ea446ba8dde4fedd9249836.png)

If t \> 1

![image79](resources/657c98a171ae4ce289400c47acbd7733.png)

![image80](resources/b3a796ca4a05402cb53853c3e4fadd82.png)

![image81](resources/4da7825b816f49d799a59bcb0a0e8efd.png)

Else

![image82](resources/36b6633edd824c0c8d98e3cd5aa1f25e.png)

![image83](resources/c0b75b17631b4f67bfda9003305bcbec.png)

generation:

![image84](resources/1ab06a6b075649fc931264cbdac65392.png)

![image85](resources/e5f5a44a9b9d41e3adaae2c2abf21bd9.png)

![image86](resources/c1e9685d21a84f70adeb6b06b6017154.png)

**Connection to MCMC**  

The aforemention introduction proceeds at the perspective of optimization. But there has another view which can date back from core idea of MCMC.
1.  Diffusion process -- staionary distribution of Markov Chain
Provided with weak restriction(ergodic) on transition probability and stationary distribution, the target distribution recurrently diffused alone a MC can converge to a simple stationary distribution, e.g. Normal Gaussian

![image87](resources/88280bfec20b4b0b9dd6da39114dc9a7.png)

Note that the forward process in diffusion can also be called as process of random walk,

![image88](resources/9087f9678e494258b729355f8fe6bcba.png)
2.  Reversal process -- recovery from stationary distribution
The key that we can recover from stationary distribution is that the Markov Chain is reversible, that requirement satisfied when detailed balance is met

![image89](resources/ca3341f8cd4240f1b98eaa65b6e3911c.png)

Also, a sufficient condition for stationary distribution is detailed balance, that brings guarantee for the Diffusion process.

![image90](resources/cd5264c72566491081c90069e570358d.png)

And, detailed balance established when transition is symmetric -- Metropolis Algorithm

![image91](resources/b5bcc0e6e2204a10a2e92ba064ca090f.png)

Here we may get some inspiration of where the final regression loss function in the paper comes from

i.e. we are reconstructing a reversible Markov Chain that holds the symmetry between forward transition and reversal transition at each time step, which is also showed in KL-divergence between reversed forward transition kernel and predicated backward transition kernel in objective.

![image92](resources/c5b7a16488a44687a5f2f9d624e7bad3.png)

![image93](resources/007cc57878f34eec95ba115fb9988543.png)

![image94](resources/e0d60d46b77f4437ab29b802076d67c0.png)
3.  Difference to MCMC
In M-H algorithm, the sampling is done by analytically computing move probability

![image95](resources/31b57c8388054f78994ce47b2377f504.png)

Since the move probability is a key element to hold the detailed balance

![image96](resources/8bae0d7c1d8a451bac95e26d7631be77.png)

While in Diffusion, the MC already satisfied the detailed balance after training, so a recursive process of sampling can directly apply on MC to generate sample from target distribution (see generation of Diffusion)

**Connection to GAN**  

DDPM and GAN are classical instance of describe probabilistic model and implicit probabilistic model, respectively.

To estimate potential distribution of data, DDPM, learning under maximum likelihood assumption, approaches it by simulating the hierarchical process of generation, while GAN, learning in a contrastive way, directly sampling from it without obviously reconstructing its analytical form. So the performance of DDPM was naturally endowed with diversity, but lack of fidelity, while GAN does the opposite. But there are ways we can bridge gap between them.
1.  The diversity edge of DDPM
Actually, we can find out it for both of them, sampling is started from a random noise, but such randomness was added at every step of sampling in DDPM, resulting in high diversity of generation, but also brought with low efficiency of sampling.

So by reducing such randomness while keep optimization objective intact, we can modify its sampling process close to GAN's.

Issues of DDPM: slow and inefficient inference
1.  Large inference time steps
![image97](resources/1a1e8dfa3837469c8ac9f934b6af832e.png)

![image98](resources/1b212566c7a7412492964227c3123e12.png)

![image99](resources/8c5fb1394dec4c18b2ef50704c0394d9.png)

The analytical form of target reverse distribution was based on Markov Assumption

![image100](resources/fbabd7fc57e5481883ecf2afbacb64c2.png)

![image101](resources/9f7b225e9c2342268d1f55fef84f89d9.png)

![image102](resources/0d7e4302e80a4725b0cf20ba53a80f50.png)

![image103](resources/bb1f106e89ba4cc492c62cb66611c5e2.png)

So in order to unlock sampling process from forward(diffusion) process, a non-Markovian forward process is needed

DDIM: faster sampling process by altering forward process from Markovian to non-Markovian

![image104](resources/a6911c88f7a34b74bc8c7e91ea69d933.png)

![image105](resources/eef0693f4080406b9f81a38125e4a3e6.png)

![image106](resources/ae65e3a77c574a22b4ebf5dec312396f.png)

![image107](resources/16f16cc6d9994eb880c4473dfa3a51a9.png)

![image108](resources/3c5b40b25eb04fc5983a323f649af8ba.png)

![image109](resources/334d30dd9dc5498db507b2d2051ad4c1.png)

![image110](resources/e67ea48de9da4c09a408c2f44f9d3617.png)

The estimated reverse distribution can be induced using the same structure

![image111](resources/bcf4bf55662f42cba2aaa5c1890175ac.png)

Which is a generalized form of DDPM(one special solution), and specialized to DDPM when

![image112](resources/717b53023ffa47bc9760173abca0b927.png)

And forward process becomes Markovian

![image113](resources/ae344f5f3a8b4d77baefaac422a60510.png)

![image114](resources/7e8692754fe54d0f80425447c5656bd0.png)

![image115](resources/5c88fe76e2e346d8a4ad1bc99d229b55.png)

![image116](resources/5bed951724b5465f9129482ba99b0834.png)

![image117](resources/69561e849aef4eeabd1d9ed42e92cc17.png)

Which has the same form as the noisy process

![image118](resources/3187940e402f400e8b9ccfcd5693898c.png)

That means each operation in sampling process is also a noisy process but output noisy result from last time step, which is relatively a denoising result compare to current one, so the whole procedure becomes a denoising process.

From such perspective, an inverse process(i.e. generated sample to noise) can also be yielded using model's estimation, which can benefits lots downstream task by transferring image into potential latent space.

Note that the forward(diffusion) process no longer being a diffusion, but with marginal distribution fixed, the noisy process remains the same

![image119](resources/25847d09f9014580910bd591ddd6f602.png)

![image120](resources/06985517ce0345fa8a8b7cf069e33982.png)

![image121](resources/83cc59720b054261a1418de552814573.png)

![image122](resources/e35f26b75c68408bae1228cce0b2791a.png)

![image123](resources/c8c1cd2d8b3f4cc9894d7c8a6dafecd0.png)

![image124](resources/ca10d1c544524d10941548d7bc05d1b9.png)

![image125](resources/111e83f15ed44138a59483b3320e520d.png)

![image126](resources/3a97d3c9ba6d4efdaddccd848470388d.png)

![image127](resources/9cba2187d4284bcf9c5461afa9e5c735.png)

![image128](resources/7c4b62bdf14947ac9ed7f8eeaa65d914.png)

![image129](resources/f3ebf9ac35db4c49942bac97bf59f9b8.png)

In principle, this implies that forward steps can be way larger than sampling step, or even a continuous time step both for forward and backward

Further, we can prove that [DDIM is discretized case of continuous ODE](https://zhuanlan.zhihu.com/p/645665386)

![image130](resources/9c7600abc30a4acf9df0b947d892d820.png)

![image131](resources/15dfd42f232d44c59f9c95fdfccfae93.png)

![image132](resources/7304e1c2d5124e9bb2b159c366a26c33.png)
2.  Pixel-level inference
LDM: forward and backward processes in latent space, instead of in pixel-level

paper "**Denoising Diffusion Probabilistic Model**"  

Derivation of formula (4)

![image133](resources/becc865da2944eddbc45bc4f5dc5fb25.png)

![image134](resources/8484af77a0554f649e036db34ded6a79.png)

![image135](resources/f219bb2a624b45758f8bb87f84d92b4a.png)

![image136](resources/b4be55e9b1304da398d032bbdf8cb597.png)

![image137](resources/9721149b3951494d98cd62957c215407.png)

basic proof

![image138](resources/18f45d13c79e4ebe9b6992704724f0b3.png)

![image139](resources/bd9271e1bf9c4aea82a306e73b886a28.png)

![image140](resources/c820335c390749cdb3d46f5793b46038.png)

![image141](resources/e2b8e6be02eb432a8c37722f3af1098c.png)

![image142](resources/ffebec9344f947e1a77470bfc11e9233.png)

![image143](resources/71d02f5bacfa40b1a67b669473aa110b.png)

![image144](resources/bfcd9766580145859bf817779ea3330b.png)

![image145](resources/06276c9095884b1a99cf19a6eacad07c.png)

![image146](resources/998c55a6373d4b37bb421a9f9b56d057.png)

![image147](resources/9c3d99900c0344b281832efcf0168cdc.png)

![image148](resources/bc5adf123ad748f4adb96b494a0e7fcf.png)

Follow the induction, the predicate can be proved !

Derivation of formula (6)

![image149](resources/b1948fedd550469ba5c9176418356782.png)

![image150](resources/b69406d255ab4c3787db7616a39b382f.png)

Proof: using formula (4)

![image151](resources/c1086ca793034184aff235d40eec6670.png)

[According to product of two Gaussian PDF is a Gaussian PDF](https://davmre.github.io/blog/statistics/2015/03/27/gaussian_quotient)

![image152](resources/c566b7991ea2429bbd5e11e61c1913a1.png)

![image153](resources/28b438fad2534aad81d4e1b1916bee05.png)

![image154](resources/b784a67e1875495ea0f10fa5a08365f9.png)

[According to product of two Gaussian PDF is a Gaussian PDF](https://davmre.github.io/blog/statistics/2015/03/27/gaussian_quotient)

![image155](resources/e59e0fb1e4a14f6084de167fe95d783c.png)

![image156](resources/08797c45f32049c3872704593b4d3976.png)

![image157](resources/d68011e863e54d909e3c906942c40786.png)

![image158](resources/51bcaf75f50940698117693214f6ee47.png)

[Score matching](https://andrewcharlesjones.github.io/journal/21-score-matching.html) + diffusion

4.3 Progressive coding
