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
1.  Psychology and neurobiology
What features and statistics are the basic elements in human texture perception?

\(i\) the basic texture statistics
2.  Mathematics and statistics
Given a set of consistent statistics, how do we generate random texture images with the identical statistics?

\(ii\) a method for mixing the exactly amount of statistics in a given recipe

**Juesz ensemble**  
*"The visual system discriminates between different textures based on the average responses of certain image filters" by Julesz*  
Definition of texture  
A family of visual pattern that share certain local statistical regularities.  
![image1](resources/57ec24e9bb2547a49cf68b5b1e46925a.png)
![image2](resources/eeb410a863d343b488fc64cfff84d969.png)
![image3](resources/d17648e3614a4c5f9a1fb550de0c1dbf.png)
![image4](resources/49a86498e02144db8e621b9b61786d73.png)
![image5](resources/e8e4eb617b924b68ae483715b4ef0eff.png)
![image6](resources/fd3d34334cdc44caadce9adb4c81c7f1.png)
![image7](resources/bb0a740ef1f74178810f5ab662cf4ddb.png)
![image8](resources/a47520fcb97a4a42a12313b04d2ba332.png)
![image9](resources/6ef6ab4fd42b419b9bb9b6ac78fc3569.png)

![image10](resources/05b9655b1142488ab765c1ec788134e8.png)

![image11](resources/4ea1cf393fcf4e90bb56e9a4e9fffef0.png)

![image12](resources/e6df344c816b4962beafc42a2625b4e2.png)

![image13](resources/b1ac6ac044e649089e06614e19364c2c.png)

![image14](resources/4ae4f81212774975be8d8ec186e19e15.png)

![image15](resources/b994ff5650b1445a8be4f860d51976f2.png)

![image16](resources/275e1727c790497d9df5cb4533e91c32.png)

**Texture Generation**  
Learn network that draw samples from the Julesz ensemble modeling a texture
1.  Generation-by-minimization  
![image17](resources/8cd741d7d561495bb1247acea6696b1c.png)  
2.  Generation-by-sampling  
![image18](resources/90323ebce91444e5b66018c315dddc0f.png)  
3.  Maximum Mean Discrepancy  
![image19](resources/0db34546eedc4627b5dfb40cfae64c20.png)

![image20](resources/362432dc55a34d169cd081a8e6eb90b4.png)  
4.  GAN

**Style Transfer**  
Indicators: visual fidelity and diversity
Generate image has style close to style image and content close to content image
1.  Stylization-by-optimization  
![image21](resources/36063e875c1743ecb8198d1e2add1a7e.png)

![image22](resources/5157c333af974ba38497e0156e31794e.png)

e.g. paper "Image Style Transfer Using Convolution Neural Networks"
2.  Stylization by feed-forward generator network  
For specific style

![image23](resources/99702a8e0b27438a9641acc927300a5d.png)  
3.  Stylization by sampling
Paper "Improved Texture Networks: Maximizing Quality and Diversity in feed-forward Stylization and Texture Synthesis"

![image24](resources/e3934a7d65cf40cf890f05c43e9c9d09.png)

![image25](resources/fb312f46272c4392b2ab5c5ed11da90a.png)

![image26](resources/77f4f8fcae974706820e276b1a3709e6.png)

The first term measures visual fidelity, the second term measures diversity(large T)

From TetureNetV1 "*In fact, our qualitative results degraded using too many example images.*"

![image27](resources/41763e9dcf02414995d3458fb332ff94.png)

The explain is quite obscure, but we can focus on filter applied in convolution and batch normalization following.

Since only these operations are applied on multiple example images.

\(1\) Filters: Note that a specific filter only active to a specific pattern, or local structure,

With larger batch size, the more variate proportion of same local structure in a content image will be, but such variation is randomness, since our batch samples are randomly chosen, and style objective is measured by filter responses from multiple image examples and one style image, it would be so hard for filter to match all response from different content images with variate proportions of same local structure to a response from style image "where structures exist in a fixed arbitrary proportion"

\(2\) Batch Normalization: The key difference between batch normalization and

Instance(contrast) normalization is the average along batch dimension.

As discussed in TextureV2

![image28](resources/d8800b7b67584307b3f39bc556cd707c.png)

The variate proportions of same local structure in different content images may result from different contrast in different images, since contrast is the difference in luminance or color that makes an object distinguishable from other objects within the same field of view, resulting the diversity of content images.

Since images in a batch have their content quite far away from each other, the BN may only discard contrast information they share, which maybe variate from batch to batch, the remain diversity part still affect the process of stylization, i.e. the filter is struggling in between contrast of content images and style image.

Extra gain from Instance normalization (by discarding contrast information of content image)  
4.  GAN
