---
title: "Contrastive learning"
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

$$
f:\mathcal{X}\to \mathcal{V},\ \ x,y\in \mathcal{X},
$$

(1) distance between similar samples' embedding are small, large for dissimilar one.

$$
d\left(x,y\right)\propto d\left(f\left(x\right),f\left(y\right)\right)
$$

  Contrastive learning: Incorporated with probability(optimization on probabilistic distance), this may lead to NCE, GAN
(2) Any transformations applied on samples have their homogeneous effects on samples' embedding but distinguishability is not change

$$
T\left(x\right)\Rightarrow f\left(T\left(x\right)\right)
$$

  Augment learning: like STM
(3) Moderate destructive operations $D$ applied on samples can be restored by using inverse mapping from samples' embedding

$$
{f}^{-1}\left(D\left(x\right)\right)\to x
$$

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

$$
{J}_{T}\left(\mathit{\theta}\right)=\frac{1}{2T}{\sum}_{t}\mathrm{ln}\left(\mathit{\sigma}\left({x}_{t};\mathit{\theta}\right)\right)+\mathrm{ln}\left(1-\mathit{\sigma}\left({y}_{t};\mathit{\theta}\right)\right),\ \ {x}_{t}~{p}_{d}\left(x\right),{y}_{t}~{p}_{n}\left(y\right)
$$

$$
J\left(\mathit{\theta}\right)=\frac{1}{2}\left\{{E}_{x~{p}_{d}\left(x\right)}\left[\mathrm{ln}\left(\mathit{\sigma}\left(x;\mathit{\theta}\right)\right)\right]+{E}_{y~{p}_{n}\left(y\right)}\left[\mathrm{ln}\left(1-\mathit{\sigma}\left(y;\mathit{\theta}\right)\right)\right]\right\}
$$

According to weak law of large numbers,${J}_{T}\left(\mathit{\theta}\right)\to J\left(\mathit{\theta}\right)$

$$
P\left(\left|{J}_{T}\left(\mathit{\theta}\right)-J\left(\mathit{\theta}\right)\right|\ge \mathit{\epsilon}\right)=0,\ \ T\to \infty 
$$

$$
\text{Theorem 1}:\ \underset{f}{argmax}\stackrel{~}{J}\left(f\right)=ln{p}_{d}(\bullet ),\ \ \stackrel{~}{J}\left(f\right)=J\left(\mathit{\theta}\right),\ f\left(\bullet \right)=ln{p}_{m}\left(\bullet ;\mathit{\theta}\right)
$$

provided

$$
\left(1\right)\ \forall \mathrm{x},{p}_{d}\left(x\right)\ne 0\Rightarrow {p}_{n}\left(x\right)\ne 0
$$

$$
\left(2\right)\ P\left(\left|{J}_{T}\left(\mathit{\theta}\right)-J\left(\mathit{\theta}\right)\right|\ge \mathit{\epsilon}\right)=0,\ \ T\to \infty 
$$

Proof:
  Using (1), ignore 1/2 for simplicity

$$
\stackrel{~}{\mathrm{J}}\left(f\right)=\frac{1}{2}\int {p}_{d}\left(x\right)\mathrm{ln}\mathit{\sigma}+{p}_{n}\left(x\right)\mathrm{ln}\left(1-\mathit{\sigma}\right)dx
$$

$$
\frac{\partial \stackrel{~}{\mathrm{J}}\left(f\right)}{\mathit{\partial}f}=\frac{1}{2}\int {p}_{d}\left(x\right)\left(1-\mathit{\sigma}\right)-{p}_{n}\left(x\right)\mathit{\sigma}dx=0
$$

$$
\ \Rightarrow f\left(\bullet \right)=\mathrm{ln}{p}_{d}\left(\bullet \right)\Rightarrow {p}_{m}\left(\bullet ;\mathit{\theta}\right)\to {p}_{d}\left(\bullet \right)
$$

$$
{\left.\frac{{\partial}^{2}\stackrel{~}{\mathrm{J}}\left(f\right)}{\mathit{\partial}{f}^{2}}\right|}_{\mathrm{ln}{p}_{d}\left(\bullet \right)}=-\frac{1}{2}\int \frac{{p}_{n}\left(x\right){p}_{d}\left(x\right)}{{p}_{d}\left(x\right)+{p}_{n}\left(x\right)}dx<0
$$

$\Rightarrow \mathrm{ln}{p}_{d}\left(\bullet \right)$ is the only maximum
  That means

$$
{p}_{m}\left(\bullet ;\mathit{\theta}\right)=c\left(\mathit{\theta}\right){p}_{m}^{0}\left(\bullet ;\mathit{\theta}\right)\to {p}_{d}\left(\bullet \right)
$$

  With ${p}_{d}\left(\bullet \right)$ is normalized, so as ${p}_{m}\left(\bullet ;\mathit{\theta}\right)$, and the normalization constant $c\left(\mathit{\theta}\right)$ can be automatically learned  


$$
\text{Theorem 2:}\ {\widehat{\mathit{\theta}}}_{T}=\underset{\mathit{\theta}}{\mathrm{argmax}}{J}_{T}\left(\mathit{\theta}\right)\stackrel{P}{\to}{\mathit{\theta}}^{\ast}=\underset{\mathit{\theta}}{\mathrm{argmax}}J\left(\mathit{\theta}\right)
$$

provided

$$
\left(1\right)\ \forall \mathrm{x},{p}_{d}\left(x\right)\ne 0\Rightarrow {p}_{n}\left(x\right)\ne 0
$$

$$
\left(2\right)\ P\left(\left|{J}_{T}\left(\mathit{\theta}\right)-J\left(\mathit{\theta}\right)\right|\ge \mathit{\epsilon}\right)=0,\ \ T\to \infty 
$$

$$
\left(3\right)\ \bm{I}=\int \bm{g}\left(\bm{x}\right)\bm{g}{\left(\bm{x}\right)}^{T}P\left(x\right){p}_{d}\left(x\right)dx\ has\ full\ rank
$$

$$
\bm{g}\left(\bm{x}\right)={\left.{\mathbf{\nabla}}_{\bm{\theta}}\mathrm{ln}{p}_{m}\left(x;\mathit{\theta}\right)\right|}_{{\mathit{\theta}}^{\ast}},P\left(x\right)=\frac{{p}_{n}\left(x\right)}{{p}_{d}\left(x\right)+{p}_{n}\left(x\right)}
$$

Then 

$$
J\left({\mathit{\theta}}^{\ast}\right)>J\left({\mathit{\theta}}^{\ast}+\mathit{\phi}\right),\forall \mathit{\phi}\ne 0
$$

$$
\left(4\right)\ {\mathrm{p}}_{\mathrm{d}}\left(\bullet \right)={p}_{m}\left(\bullet ;{\mathit{\theta}}^{\ast}\right)
$$

Proof of (3):
  (3) assures that for large T, ${\mathrm{J}}_{T}$ becomes peaky enough around the true value ${\theta}^{\ast}$
   $\mathrm{i}.\mathrm{e}.\ {\left.{\nabla}_{\mathit{\theta}}^{2}{J}_{T}\left(\mathit{\theta}\right)\right|}_{{\mathit{\theta}}^{\ast}}\to {\left.{\nabla}_{\mathit{\theta}}^{2}J\left(\mathit{\theta}\right)\right|}_{{\mathit{\theta}}^{\ast}}\ $ should be positive define, i.e. has full ranks

$$
{\nabla}_{\mathit{\theta}}^{2}J\left(\mathit{\theta}\right)=\frac{1}{2}\int \mathit{\sigma}\left(\mathit{\sigma}-1\right)\left({p}_{d}\left(x\right)+{p}_{n}\left(x\right)\right)\bm{A}\ +\bm{B}\left({p}_{d}\left(x\right)-\left({p}_{d}\left(\bm{x}\right)+{p}_{n}\left(x\right)\right)\mathit{\sigma}\right)dx
$$

$$
\bm{A}={\mathbf{\nabla}}_{\bm{\theta}}\mathrm{ln}{p}_{m}\left(x;\mathit{\theta}\right){{\mathbf{\nabla}}_{\bm{\theta}}\mathrm{ln}{p}_{m}\left(x;\mathit{\theta}\right)}^{\bm{T}}
$$

$$
\bm{B}={\mathbf{\nabla}}_{\bm{\theta}}^{2}\mathrm{ln}{p}_{m}\left(x;\mathit{\theta}\right)
$$

  Take in ${\mathit{\theta}}^{\ast}$

$$
\mathit{\sigma}\left({\mathit{\theta}}^{\ast}\right)=\frac{{p}_{d}\left(x\right)}{{p}_{d}\left(x\right)+{p}_{n}\left(x\right)}
$$

$$
\bm{A}=\bm{g}\left(\bm{x}\right)\bm{g}{\left(\bm{x}\right)}^{\bm{T}}
$$

$$
\mathit{\sigma}\left(\mathit{\sigma}-1\right)\left({p}_{d}\left(x\right)+{p}_{n}\left(x\right)\right)=\frac{{p}_{n}\left(x\right)}{{p}_{d}\left(x\right)+{p}_{n}\left(x\right)}{p}_{d}\left(x\right)=P\left(x\right){p}_{d}\left(x\right)
$$

$$
{p}_{d}\left(x\right)-\left({p}_{d}\left(\bm{x}\right)+{p}_{n}\left(x\right)\right)\mathit{\sigma}=0
$$

$$
\Rightarrow {\left.{\mathbf{\nabla}}_{\bm{\theta}}^{2}J\left(\mathit{\theta}\right)\right|}_{{\mathit{\theta}}^{\ast}}=\int \bm{g}\left(\bm{x}\right)\bm{g}{\left(\bm{x}\right)}^{T}P\left(x\right){p}_{d}\left(x\right)dx=\bm{I}
$$

  When $\bm{I}$ has full rank, so ${\left.{\mathbf{\nabla}}_{\bm{\theta}}^{2}J\left(\mathit{\theta}\right)\right|}_{{\mathit{\theta}}^{\ast}}$ can be either positive define or negative define
  Note that $\mathbf{s}\mathbf{c}\mathbf{o}\mathbf{r}\mathbf{e}\left({\mathit{\theta}}^{\ast}\right)\u2254{\left.{\mathbf{\nabla}}_{\bm{\theta}}\mathrm{ln}{p}_{m}\left(x;\mathit{\theta}\right)\right|}_{{\mathit{\theta}}^{\ast}}$
  When $P\left(x\right)=c$, we get Fisher information matrix

$$
{\left.{\mathbf{\nabla}}_{\bm{\theta}}^{2}J\left(\mathit{\theta}\right)\right|}_{{\mathit{\theta}}^{\ast}}\propto E\left[\bm{g}\left(\bm{x}\right)\bm{g}{\left(\bm{x}\right)}^{T}\right]=Var\left(score\left({\mathit{\theta}}^{\ast}\right)\right)
$$

  Larger variance, lesser information about $\mathit{\theta}$, higher uncertainty of $\mathit{\theta}$
  When ${\mathit{\theta}}^{\ast}$ is a good explanation of data, the region where data sit will have high probabilities(Maximum Likelihood), so ${\left.{\mathbf{\nabla}}_{\bm{\theta}}\mathrm{ln}{p}_{m}\left(x;\mathit{\theta}\right)\right|}_{{\mathit{\theta}}^{\ast}}$ on different $x$ in data won't far from each other(all are flat in infinitesimal neighbor around ${\mathit{\theta}}^{\ast}$), leading to small variance of score
Proof:
  That equivalent to prove

$$
P\left(\left|{\widehat{\mathit{\theta}}}_{T}-{\mathit{\theta}}^{\ast}\right|\ge \mathit{\epsilon}\right)=0,\ \ T\to \infty 
$$

  The basic idea is to prove its upper bound convergent to 0 in probability too
  In order to make (2) come into handy, we also need to transform the predicate into similar form

**Application on Logistic Regression**  
Samples of NCE generated from mixture of two probability distributions, one is real distribution ${\mathrm{P}}_{train}$ where training data were sampled, the other is artifact noise distribution $\mathrm{Q}$.
Note that in NLP, sampling from $\mathrm{Q}$ can be done by randomly replacing words in scentence.  
**Sampling process**  

$$
{w}_{i}~{P}_{train},\ \ {\stackrel{~}{w}}_{i1},{\stackrel{~}{w}}_{i2}\dots {\stackrel{~}{w}}_{ik}~Q.i.i.d
$$

Joint distribution conditioned on label

$$
p\left(y,w|c\right)=y\frac{1}{k+1}{P}_{train}\left(w|c\right)+\left(1-y\right)\frac{k}{k+1}Q\left(w\right)
$$

Objective: log-likelihood

$$
{J}_{\mathit{\theta}}=-{\sum}_{{w}_{i}\in V}\left[logP\left(y=1|{w}_{i},{c}_{i}\right)+k{E}_{{\stackrel{~}{w}}_{ik}~Q}\left[\mathrm{log}P\left(y=0|{\stackrel{~}{w}}_{ik},{c}_{i}\right)\right]\right]
$$

According to Monte Carlo

$$
{J}_{\mathit{\theta}}=-{\sum}_{{w}_{i}\in V}\left[\mathrm{log}P\left(y=1|{w}_{i},{c}_{i}\right)+{\sum}_{j=1}^{k}\mathrm{log}P\left(y=0|{\stackrel{~}{w}}_{ij},{c}_{i}\right)\right]
$$

where

$$
P\left(y|w,c\right)=\frac{p\left(y,w|c\right)}{p\left(w|c\right)}=\frac{p\left(y,w|c\right)}{{\sum}_{{y}^{\prime}}p\left({y}^{\prime},w|c\right)}\left\{\begin{array}{c}p\left(y=1,w|c\right)=\frac{1}{k+1}{P}_{train}\left(w|c\right)\\ p\left(y=0,w|c\right)=\frac{k}{k+1}Q\left(w\right)\end{array}\right.
$$

$$
\left\{\begin{array}{c}p\left(y=1|w,c\right)=\frac{\frac{1}{k+1}{P}_{train}\left(w|c\right)}{\frac{1}{k+1}{P}_{train}\left(w|c\right)+\frac{k}{k+1}Q\left(w\right)}=\frac{{P}_{train}\left(w|c\right)}{{P}_{train}\left(w|c\right)+kQ\left(w\right)}\\ p\left(y=0|w,c\right)=1-p\left(y=1|w,c\right)\end{array}\right.
$$

  where

$$
{P}_{train}\left(w|c\right)=softmax\left(w,c\right)=\frac{\mathrm{exp}\left({h}^{T}{v}_{w}^{\prime}\right)}{{\sum}_{{w}_{i}\in V}\mathrm{exp}\left({h}^{T}{v}_{{w}_{i}}^{\prime}\right)}
$$

Normalization factor can be automatically learned though optimization

$$
{P}_{train}\left(w|c\right)=\frac{\mathrm{exp}\left({h}^{T}{v}_{w}^{\prime}\right)}{Z\left(c\right)},Z\left(c\right)={\sum}_{{w}_{i}\in V}\mathrm{exp}\left({h}^{T}{v}_{{w}_{i}}^{\prime}\right)
$$

[Since auto-normalize is assured by NCE, there is no need of introduction of normalization factor, i.e. normalization will be automatically fulfilled by weights](https://www.ruder.io/word-embeddings-softmax/#noisecontrastiveestimation)  
Set $Z\left(c\right)=1$

$$
{P}_{train}\left(w|c\right)=\mathrm{exp}\left({h}^{T}{v}_{w}^{\prime}\right)\ \in \left[0,1\right]
$$

$$
\Rightarrow p\left(y=1|w,c\right)=\frac{\mathrm{exp}\left({h}^{T}{v}_{w}^{\prime}\right)}{\mathrm{exp}\left({h}^{T}{v}_{w}^{\prime}\right)+kQ\left(w\right)}
$$

$$
\Rightarrow {J}_{\mathit{\theta}}=-{\sum}_{{w}_{i}\in V}\left[\mathrm{log}\frac{\mathrm{exp}\left({h}^{T}{v}_{{w}_{i}}^{\prime}\right)}{\mathrm{exp}\left({h}^{T}{v}_{{w}_{i}}^{\prime}\right)+kQ\left({w}_{i}\right)}+{\sum}_{j=1}^{k}\mathrm{log}\frac{kQ\left({\stackrel{~}{w}}_{ij}\right)}{\mathrm{exp}\left({h}^{T}{v}_{{\stackrel{~}{w}}_{ij}}^{\prime}\right)+kQ\left({\stackrel{~}{w}}_{ij}\right)}\right]
$$

Gradient of NCE will converge to Softmax, as k approaching to size of vocabulary

$$
{J}_{\mathit{\theta}}=-{\sum}_{{w}_{i}\in V}[-\mathcal{E}\left({w}_{i}\right)-\mathrm{log}\left(\mathrm{exp}\left(-\mathcal{E}\left({w}_{i}\right)\right)+kQ\left({w}_{i}\right)\right)+{\sum}_{j=1}^{k}\mathrm{log}kQ\left({\stackrel{~}{w}}_{ij}\right)-\mathrm{log}\left(\mathrm{exp}\left({h}^{T}{v}_{{\stackrel{~}{w}}_{ij}}^{\prime}\right)+kQ\left({\stackrel{~}{w}}_{ij}\right)\right)]\ 
$$

$$
{\nabla}_{\mathit{\theta}}{J}_{\mathit{\theta}}=-{\sum}_{{w}_{i}\in V}\left[-{\nabla}_{\mathit{\theta}}\mathcal{E}\left({w}_{i}\right)+\frac{\mathrm{exp}\left(-\mathcal{E}\left({w}_{i}\right)\right){\nabla}_{\mathit{\theta}}\mathcal{E}\left({w}_{i}\right)}{\mathrm{exp}\left(-\mathcal{E}\left({w}_{i}\right)\right)+kQ\left({w}_{i}\right)}+{\sum}_{j=1}^{k}\frac{\mathrm{exp}\left(-\mathcal{E}\left({\stackrel{~}{w}}_{ij}\right)\right){\nabla}_{\mathit{\theta}}\mathcal{E}\left({\stackrel{~}{w}}_{ij}\right)}{\mathrm{exp}\left(-\mathcal{E}\left({\stackrel{~}{w}}_{ij}\right)\right)+kQ\left({\stackrel{~}{w}}_{ij}\right)}\right],
$$

$$
\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ k\to \left|V\right|-1
$$

$$
\Rightarrow {\sum}_{{w}_{i}\in V}\left[{\nabla}_{\mathit{\theta}}\mathcal{E}\left({w}_{i}\right)-{\sum}_{{w}_{j}\in V}\frac{\mathrm{exp}\left(-\mathcal{E}\left({w}_{j}\right)\right){\nabla}_{\mathit{\theta}}\mathcal{E}\left({w}_{j}\right)}{\mathrm{exp}\left(-\mathcal{E}\left({w}_{j}\right)\right)+kQ\left({w}_{j}\right)}\right],
$$

$$
\frac{\mathrm{exp}\left(-\mathcal{E}\left({\mathrm{w}}_{\mathrm{j}}\right)\right)}{\mathrm{exp}\left(-\mathcal{E}\left({w}_{j}\right)\right)+kQ\left({w}_{j}\right)}=p\left(y=1|{w}_{j},c\right)
$$

$$
\Rightarrow {\sum}_{{w}_{i}\in V}\left[{\nabla}_{\mathit{\theta}}\mathcal{E}\left({w}_{i}\right)-{E}_{{w}_{j}~p}\left[{\nabla}_{\mathit{\theta}}\mathcal{E}\left({w}_{j}\right)\right]\right]
$$

**Comparison between NCE and GAN**  
From paper "ON DISTINGUISHABILITY CRITERIA FOR ESTIMATING GENERATIVE MODELS"
1. A modified version of NCE with dynamic generator is equivalent to MLE
That was proved by considering extreme case where the model is copied as new noise distribution at each step of learning, which was called SCE, and results show that SCE has same expected gradient as MLE
2. The existing theoretical work on GANs does not guarantee convergence on practical applications
That is mainly a results from optimizing in non-convex case
(i) mechanism of min-max optimization fails in [non-convex case](onenote:#Convex%20Optimization&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={EC2F328D-F4C1-4EE8-B893-8EE9ACD0103F}&object-id={05C97FFE-A206-0ED5-2623-1BE375DBAAEE}&D&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one) where minimizing lower bound is not guarantee minimization of its supreme.
(ii) Non-convergence of gradient-based learning (waiting for more testify)
3. Because GANs do the model estimation in the generator network, they cannot recover maximum likelihood using same objective of NCE
MLE form of gradient

$$
\underset{{p}_{m}}{\mathrm{max}}{E}_{x~{p}_{d}}\left[\mathrm{log}{p}_{c}\left(y=1|x\right)\right]\Rightarrow \underset{{p}_{m}}{\mathrm{max}}{E}_{x~{p}_{d}}\left[\mathrm{log}{p}_{c}\left(y=0|x\right)\right]
$$

$$
\Rightarrow {\mathrm{E}}_{x~{p}_{d}}\left[{\nabla}_{\mathit{\theta}}\mathrm{log}{p}_{g}\left(x\right)\right]
$$

Adjust GAN gradient into MLE form

$$
\underset{{p}_{g}}{\mathrm{min}}{E}_{x~{p}_{g}}\left[\mathrm{log}{p}_{c}\left(y=0|x\right)\right]
$$

$$
\Rightarrow -{\mathrm{E}}_{x~{p}_{g}}\left[f\left(x\right){\nabla}_{\mathit{\theta}}\mathrm{log}{p}_{g}\left(x\right)\right],\ \ f\left(x\right)=\mathrm{log}{p}_{c}\left(y=0|x\right)
$$

  Turn into maximum likelihood derivatives

$$
\Rightarrow {\mathrm{E}}_{x~{p}_{d}}\left[{\nabla}_{\mathit{\theta}}\mathrm{log}{p}_{g}\left(x\right)\right],\ \ f\left(x\right)=-\frac{{p}_{d}\left(x\right)}{{p}_{g}\left(x\right)}
$$

  The discriminator can provide necessary information for computing maximum likelihood derivatives

$$
{\mathrm{p}}_{c}\left(y=1|x\right)=\mathit{\sigma}\left(a\left(x\right)\right)=\frac{{p}_{d}\left(x\right)}{{p}_{d}\left(x\right)+{p}_{g}\left(x\right)}\Rightarrow a\left(x\right)=\mathrm{ln}\frac{{p}_{d}\left(x\right)}{{p}_{g}\left(x\right)}
$$

$$
\Rightarrow f\left(x\right)=-\mathrm{exp}\left(a\left(x\right)\right)
$$

  But this is different from the value given by distinguishability game

$$
f\left(x\right)=-\mathit{\zeta}\left(a\left(x\right)\right)=-\mathrm{log}\left(1+\mathrm{exp}\left(a\left(x\right)\right)\right)=\mathrm{log}{p}_{c}\left(y=0|x\right)
$$

$$
\mathrm{i}.\mathrm{e}.\ {E}_{x~{p}_{g}}\left[\mathrm{log}{p}_{c}\left(y=0|x\right)\right]\ in\ \mathrm{V}\left({p}_{c},{p}_{g}\right)
$$

  If we replace $f\left(x\right)$ satisfying MLE form back in objective, we can never hold a distinguishability game.

Preliminary:
  ${\mathrm{p}}_{d}$: the underlying data distribution
  ${\mathrm{p}}_{m}$: distribution modeled to reconstruct ${\mathrm{p}}_{d}$
  ${\mathrm{p}}_{g}$: generator in GAN, also noise distribution in NCE  
Both method are primarily driven by *distinguishability game value function:*

$$
\mathrm{V}\left({p}_{c},{p}_{g}\right)={E}_{x~{p}_{d}}\left[\mathrm{log}{p}_{c}\left(y=1|x\right)\right]+{E}_{x~{p}_{g}}\left[\mathrm{log}{p}_{c}\left(y=0|x\right)\right]
$$

  Where

$$
{p}_{c}\left(y=1|x\right)=\frac{{p}_{m}\left(x\right)}{{p}_{m}\left(x\right)+{p}_{g}\left(x\right)}\ or\ \frac{{p}_{d}\left(x\right)}{{p}_{d}\left(x\right)+{p}_{g}\left(x\right)}
$$

But they have different learning targets
For NCE:

$$
\underset{{p}_{m}}{\mathrm{max}}V\left({p}_{c},{p}_{g}\right)\equiv \underset{{p}_{m}}{\mathrm{max}}{E}_{x~{p}_{d}}\left[\mathrm{log}{p}_{c}\left(y=1|x\right)\right],\ \ {p}_{g}\ is\ fixed
$$

  Convergent on optimal where

$$
{p}_{m}\left(x\right)={p}_{d}\left(x\right),\ if\ {p}_{d}\left(x\right)\in \left\{{p}_{m}\left(x;\mathit{\theta}\right)\right\}
$$

  i.e. NCE works by learning in the discriminator(via a generative model that is used to implicitly define the generator), maximizing acceptance rate of samples sampled from target distribution
For GAN:

$$
V\left(D,G\right)={E}_{x~{p}_{d}}\left[\mathrm{log}D\left(x\right)\right]+{E}_{x~{p}_{g}}\left[\mathrm{log}\left(1-D\left(G\left(x\right)\right)\right)\right]
$$

$$
\underset{G}{\mathrm{min}}\underset{D}{\mathrm{max}}V\left(D,G\right)\equiv \underset{{p}_{g}}{\mathrm{min}}{E}_{x~{p}_{g}}\left[\mathrm{log}{p}_{c}\left(y=0|x\right)\right]
$$

  Convergent on optimal where
     ${p}_{g}\left(x\right)={p}_{d}\left(x\right),\ if\ V\left(D,G\right)$ is convex function
  i.e. GAN works by learning in the generator, minimizing rejection rate of samples generated from generator
