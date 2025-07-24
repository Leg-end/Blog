---
title: Style Transfer
published: 2023-09-24
description: "Early related works of style transfer"
tags: ["Gmm matrix", "Instance normalization"]
category: Generative-Models
draft: false
---

**Fundamental question to texture**  
  *"What features and statistics are characteristic of a texture pattern, so that texture pairs that share the same features and statistics cannot be told apart by pre-attentive human visual perception" by Julesz*

**Major challenges of texture modeling**  
1. Psychology and neurobiology
What features and statistics are the basic elements in human texture perception?
(i) the basic texture statistics
2. Mathematics and statistics
Given a set of consistent statistics, how do we generate random texture images with the identical statistics?
(ii) a method for mixing the exactly amount of statistics in a given recipe

**Juesz ensemble**  
  *"The visual system discriminates between different textures based on the average responses of certain image filters" by Julesz*
Definition of texture
  A family of visual pattern that share certain local statistical regularities.

$$
\mathrm{image}\ x:\mathrm{\Omega}\to {R}^{3},\ \ \mathrm{\Omega}=\left\{1,\dots ,H\right\}\times \left\{1,\dots ,W\right\},x\in X
$$

local statistical , response of filter ${F}_{l}:\mathcal{X}\times \mathrm{\Omega}\to R,\ \ l=1,\dots ,L$
  $\mathrm{e}.\mathrm{g}.\ {F}_{l}\left(x,u\right)$, response at location u on image x

$$
\mathrm{characteristic}\ {\mathit{\mu}}_{l}\left(x\right)=\frac{1}{\left|\mathrm{\Omega}\right|}{\sum}_{u\in \mathrm{\Omega}}{F}_{l}\left(x,u\right)
$$

$$
\mathrm{Julesz}\ \mathrm{ensemble}\ {\mathcal{T}}_{\mathit{\epsilon}}=\left\{x\in \mathcal{X}:\mathcal{L}\left(x\right)\le \mathit{\epsilon}\right\},\ \ \mathcal{L}\left(x\right)={\sum}_{l=1}^{L}{\left({\mathit{\mu}}_{l}\left(x\right)-{\stackrel{-}{\mathit{\mu}}}_{l}\right)}^{2}
$$

  i.e. texture images that share same statistics(characteristic) ${\stackrel{-}{\mathit{\mu}}}_{l}$

$$
\mathrm{texture}\ p\left(x\right)=\left\{\begin{array}{c}\frac{{e}^{-\frac{\mathcal{L}\left(x\right)}{T}}}{\underset{y\in {\mathcal{T}}_{\mathit{\epsilon}}}{\int}{e}^{-\frac{\mathcal{L}\left(y\right)}{T}}dy},\ \ x\in {\mathcal{T}}_{\mathit{\epsilon}}\\ 0,\ \ otherwise\end{array}\right.,\ \ T>0
$$

Induction of matrix form of $\mathcal{L}\left(x\right)$  

$$
\bm{F}=\left({F}_{1},\dots ,{F}_{L}\right)
$$

$$
\stackrel{-}{\bm{\mu}}=\left({\stackrel{-}{\mathit{\mu}}}_{1},\dots ,{\stackrel{-}{\mathit{\mu}}}_{L}\right)
$$

$$
\bm{\mu}\left(x\right)=\left({\mathit{\mu}}_{1}\left(x\right),\dots ,{\mathit{\mu}}_{L}\left(x\right)\right)
$$

$$
=\frac{1}{\left|\mathrm{\Omega}\right|}\left[1,\dots ,1\right]\left[\begin{array}{ccc}{F}_{1}\left(x,{u}_{1}\right)& \dots & {F}_{L}\left(x,{u}_{1}\right)\\ \vdots & \ddots & \vdots \\ {F}_{1}\left(x,{u}_{\left|\mathrm{\Omega}\right|}\right)& \dots & {F}_{L}\left(x,{u}_{\left|\mathrm{\Omega}\right|}\right)\end{array}\right]
$$

$$
=\frac{1}{\left|\mathrm{\Omega}\right|}{\sum}_{u\in \mathrm{\Omega}}\bm{F}\left(u\right)
$$

$$
\mathcal{L}\left(x\right)={\left(\bm{\mu}\left(x\right)-\stackrel{-}{\bm{\mu}}\right)\left(\bm{\mu}\left(x\right)-\stackrel{-}{\bm{\mu}}\right)}^{T}
$$

$$
=\frac{1}{{\left|\mathrm{\Omega}\right|}^{2}}{\sum}_{u\in \mathrm{\Omega}}\left(\bm{F}\left(u\right)-\stackrel{-}{\bm{\mu}}\right){\sum}_{u\in \mathrm{\Omega}}{\left(\bm{F}\left(u\right)-\stackrel{-}{\bm{\mu}}\right)}^{T}
$$

$$
=\frac{1}{{\left|\mathrm{\Omega}\right|}^{2}}{\sum}_{i,j=1}^{\left|\mathrm{\Omega}\right|}\left(\bm{F}\left({u}_{i}\right)-\stackrel{-}{\bm{\mu}}\right){\left(\bm{F}\left({u}_{j}\right)-\stackrel{-}{\bm{\mu}}\right)}^{T}
$$

$$
=\frac{1}{{\left|\mathrm{\Omega}\right|}^{2}}{\sum}_{i,j=1}^{\left|\mathrm{\Omega}\right|}{\sum}_{l=1}^{L}\left({F}_{l}\left({u}_{i}\right)-{\stackrel{-}{\mathit{\mu}}}_{l}\right)\left({F}_{l}\left({u}_{j}\right)-{\stackrel{-}{\mathit{\mu}}}_{l}\right)
$$

**Texture Generation**  
Learn network that draw samples from the Julesz ensemble modeling a texture
1. Generation-by-minimization

$$
{x}^{\ast}=\underset{x\in \mathcal{X}}{\mathrm{argmin}}\mathcal{L}\left(x\right)
$$

2. Generation-by-sampling

$$
{g}^{\ast}=\underset{g}{\mathrm{argmin}}{E}_{z~p\left(z\right)}\left[\mathcal{L}\left(g\left(z\right)\right)\right]
$$

3. Maximum Mean Discrepancy

$$
{g}^{\ast}=\underset{g}{\mathrm{argmin}}\left|{E}_{z~p\left(z\right)}\left[{\mathit{\phi}}_{\mathit{\alpha}}\left(g\left(z\right)\right)\right]-{E}_{x~p\left(x\right)}\left[{\mathit{\phi}}_{\mathit{\alpha}}\left(x\right)\right]\right|
$$

 ${\mathit{\phi}}_{\mathit{\alpha}}\left(x\right)$ is statistic, $p\left(x\right)$ can be described by ${E}_{x~p\left(x\right)}\left[{\mathit{\phi}}_{\mathit{\alpha}}\left(x\right)\right]$
4. GAN  

**Style Transfer**  
Indicators: visual fidelity and diversity
Generate image has style close to style image and content close to content image
1. Stylization-by-optimization

$$
x\u2254x-\mathit{\lambda}\left(\frac{\mathit{\partial}\left(\mathit{\alpha}{\mathcal{L}}_{content}\left(x,{x}_{c}\right)+\mathit{\beta}{\mathcal{L}}_{style}\left(x,{x}_{s}\right)\right)}{\mathit{\partial}x}\right)
$$

 $x$ can be random noise or copy of content image
e.g. paper "Image Style Transfer Using Convolution Neural Networks"
2. Stylization by feed-forward generator network
For specific style

$$
{g}^{\ast}=\underset{g}{\mathrm{argmin}}{E}_{{x}_{c}~p\left({x}_{c}\right),z~p\left(z\right)}\left[{\mathcal{L}}_{style}\left(g\left({x}_{c},z\right)\right)+\mathit{\alpha}{\mathcal{L}}_{content}\left(g\left({x}_{c},z\right),{x}_{c}\right)\right]
$$

3. Stylization by sampling
Paper "Improved Texture Networks: Maximizing Quality and Diversity in feed-forward Stylization and Texture Synthesis"

$$
\underset{q}{\mathrm{argmin}}KL\left(q\left|\right|p\right)
$$

$$
KL\left(q\left|\right|p\right)\propto \frac{1}{T}{E}_{{x}_{c}~p\left({x}_{c}\right),x~q\left(x\right)}\left[\mathcal{L}\left(x\right)+\mathit{\alpha}{\mathcal{L}}_{content}\left(x,{x}_{c}\right)\right]-H\left(q\right)
$$

$$
{E}_{{x}_{c}~p\left({x}_{c}\right),x~q\left(x\right)}\left[\mathcal{L}\left(x\right)+\mathit{\alpha}{\mathcal{L}}_{content}\left(x,{x}_{c}\right)\right]
$$

$$
={E}_{{x}_{c}~p\left({x}_{c}\right),z~\mathcal{N}\left(0,I\right)}\left[\mathcal{L}\left(g\left({x}_{c},z\right)\right)+\mathit{\alpha}{\mathcal{L}}_{content}\left(g\left({x}_{c},z\right),{x}_{c}\right)\right]
$$

The first term measures visual fidelity, the second term measures diversity(large T)

From TetureNetV1 "*In fact, our qualitative results degraded using too many example images.*"
Author speculate that "*stylization by a convolutional architecture uses local operations; since the same local structures exist in different combinations and proportions in different natural images y, it is difficult for local operators to match in all cases the overall statistics of the reference texture *${x}_{0}$*, where structures exist in a fixed arbitrary proportion*"  
The explain is quite obscure, but we can focus on filter applied in convolution and batch normalization following.
Since only these operations are applied on multiple example images.  
(1) Filters: Note that a specific filter only active to a specific pattern, or local structure,  
  With larger batch size, the more variate proportion of same local structure in a content image will be, but such variation is randomness, since our batch samples are randomly chosen, and style objective is measured by filter responses from multiple image examples and one style image, it would be so hard for filter to match all response from different content images with variate proportions of same local structure to a response from style image "where structures exist in a fixed arbitrary proportion"  
(2) Batch Normalization: The key difference between batch normalization and  
  Instance(contrast) normalization is the average along batch dimension.
  As discussed in TextureV2
  "*A simple observation that may make learning simpler is that the result of stylization should not, in general, depend on the contrast of the content image but rather should match the contrast of the texture that is being applied to it. Thus, the generator network should discard contrast information in the content image *${x}_{0}$"  
  The variate proportions of same local structure in different content images may result from different contrast in different images, since contrast is the difference in luminance or color that makes an object distinguishable from other objects within the same field of view, resulting the diversity of content images.
  Since images in a batch have their content quite far away from each other, the BN may only discard contrast information they share, which maybe variate from batch to batch, the remain diversity part still affect the process of stylization, i.e. the filter is struggling in between contrast of content images and style image.

Extra gain from Instance normalization (by discarding contrast information of content image)  
4. GAN
