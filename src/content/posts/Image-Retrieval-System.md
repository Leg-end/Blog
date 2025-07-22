---
title: "Image Retrieval System"
published: 2023-07-06
description: "Structurize and Retrieval"
tags: ["Approximate KNN", "Google Landmark"]
category: Retrieval
draft: false
---

Given a query image, we need to find out its matching images from database.
This was done by doing KNN matching on feature descriptors between query image and database images.
So the Image Retrieval System's core job is gather close item into cluster, let each item close to its nearest neighbor. Then scope of search can be narrowed down so as to locate matching item more quickly. This is constructing structural index of vectors.

Description Framwork  
![image1](resources/39b77d1613104549aedbd3c6025ed33f.png)
1.  Covariant regions of interest are detected and described by a local d-dimension descriptor.(e.g. SIFT)
![image2](resources/ea22bdfca1ff468181a26fcd8d025832.png)
2.  Quantize these local descriptors by coarse quantizer.
![image3](resources/5c909f712fdc4e0d9082102f2da20f2c.png)
3.  Histogram of descriptors falling in different(total K) Voronoi cells yields the global descriptor with dimension K(count in each cell). Then weighted it with [inverse document frequency](https://www.jianshu.com/p/f70d3dba74cc).  
![image4](resources/3913cf18063147f59c2ed490027a1bf0.png)
4.  Normalization  
![image5](resources/225c805f5ff148e9b426ca000a1d3088.png)  
From paper "**Negative evidences and co-occurrences in image retrieval: the benefit of PCA and whitening**"
Advance 1: dimensionality reduction using PCA  
co-occurrence cause Dim1 has intersection with Dim2, i.e. there exist data only depend on Dim 1, but when we treat each dim as independent, we will over-counting the intersection region. That's why de-correlation is important with the role that PCA plays.
Advance 2: co-missing also matters  
![image6](resources/c97a828a065f45e4929ef57263103d9b.png)

![image7](resources/cd0ec3567cc241dcaf0a9feb15b0b81f.png)

vectors with component both 0 also provide useful information when matching. By centralizing vectors, 0 term turns into negative, then becomes positive term in dot product.

![image8](resources/8a62803eb5834362992c6d46422906fe.png)

![image9](resources/4110ffb6c2414db3ab47ce3ea4d4eee6.png)
Advance 3: enhance vector's represent richness by concatenate multiple quantization  
![image10](resources/6cc2c83d95c24db18353ac8cb2e79e17.png)

![image11](resources/b66442dae6ec425ab9592166953e02cf.png)

after concatenation, PCA is applied to get rid of high correlation among quantizers.

Retrival Framework
represent vector as (coarse quantizer, fine quantizer)
1.  coarse quantizer
Divide database into different clusters(Voronoi cells) by k-mean

![image12](resources/813bfdb7a8f74c91a162e440bc8ca6d1.png)

![image13](resources/67eb11ea7c1640a28059815ab62f7524.png)

K centroids will be store in Inverted file

![image14](resources/7a00c166a03e47409304a129f9c75508.png)

2.  for each cluster, do fine quantizer
(Or hierarchically)Split Voronoi cell into many small blocks and code them

1.  From paper "**Hamming embedding and weak geometric consistency for large scale image search**"  
![image15](resources/510a75006a3f4c56b933d5ea2e1cf76c.png)

![image16](resources/d00c8c11ce7c417d891970da2b1c1ce3.png)

Step 1: Orthogonal Projection

![image17](resources/b0bcdc6d59fa4ee58258b8972ae904ad.png)

Step 2: median divider for each dimension k

![image18](resources/5f861f77f3064cf08b8ebe46789842ba.png)

Step 3: computing the code for dimension k

![image19](resources/3af4f7098cea46bb9cf7bed685acf741.png)

![image20](resources/8e2c2b5c949c48c493086c0c6d4dc13c.png)

Step 4: compute Hamming distance

![image21](resources/35f7c54188c44dd9b4fed5ef791ef15d.png)

Question: there exist the case NNs in the Euclidean space have its Hamming distance is not small, e.g. 2 dim, we can divide a cell into 4 quadrants according to median, so only points fall in the same quadrant are NNs.

since we can not ensure point (0, 0) in data, so there may be NNs scatter on diagonal line, resulting in falling into different quadrants.

Briefly, similar issue to k-mean, NNs in Euclidean space fall on the two side of border become non-NN. Which can be solved by searching multiple cells at same time, nprobe parameter in faiss

2.  From paper "**Product quantization for nearest neighbor search**"  
In contrast to method 1), which is a flat way of finer quantization, the method here is a hierarchical one.

Do product quantization on residual vector (vector - centroid), that is doing vector quantization for each sub vector of residual vector. Then represent each sub vector with its sub voronoi cell code.

![image22](resources/be0de7c5a71d4d47896b1cd20c762e64.png)

![image23](resources/e5fa8c3262d848f7bfe00de2cff33a21.png)

![image24](resources/5f8f8afe2d834d328494acd5798b4694.png)

Database indexing

Get residual vector and its m sub vectors, d % m=0

![image25](resources/7a091961950c49a0827ecb105741b380.png)

![image26](resources/1ae4e4dc5d594fb7b60d654fc842d5df.png)

![image27](resources/fd92c6ffc26444f0aa01cdab6bdc22a2.png)

![image28](resources/c6f8841cbb4e48c1a1672bf5a7661f1c.png)

Finer quantizer

![image29](resources/c0858d2094a4435683f0a39713b7b67d.png)

![image30](resources/e8a6e1803cd64dcab4cf04522e478592.png)

![image31](resources/92fbabc51ac0411db729c68aa90c4efc.png)

![image32](resources/904a96fcf2c84847b757c8391c863bf6.png)

Represent in binary form

![image33](resources/67568295635d4131bc5d550cf6216ff5.png)

indexed vector

![image34](resources/2fc982f34bdc4766b0d5010608c4414c.png)

![image35](resources/dc1686d331444785aed340aa2acad9cb.png)

![image36](resources/d4b589b8f88b47cd95f91cc20fdb1c7f.png)

![image37](resources/29a6705dc81446b7a0e194a968317cb0.png)

Query process

![image38](resources/1280675676e647cab13d8e715b78d13e.png)

![image39](resources/6462840770d0457391969f76521cfc57.png)

![image40](resources/11a218020964427fac51494a717bb13c.png)

![image41](resources/e970c03243234a1d90a72cc0e65e8fb8.png)

![image42](resources/b269026ecc88440681e2ed6ad8091c0a.png)

![image43](resources/a01de4673a9a4fa386e732d90635a85d.png)

3.  From paper "**Large-Scale Image Retrieval with Attentive Deep Local Features**", i.e. 1) + 2)  
Step 1: Voronoi cell partition

This was done by applying **K-D Tree** algorithm to hierarchically split Voronoi cell into blocks

Step 2: Locally optimized **Product Quantizer**

Then apply **Product Quantizer** for each sub tree of K-D Tree

Provided: dim sequence DS (which dim should be first split)

This dim sequence was built base on picking dimension with maximum variance at each depth.

Then it can filter lots points that are quite far from query from the start, since the gap on that dimension is sufficiently large to be distinguished.

Search processing of K-D Tree:
```
Pseudocode:

\# following the searching trajectory from coarse to finer cell hierarchically,

\# ordered by dim sequence, we'll finally reach the nearest point

min = d(root, query); i = 1 \# record current minimum distance

dim = DS\[i\]

if (query\[dim\] \< root\[dim\]) \# go to which branch

dim = DS\[i+1\]

if (\|query\[dim\] - root.lchid\[dim\]\| \> min)

return root

else

tmp = d(query, root.lchid)

if (tmp \> min) return root

min = tmp

root = root.lchild; i += 1

repeat this process

else

dim = DS\[i+1\]

if (\|query\[dim\] - root.rchid\[dim\]\| \> min)

return root

else

tmp = d(query, root.rchid)

if (tmp \> min) return root

min = tmp

root = root.rchild; i += 1

repeat this process
```
3.  search  
![image44](resources/4d8409f2ca4747c1aaef5664eca3f016.png)

![image45](resources/be6d832c80574450b154076e77d921a8.png)

![image46](resources/7c6c09a8d1824e18a89e181a779f1e53.png)

![image47](resources/7fdc2ab844e448c8872466eb159995b3.png)

![image48](resources/8c76474e66ec4ee88a5e0c45cb08faf6.png)

![image49](resources/8a4e6de8732744a38334a3e7eeff28c3.png)

![image50](resources/57e8daa2509f4f0c90223106b5b04bd5.png)

From Step 1 to 2, we quickly narrow down search scope, and then at Step 3, we accurately locate matching items.

e.g. For Face Recognition, we may narrow search scope by coarse quantization such as style of face, then exactly matching between face feature vectors in an efficiency small realm.
