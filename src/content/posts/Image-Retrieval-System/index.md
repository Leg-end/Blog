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
Image $\to $ global description
1. Covariant regions of interest are detected and described by a local d-dimension descriptor.(e.g. SIFT)
Image $\to $ local descriptors
2. Quantize these local descriptors by coarse quantizer.
Images(from Database) $\to $ local descriptors $\to $ descriptor centroids
3. Histogram of descriptors falling in different(total K) Voronoi cells yields the global descriptor with dimension K(count in each cell). Then weighted it with [inverse document frequency](https://www.jianshu.com/p/f70d3dba74cc).
Local descriptors(from query) $\to $ global descriptor \* idf
4. Normalization
global descriptor \* idf $\to $ feature vector
From paper "**Negative evidences and co-occurrences in image retrieval: the benefit of PCA and whitening**"
Advance 1: dimensionality reduction using PCA
  co-occurrence cause Dim1 has intersection with Dim2, i.e. there exist data only depend on Dim 1, but when we treat each dim as independent, we will over-counting the intersection region. That's why de-correlation is important with the role that PCA plays.
Advance 2: co-missing also matters
  distance metric := dot product between feature vectors

$$
d\left(\bm{u},\bm{v}\right)={\bm{u}}^{\bm{T}}\bm{v}
$$

  vectors with component both 0 also provide useful information when matching. By centralizing vectors, 0 term turns into negative, then becomes positive term in dot product.

$$
\bm{v}:=\bm{v}-\bm{\alpha}\stackrel{-}{\bm{v}}
$$


$$
d\left(\bm{u},\bm{v}\right)={\left(\bm{u}-\bm{\alpha}\stackrel{-}{\bm{u}}\right)}^{T}\left(\bm{v}-\bm{\alpha}\stackrel{-}{\bm{v}}\right)
$$

Advance 3: enhance vector's represent richness by concatenate multiple quantization

$$
\bm{v}=\bm{P}\bm{C}\bm{A}\left(\left[{q}_{1}\left(\bm{v}\right),{q}_{2}\left(\bm{v}\right),\dots ,{q}_{N}\left(\bm{v}\right)\right]\right)
$$

  each ${q}_{i}$ is a quantizer with same or different number of centroids
  after concatenation, PCA is applied to get rid of high correlation among quantizers.

Retrival Framework
represent vector as (coarse quantizer, fine quantizer)
1. coarse quantizer
Divide database into different clusters(Voronoi cells) by k-mean

$$
q:{R}^{d}\to C,\ \ C:=\left\{{\bm{c}}_{\bm{i}};i\in I\right\},I=\left\{0,\dots ,k-1\right\}
$$


$$
{V}_{i}:=\left\{\bm{x}\in {R}^{d}:q\left(\bm{x}\right)={\bm{c}}_{\bm{i}}\right\}
$$

K centroids will be store in Inverted file

$$
IF:=\left\{<i,{\bm{c}}_{\bm{i}}>|i\in I,{\bm{c}}_{\bm{i}}\in C\right\}
$$

2. for each cluster, do fine quantizer
(Or hierarchically)Split Voronoi cell into many small blocks and code them
1) From paper "**Hamming embedding and weak geometric consistency for large scale image search**"
For each dimension, draw a line cross median(calculated from data) value of this dim and then split cell into two parts, part has values bigger than median will be coded as 1, otherwise 0. This will results in ${2}^{N}$ blocks, if with N dim, which requires N bits to code these blocks.
For Voronoi cell ${V}_{i}$
Step 1: Orthogonal Projection

$$
\bm{z}=\bm{P}\bm{x}=\left({z}_{1},{z}_{2},\dots ,{z}_{{d}_{b}}\right),\ \bm{P}\in {R}^{{d}_{b}\times d},{\bm{P}}^{\bm{T}}\bm{P}=\bm{I},\ \bm{x}\in {V}_{i}
$$

Step 2: median divider for each dimension k

$$
{\mathit{\tau}}_{q\left(\bm{x}\right),k}=median\left(\left\{{z}_{k}|\bm{x}\in {V}_{i}\right\}\right)
$$

Step 3: computing the code for dimension k

$$
{b}_{k}\left(\bm{x}\right)=\left\{\begin{array}{c}1,\ \ {z}_{k}>{\mathit{\tau}}_{q\left(\bm{x}\right),k}\\ 0,\ \ otherwise\end{array}\right.
$$


$$
b\left(\bm{x}\right)=\left({b}_{1}\left(\bm{x}\right),\dots ,{b}_{{d}_{b}}\left(\bm{x}\right)\right)
$$

Step 4: compute Hamming distance

$$
h\left(b\left(\bm{x}\right),b\left(\bm{y}\right)\right)={\sum}_{k=1}^{{d}_{b}}1-int\left({b}_{k}\left(\bm{x}\right)=={b}_{k}\left(\bm{y}\right)\right)
$$

  Question: there exist the case NNs in the Euclidean space have its Hamming distance is not small, e.g. 2 dim, we can divide a cell into 4 quadrants according to median, so only points fall in the same quadrant are NNs.
  since we can not ensure point (0, 0) in data, so there may be NNs scatter on diagonal line, resulting in falling into different quadrants.
  Briefly, similar issue to k-mean, NNs in Euclidean space fall on the two side of border become non-NN. Which can be solved by searching multiple cells at same time, nprobe parameter in faiss

2) From paper "**Product quantization for nearest neighbor search**"
In contrast to method 1), which is a flat way of finer quantization, the method here is a hierarchical one.
Do product quantization on residual vector (vector - centroid), that is doing vector quantization for each sub vector of residual vector. Then represent each sub vector with its sub voronoi cell code.
![](image_1.fe4e47bf.png)

$$
CodeBook\ C:=\left\{<i,{\bm{c}}_{\bm{i}}>|i\in I\right\}
$$


$$
CodeBook\ {C}_{i}:=\left\{<j,{\bm{c}}_{\bm{i}\bm{j}}>|j\in {I}_{i}\right\}\ of\ subvector\ i
$$

Database indexing
Get residual vector and its m sub vectors, d % m=0
So each sub vectors can be quantized into ${k}^{\ast}$ cell, the Dicar combination of ${k}^{\ast}$ cells in each part results in k cells

$$
{\bm{x}}^{\left(r\right)}=\bm{x}-q\left(\bm{x}\right),\ {\left({k}^{\ast}\right)}^{m}=k
$$


$$
{u}_{i}\left({\bm{x}}^{\left(r\right)}\right)=\left({x}_{\left(i-1\right)\ast \frac{d}{m}+1:i\ast \frac{d}{m}}^{\left(r\right)}\right)
$$


$$
{q}_{{p}_{i}}:{u}_{i}\left({R}^{d}\right)\to {C}_{i},\ \ {C}_{i}:=\left\{{c}_{ij};j=0,\dots ,{k}^{\ast}-1\right\}
$$

Finer quantizer

$$
{\bm{x}}^{\left(\bm{r}\right)}=\left({u}_{1}\left({\bm{x}}^{\left(\bm{r}\right)}\right),\dots ,{u}_{m}\left({\bm{x}}^{\left(\bm{r}\right)}\right)\right)\to \left[{q}_{{p}_{1}}\left({u}_{1}\left({\bm{x}}^{\left(\bm{r}\right)}\right)\right),\dots ,{q}_{{p}_{m}}\left({u}_{m}\left({\bm{x}}^{\left(\bm{r}\right)}\right)\right)\right]
$$


$$
\Rightarrow {q}_{p}:{u}_{1}\left({R}^{d}\right)\times {u}_{2}\left({R}^{d}\right)\times \dots \times {u}_{m}\left({R}^{d}\right)\to {C}_{1}\times {C}_{2}\times \dots \times {C}_{m}=C
$$

Here, each sub voronoi cell can be coded with $\left\lceil \log_2(k^*) \right\rceil$ bits

$$
{q}_{{p}_{i}}\left({u}_{i}\left({\bm{x}}^{\left(r\right)}\right)\right)={\bm{c}}_{ij}
$$

Represent in binary form

$$
{\mathrm{b}}_{\mathrm{i}}\left({\bm{c}}_{ij}\right)={\left(j\right)}_{2}\ \wedge \ \text{0x}\{1\}_{\left\lceil \log_2(k^*) \right\rceil}
$$

indexed vector

$$
b\left({\bm{x}}^{\left(r\right)}\right)=\left({b}_{1}\left({q}_{{p}_{1}}\left({u}_{1}\left({\bm{x}}^{\left(\bm{r}\right)}\right)\right)\right),\dots ,{b}_{m}\left({q}_{{p}_{m}}\left({u}_{m}\left({\bm{x}}^{\left(r\right)}\right)\right)\right)\right)
$$

This will introduce an inserted list for each Voronoi cell, indicated by codebook $C$

$$
IF:=\left\{<i,{\mathcal{L}}_{i}>|i\in I\right\}
$$


$$
{\mathcal{L}}_{i}:=\left\{<id,b\left({\bm{x}}^{\left(\bm{r}\right)}\right)>|\bm{x}\in {V}_{i},i\in I\right\},\ \ id\ is\ vector\ or\ image\ identifier
$$

Query process

$
query:=\bm{x}
$
$I^{\prime} = \arg\min_{k} \left\{ d\left(\bm{x}, \bm{c}_i\right)^2 \mid \bm{c}_i \in C \right\}$ \# locate coarse cells, k is nprob  
for i in ${I}^{\prime}$, get ${C}_{i},{\mathcal{L}}_{i}$ \# locate finer cells around ${{c}}_{{i}}$  
$
{\bm{x}}^{\left(\bm{r}\right)}=\bm{x}-{\bm{c}}_{\bm{i}}
$  
\# by comparing all finer residual code in cell ${{c}}_{{i}}$  
Maxheap($\left\{d{\left({\bm{x}}^{\left(\bm{r}\right)},{q}_{p}\left({\bm{y}}^{\left(\bm{r}\right)}\right)\right)}^{2}|b\left({\bm{y}}^{\left(\bm{r}\right)}\right)\in {\mathcal{L}}_{i}\right\}$)

3) From paper "**Large-Scale Image Retrieval with Attentive Deep Local Features**", i.e. 1) + 2)
```
Step 1: Voronoi cell partition
  This was done by applying **K-D Tree** algorithm to hierarchically split Voronoi cell into blocks
Step 2: Locally optimized **Product Quantizer**
  Then apply **Product Quantizer** for each sub tree of K-D Tree
  Provided: dim sequence DS (which dim should be first split)
    This dim sequence was built base on picking dimension with maximum variance at each depth.
    Then it can filter lots points that are quite far from query from the start, since the gap on that dimension is sufficiently large to be distinguished.
  Search processing of K-D Tree:
  Pseudocode:
    \# following the searching trajectory from coarse to finer cell hierarchically,
    \# ordered by dim sequence, we'll finally reach the nearest point
    min = d(root, query); i = 1 \# record current minimum distance
    dim = DS\[i\]
    if (query\[dim\] < root\[dim\]) \# go to which branch
      dim = DS\[i+1\]
      if (|query\[dim\] - root.lchid\[dim\]| > min)
        return root
      else
        tmp = d(query, root.lchid)
        if (tmp > min) return root
        min = tmp
        root = root.lchild; i += 1
        repeat this process
    else
      dim = DS\[i+1\]
      if (|query\[dim\] - root.rchid\[dim\]| > min)
        return root
      else
        tmp = d(query, root.rchid)
        if (tmp > min) return root
        min = tmp
        root = root.rchild; i += 1
        repeat this process
```

3. search
```
Give query x
Step 1: locate coarse quantization of x
  Find the top-k Voronoi cells that have minimal distance with x
Step 2: locate fine quantization of x
  For each neighborest Voronoi cell, find the top-k sub Voronoi cells that have minimal distance with x
Step 3: locate exact items(real item exists in database) match with x
  For each neighborest sub Voronoi cell, find the top-k items that have minimal distance with x
From Step 1 to 2, we quickly narrow down search scope, and then at Step 3, we accurately locate matching items.
e.g. For Face Recognition, we may narrow search scope by coarse quantization such as style of face, then exactly matching between face feature vectors in an efficiency small realm.
```
