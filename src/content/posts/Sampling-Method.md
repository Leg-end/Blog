---
title: Sampling Method
published: 2023-10-05
description: "How to simulate data generation process"
tags: ["Statistic Inference", "Sampling"]
category: Generative-Models
draft: false
---

This topic also has its connection to **Statistical Inference** in **Chapter 5.6**

**Problem & Analysis**  
![image1](resources/c011af22b8a04a54a64c02656036676a.png)
![image2](resources/bddb34141595423c9cde651db0f5f572.png)

In more specific case, we are doing a series of trial  
![image3](resources/818eb1ff840b4d99953cf3863b884992.png)  
We want to know the probability of event based on n trials  
![image4](resources/3b8d555fe95d4440a024cf2d0246394c.png)  
It would be too difficult to directly do numeric computation
![image5](resources/a777c32823ff4bed8cae7ea6f507d5ed.png)  
The more simple way is(Monte Carlo Sampling)  
![image6](resources/4b6c730c808e4e0e9ed2cf6b331d9e09.png)
![image7](resources/9da7c22a681544a9a19cc50212cd80ff.png)
![image8](resources/385b1a35561e43bbb868bb3eb74305a8.png)
![image9](resources/85c645db804c45399eadd1fbb52b40a3.png)

Note that accurate solution for moment is also hard to reach, so some approximation method can be applied, e.g. Taylor series approximation
\(iv\) further, the probability of event could be directly estimated by central limit theorem

So in the core is how to generate random samples. Actually, we already have lots algorithms that can generate random samples from uniform distribution, so now we only need to care about how to get arbitrary random variable from uniform one.
![image10](resources/64d76cdadaa1449789951d4aa651a7ca.png)
1.  ![image11](resources/fdb65933db844325af34490cfa82cff8.png)
2.  ![image12](resources/4b0bd6254f124dd0ba944f5342a589e0.png)
![image13](resources/a6c439ac3209440d90e06071c43bf51d.png)
![image14](resources/3bec755ce10b48d28dbb1ca029b05ac7.png)
e.g. generator in GAN
Obviously, IPM doesn’t have a tractable likelihood function, so it can only learn in likelihood-free way, like adversarial or contrastive way of learning.

**Directly From uniform to arbitrary distribution**  
Target distribution of Y can be transformed uniform one by a specific function
![image15](resources/032cc23477c64b46b34833f1180e83d1.png)
We can get random variable Y transformed from Z with a function which is the inverse of Y's CDF
Also, we see that any random variable has its CDF value a uniform distribution  
![image16](resources/4deb23d21455433a838c56203a3bcfc6.png)  
Note that for multivariant case  
![image17](resources/1c91fded0fef4d94abcaa4749c8cb268.png)  
The sampling process on Y is then  
Continuous Case:  
![image18](resources/f13b47c733084ee49ac9f07f3171e590.png)  
Discrete Case:  
![image19](resources/c4ee2768dbe346afa0e16989a2cd83e1.png)

![image20](resources/db99234b545f47f89c2da9f27a37416e.png)

But the above method failed when CDF has no analytical expression

**Indirectly From uniform to arbitrary distribution**  
![image21](resources/d1925d8d85b34c738514218d57eaa81f.png)  
The core idea can always relate to geometry, we uniformly sample points from a rectangular which has its length and width uniformly ranged in \[0, 1\], and then discard points outside of target distribution region. i.e. we are trying to cover target distribution's integral region with sampling points falling in it.
e.g. Box-Muller method for generating samples from Gaussian Distribution
In order to cut the sample size, we need to shrink the rectangular as tight as with target distribution. i.e.
![image22](resources/a21b76fc122342748f66cf82ffe78a6a.png)
![image23](resources/73b12a0c422a45fbaa02abcb7bdab74d.png)
![image24](resources/064d482fa1b547908ba620256636ac56.png)
![image25](resources/a48f96377a1a40008125a75ddb09ec6d.png)

![image26](resources/7b4021de688d4743afde4959c60b360d.png)
![image27](resources/c95603f13ca6419795ae4183cf34e89c.png)
![image28](resources/5bc3a14da3a94d90b7eb194072f19590.png)
![image29](resources/81bf2e5ea4a54869aefa226309691ded.png)  
Proof:  
![image30](resources/50b2e1321da0431d8eed49f55a71bf5b.png)

![image31](resources/71c1b6eaa1d44f6b9fb35a3bf174c949.png)
![image32](resources/0e9736e9a096497c8023c0eb8e1bf187.png)
![image33](resources/2abb8209eae94de68e7d5bf823017e1d.png)

![image34](resources/8f446fb672a44c388ad53cb653ec9a6f.png)

But there exist a shortage preventing it from adapting to high dimensional case:
![image35](resources/baab5680543d47e6af10bdae941bfbc8.png)
![image36](resources/b7c68a94163847f89756dd2b759f301e.png)
![image37](resources/4abeb8614ce4486885188f694ee22087.png)

**Importance Sampling**  
It focus on approximating moment estimation in (iii) of section Problem & Analysis but not itself provide a mechanism for drawing samples from target distribution
It has its simple idea that sampling on proposal distribution where points are easily drew, comparing to its target counterpart which is hard to sample but evaluable.
![image38](resources/b91b7c74a8dc4780b1e6337bed6ecd93.png)
By law of weak large number
![image39](resources/b2e80fe6c4954247a5ce8ddbdc9ae4df.png)
![image40](resources/357e7042066b44ca8788b34a72c9a72a.png)
The major drawback is that it may produce results that are arbitrarily error and with no diagnostic indication.
![image41](resources/7f6465d023424c0797b4adec697d9342.png)

**Sampling-importance-resampling**  
Turning Importance Sampling method available for drawing samples
![image42](resources/09c0927656264c3bbfb3d2b2f8e2a2f2.png)
![image43](resources/026d228e2b5d44e58b8b6f23f8cb38c7.png)
![image44](resources/1058bee2f523469b932fb59252ab01a1.png)  
Proof:  
![image45](resources/a32b84aa168e4bc4b829cdd2ef334f20.png)

Sampling Method + EM = IP, inspiration of Data Augmentation Algorithm (todo)

[**MCMC**](https://towardsdatascience.com/langevin-dynamics-29bbb9407b47)  
Resource: <https://bjlkeng.io/posts/markov-chain-monte-carlo-mcmc-and-the-metropolis-hastings-algorithm/>  
Base on the idea of accept/reject, we can simplify sampling method into two component,
First we sample from a proposal distribution, Second we accept it or reject it according to same rule which will prefer sampling points staying in high density region of target distribution.
But in the aforementioned methods in which directly sampling a point perfectly sitting in high density region of target distribution is so hard, MCMC tries firstly to explore the target region by sampling a sequence from proposal and transitional according to acceptance rate.
So the exploration will eventually lead it to the sketch of target distribution and upon which a sampling trajectory leading to high density region will be built.
So the key point is to find suitable accept/reject rule keeping sampling point in high density region. But it also induce same drawbacks:
1.  To explore the region of target distribution, we may need to iterate the whole data several times
2.  Only high density region(where data samples are gathered densely) has high accept rate, resulting ignorance for rare events(border region of target distribution)
3.  Random walk issue may drag the efficient of sampling(exploration), causing slow convergence. (since a small moving step will be adapted to avoid high rejection rate)

It samples a sequence from proposal slowly converging to target distribution.
Promise of convergence of sampling on Markov Chain
we know that transition matrix T has maximum eigenvalue 1, so the iterative multiplication will eventually converges to its eigenvector of eigenvalue 1, i.e. invariant(target) distribution, provided T satisfies some weak restrictions

![image46](resources/d1fbd5a28bfd4dfd9c5aa2ca12d74987.png)
This is equivalent to **guided** walk in region of target distribution
Allow sampling from large classes of distribution and scale well in high dimensionality

[**Metropolis-Hastings Algorithm**](https://natan-katz.medium.com/metropolis-hastings-review-2dfeb0c3d0eb)  
\(i\) initialize  
![image47](resources/63c96b93e67949cb80c77175cf5c970a.png)  
\(ii\) Iterate  
![image48](resources/e1beebf1231a4ab8bd1886363bb38f0c.png)

![image49](resources/9ba1b8d5045745edada486a421d06afe.png)

calculate acceptance probability

![image50](resources/b8e2ea77fab14ecea70a72f6cb37ae42.png)

Accept or reject according to uniform sampling

![image51](resources/1cd985a5b1d640dfac62698af466a5ed.png)  
Note that when proposal distribution is symmetric, it reduces to **Metropolis Algorithm**  
![image52](resources/3295bc4522f0436996906947f1919d5e.png)
![image53](resources/5336861cd69f46f1a88992afb14b7be3.png)  
Proof of converge:  
![image54](resources/79b2dee03b4e4004bbe71aa4e5171687.png)

![image55](resources/621a88651b9d4ceba18f0e335ad47cd0.png)

![image56](resources/8ee19e25ae654c17bdfe3e4291d58b1a.png)

![image57](resources/010235eab1d54e2cbd440527f730bfa2.png)

This is exactly detailed balance, so convergence is assured

**Gibbs Sampling**  
Special case of Metropolis-Hastings with fold line trajectory sampling path for multivariate variable  
\(i\) initialize  
![image58](resources/bda9d78d07be4a728d777bd2d32470e5.png)  
\(ii\) iterate  
![image59](resources/6fcaa81dc9704160b35e76db7a4299d8.png)

![image60](resources/c17dbf62c7094f01b5954722b87b819d.png)

…

![image61](resources/75828422a7b44d058fce16f7838b3aa3.png)

[**Hamiltonian Monte Carlo**](https://bjlkeng.io/posts/hamiltonian-monte-carlo/)

"The main idea behind HMC is that we're going to use Hamiltonian dynamics to simulate moving around our target distribution's density. The analogy used in \[1\] is imagine a puck moving along a frictionless 2D surface[<sup>2</sup>](https://bjlkeng.io/posts/hamiltonian-monte-carlo/#id4). It slides up and down hills, losing or gaining velocity (i.e. kinetic energy) based on the gradient of the hill (i.e. potential energy)"

That is, we are simulating a trajectory of particle on surface vertically flipped from our target distribution where high density region correspond to the valley absorbing particle to stay in for most of the time.
Note that the introduce of momentum is for randomness, which simulates interaction with heat bath, without it, any particle will only follow the only optimal trajectory leading to valley. This is as expected because the particle will get "pulled" into the dips while the momentum could vary by the interaction with the heat bath. So we may also get little chances of particle showing in low density region.
So the all possible states(canonical ensemble) a particle in the system can be caught by a probability distribution, i.e. canonical distribution, which can be set as Boltzman distribution.
PS. This can be related to gradient descent algorithm with momentum which is designed to jump out of local optimal by adding more randomness

Analog
<table>
<colgroup>
<col style="width: 49%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Physic</th>
<th>MCMC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>![image62](resources/da17dabbfffd4b97badb9c926e2847e3.png)</td>
<td><p>Variable of target distribution</p>
<p>![image63](resources/762a42fdb73640f98c2fc845897ffaef.png)</p>
<p></p></td>
</tr>
<tr class="even">
<td>![image64](resources/d9c798b959c5491b8ebe33b8ff396a2b.png)</td>
<td>![image65](resources/e5fc3c812a514053a0b84f1f1b1afcd3.png)</td>
</tr>
<tr class="odd">
<td><p>![image66](resources/e110e4ac000b47f1bc186da8b0b01fb0.png)</p>
<p>simulate both the particle moving around as well as the random changes in direction that occur when it interacts with the heat bath.</p></td>
<td><p>Randomness when sampling</p>
<p>Guidance for sampling (both direction and magnitude)</p></td>
</tr>
<tr class="even">
<td><p>![image67](resources/e0e8988c43fc42b1ae22e3c7560bee25.png)</p>
<p></p></td>
<td>![image68](resources/6caa40694aef45a3bc2b8eccfe0e3263.png)</td>
</tr>
<tr class="odd">
<td>![image69](resources/3ab64b4b88dc42c38049c22e2a18a49a.png)</td>
<td>Can be used to model canonical distribution</td>
</tr>
</tbody>
</table>

Classical Mechanics: Net force  
![image70](resources/7269b30e8f574264ae3b741c86e2aa77.png)
![image71](resources/15d6070e19af4fba99b186e04558e7da.png)  
Lagrangian Mechanics: Total energy  
![image72](resources/eee4a78fff384b8ab72c60dab6e20c75.png)

![image73](resources/9e71dbfb8ccf4737a6ddab3996c7a695.png)

![image74](resources/54da7a70ffe648aa9cfee4e812f96127.png)
![image75](resources/ed02529a91614d5d91e42fd31bc45a62.png)
![image76](resources/acb95ec3bd014a1db89f2c4999bcf97a.png)

phase space:= {(position(state), momentum(direction & magnitude))}
Hamiltonian and Hamilton's Equations: System energy under phase space  
![image77](resources/de8a7209abfb4976b32175763b7410b1.png)

![image78](resources/a06b5f4ec9704e0c9d07f8016ca365e3.png)  
Using phase space coordinate by introducing generalized momentum  
![image79](resources/3e8ba803d6a24b698ad70b7de69a5cd3.png)
![image80](resources/a20d954a00f14ca8b3d53061b4b5e0c8.png)
![image81](resources/01b7928af0724997bcc4444cd2516a80.png)
![image82](resources/e96281811bd0469e8a3dc61632843aa9.png)
![image83](resources/0c900946b36d49e7984b55cdfcf8beaa.png)
![image84](resources/2028929ca3bd4c099cb13679787f1dfa.png)
![image85](resources/fefc0b6ee5c6426fa77906a6fea33f1c.png)

at the peril of discretization error, to mitigate such error we can use Modified Euler Method

![image86](resources/3c0291bd527348668004b1a5c069e16d.png)

Or further, Leapfrog Method(Simpson Method)

![image87](resources/56ed2aafbe5143748dfb716caf658439.png)
Guarantees for fast convergence  
\(1\) Conservation of the Hamiltonian: The overall energy of the combined system(heat bath and internal system) is conserved.
![image88](resources/eaf4c1c74d464b35b8d10f2dca3d807f.png)  
\(2\) Volume preservation  
![image89](resources/be2e198c75c8477a8652d8e43914884e.png)

So the random walk (transition of state) will be bounded in limited volume

And we can only focus on an infinitesimal region of state where associated quantities (density, Hamiltonian, etc.) can be treated as constants. That greatly eases the way to proof detailed balance and correct probability according to canonical distribution built on that

![image90](resources/095148183799491ea992c22ee93f2a3a.png)
![image91](resources/90d160cc69b2477ead194dfc312a0ea1.png)
![image92](resources/b2acc2e879cd468e8a59d396ea685f3e.png)

![image93](resources/a6d0c75681dd4b50ae250d271920b3bd.png)

![image94](resources/a5144eeb9afc4e71803df0b54e147257.png)
![image95](resources/469cd20d82da43cca0a48e84fae1936e.png)  
So the whole process is essentially the same structure as MH but using Hamiltonian dynamics to find new proposal sample.
Step 1: Simulation of random interaction with heat bath  
![image96](resources/9ba1d39907dd4ce8a28bf59b06902945.png)

![image97](resources/d91573d35bae4015a7d9b27940ecd05b.png)
![image98](resources/e20246c26fc44e83a14079c8dbbac7a9.png)

![image99](resources/da842887188d4199943e3a082c3b34fe.png)
![image100](resources/09c1198f373e4babb87017f33010fd36.png)
![image101](resources/81b6f848024e461d9f1cb74bfb4eb43f.png)
So we have
![image102](resources/1a7012f4c6a3414c8c24755ebe4e33b7.png)

![image103](resources/d0004e765df5492abef9daee729bd3aa.png)

![image104](resources/ab0f0bcb40b14ca897d18d76d86e6a2f.png)  
Note that if we were able to simulate Hamiltonian dynamics exactly, recall that the Hamiltonian is constant along a trajectory ([Conservation of the Hamiltonian](onenote:#Sampling%20Method&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={4F341C3A-CF66-4855-B9B3-DA4571AC8699}&object-id={ADC9A1B0-44DE-0EC9-0325-78F34E1AD9E3}&A3&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one)), i.e.  
![image105](resources/e6033489f694430c913f37aa1712b2c9.png)
Then we would get 100% acceptance rate as we mentioned in premises of "[Guarantees for fast convergence]  (onenote:#Sampling%20Method&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={4F341C3A-CF66-4855-B9B3-DA4571AC8699}&object-id={ADC9A1B0-44DE-0EC9-0325-78F34E1AD9E3}&A1&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one)"  
But the discretization error will not get us there so we need the MH step (reject & accept)  
Limitation
1.  Sampling is only available for continuous distribution
Recall that Hamiltonian equations are built upon derivatives
2.  A evaluable function proportional to target distribution is needed, and derivatives can be computed in any non-zero region of the distribution
3.  Hyperparameters need careful tuning, including
![image106](resources/165ea73b3a734f018116139db384db6e.png)

These can be tuned according to index of autocorrection between sampling points

\(b\) momentum, variance for Gaussian distribution

Too low momentum may ignore tails of target distribution

Too high momentum may lead to low acceptance rates

[**LMC**](https://bjlkeng.io/posts/bayesian-learning-via-stochastic-gradient-langevin-dynamics-and-bayes-by-backprop/)  
Langevin Monte Carlo (LMC)[\[Radford2012\]](https://bjlkeng.io/posts/bayesian-learning-via-stochastic-gradient-langevin-dynamics-and-bayes-by-backprop/#radford2012)is a special case of HMC where we only take asinglestep in the simulation to propose a new state (versus multiple steps in a typical HMC algorithm)  
![image107](resources/dec336edd5f0480fbd1f4855e3bd1d82.png)
![image108](resources/60735e92dc2940a7a71c9ac3fc12a9ed.png)

![image109](resources/71cd8910782e48e09c52a805043c1a40.png)

![image110](resources/f6879372e6e94f0a8375c102f3d4e0c8.png)

![image111](resources/e6c0641c034d46308975e5f32eff566f.png)  
This is known as Langevin Equation, and can be re-write in the form of stochastic gradient descent with
![image112](resources/7b4490a850114dd9b343a38884a8942a.png)

![image113](resources/2b6db0e7d9ca44f59eda9acbb02084ed.png)  
We can get
![image114](resources/b36d72337b0d4845b80d248ce3bc48f1.png)  
SGLD: SGD + LMC  
Stochastic Gradient Langevin Dynamics  
This is simply the LMC applied on mini-batch data  
![image115](resources/9b7d694a83af40c4945a3d51d852cc0e.png)

![image116](resources/9bdad027ab394691b9c5c2c213fa401f.png)  
To make sure the new update rule still leading to solution of LMC, i.e. posterior distribution, one must prove that the overall randomness was dominated by injected gaussian noise
This is equivalent to prove that scale of variance of gaussian noise is larger than that of mini-batch data

**Why it can converges to target distribution ?**  
If we simply just sample along maximal gradient without injected noise, we can only reach to mode of target distribution
But with random perturbation, we can reach a set around the mode following the distribution of target one.
Imagine that each sampling will be on different path that leads to different points, all these samples forms the sample space of target distribution, and the tendency that towards them corresponding to their probability in the target distribution,

PS: estimation of PDF is always the first problem before sampling from it.
The basic density estimation thoughts can date back to histogram, which has a logical and clear chain of thoughts in [here](https://milania.de/blog/Introduction_to_kernel_density_estimation_(Parzen_window_method)).
![image117](resources/b367065ddb2d4294bc01040a8c525afa.png)

![image118](resources/1a20da2e397142bfb769d59162941f6f.png)
But described as forms of step function often fails to real application, so in the call of continuous form of pdf, Parzen Window Estimator, alas Kernel density estimation, was introduced by simply modified the form of bins with more complicated kernel function
![image119](resources/68a1d29082e842528c4787199e691b6e.png)

![image120](resources/a824c21d0e724b199e07d26cfbb19613.png)  
IMO, There is also a strong connection between PWE and posterior estimation if we take the pursued pdf as a posterior, then following the rules of Bayesian laws  
![image121](resources/dbf0a510f02243ab90a601cf71d4554b.png)

![image122](resources/47560fe624d844e39e00ac871ef058c6.png)  
If we assume that any sample can be uniformly sampled from a bin, then we'll have
![image123](resources/a9a8dc47ee074538b5d2ff58112e043b.png)  
And the likelihood is approximately quantity estimated in a bin, which for simple histogram is
![image124](resources/03a99af9abfb42349444023e9224cc66.png)
for PWE is
![image125](resources/78a4c5f8ea984b72ace93093a22b1b42.png)
Provided with assumption that
![image126](resources/b3f46db344fd4b6881d13876046a68f9.png)  
We can infer that kernel function can be function of exponential form, e.g. Gaussian kernel function, which equals to add Gaussian noise to sample points, so the overall pdf is the combination of Gaussian distributions centering at different data points. This also sounds bits of outter interpolation.  
![image127](resources/74d3ea4cbe754c70ad6189783cb460fd.png)

\[1\] Implicit Maximum Likelihood Estimation  
\[2\] Learning in Implicit Generative Models
