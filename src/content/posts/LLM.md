---
title: LLM
published: 2025-07-08
description: "All about LLM"
tags: ["RoPE", "KV Cache", "Flash Attention", "ZERO-DP&R"]
category: Generative-Models
draft: false
---

**Faster self-attention**  
[Reformer](https://www.pragmatic.ml/reformer-deep-dive/)
1.  ![image1](resources/00f4a0dee59c417887256364b78ad324.png)  
Block QQV self-attention using LSH(Locality Sensitivity Hashing) to distribute key into different blocks(buckets)

![image2](resources/3d42f45ffffa4a73808238af868b036c.png)

![image3](resources/373900b5dba74a0bb000ca1207815e01.png)  
2.  Activation Checkpoints: Avoid storing key and values which cost quantity of memory consumption (when backpropagate)
![image4](resources/49c98010e004477bbdfc8a3946b2d458.png)

![image5](resources/8a994276fa154c7ab7748a096c35c180.png)
```
def forward_pass(x1, x2, Wf, Wg):

""" Need an extra node in the computational graph because the gradient of the loss with respect to z1 \# differs from the gradient of loss with respect to y1 x1: one half of layer input x2: other half of layer input Wf: weights that parameterize function f Wg: weights that parameterize function g """

z1 = x1 + f(Wf, x2)

y2 = x2 + g(Wg, z1)

y1 = z1
```

```
def backward_pass(y1, y2, d_y1, d_y2, Wf, Wg):

""" Pseudocode for RevNet of backward pass y1: one half of layer output y2: second half of layer output d_y1: derivative of y1 d_y2: derivative of y2 Wf: weights that parameterize function f Wg: weights that parameterize function g """

z1 = y1 # middle checkpoint to reconstruct input(key and value)

# Extra computation -- the price we pay for memory \# complexity that doesn't scale with n_layers \# Importantly this means we don't have to store x1 or x2!

x2 = y2 - g(Wg, z1)

x1 = y1 - f(Wf, x2)

# Standard backprop: # vjp --\> Vector Jacobian Product

d_Wf, partial_x2 = jax.vjp(f, Wf, x2)(d_z1)

d_Wg, partial_z1 = jax.vjp(g, Wg, z1)(d_y2)

d_z1 = d_y1 + partial_z1 \# d_x1 also follows reisudal connection

d_x2 = d_y2 + partial_x2 \# d_x2 also follows residual connection

d_x1 = d_z1

return x1, x2, d_x1, d_x2, d_Wf, d_Wg
```

3.  Avoid large memory consumption with long positional encoding  
![image6](resources/5968e1566e2741b4b7e5f30385363d67.png)

![image7](resources/814610a4946f41838b517df6c7c88004.png)

![image8](resources/af7885639b024d2689df5147280b991e.png)

Longformer
Reduce computation cost from O(L^2) to O(wL), w is window size
1.  Local attention (Dilated Conv-style attention)  
For each token in sequence, only compute attentions with tokens within fixed window center around it.

Similar to Convolutional network, deeper layer can have larger vision field  
2.  Global attention  
Only allow few specific tokens (e.g. CLS token) have global attention to other tokens

MQA(Muti-query attention)
Keep all attention heads share same key and value matrixes, but different query matrixes
![image9](resources/c37cb9d822c74cbfa64a92495621cfe2.png)
Goods:  
1.  Reduce consumption of memory of KV-cache
2.  Less I/O for Key/Value matrixes
Bads:
1.  Performance drop due to loss of representation capability, can be amended by increase scale of FFN or do further training
2.  Unstable training, requiring hyperparameter tuning

GQA(Group query attention)
It can be seem as multi-group MQA, heads in same group share same Key/Value matrixes
![image10](resources/2594cffa6a054815ac05a7de716c95c5.png)

Attention with prior structure to cut computation
1.  Sparse attention, sparse correlate relationship between Q and K
2.  Sliding window attention, fixed attention in small scope by defining sliding mask (note it is similar to convolutional network, the receptive field will be expanded as depth increasing)
![image11](resources/a82242b66c4544819e8186bdb2b43315.png)
3.  Interleave 'full' and 'LR' attention, e.g. every 4th layer is a full attention, others are sliding window attention

**Details when do LLM Inference**
1.  [Tokenization](https://huggingface.co/docs/transformers/tokenizer_summary#wordpiece) (BPE, Byte-BPE, WordPiece)
Mostly used is subword tokenization which rely on the principle that frequently used words should not be split into smaller subwords, but rare words should be decomposed into meaningful subwords. In this way, a reasonable vocabulary won't cause huge token embedding and quantity computation of softmax.

Thus in general, tokenization contains two phase
1.  First, train a vocabulary containing the smallest subwords, which are also most common one according to some statistical metrics
Take BPE as example:

\(1\) pre-tokenization: split training data into words and count their frequencies

SentencePiece (+Unigram(remove rule) ) for languages use different separation rules

\(2\) create a base vocabulary consisting of symbols that occur in unique words

\(3\) learn merge rules to expand vocabulary by merging two unique symbold with highest frequency til reaching expected vocabulary size or the new merged subword has frequency below certain threshold.

WordPiece take similar steps as BPE, but with likelihood as metric

![image12](resources/be26cddad37a4b19961c10d607188c62.png)  
2.  Encode a string into token ids or decode them back to human readable string.
Encode: Split sentence into subwords according vocabulary, and then convert them to token ids

Note: for a long word splitting into couple subwords, there will be special token for their connection

e.g. transformer -\> trans form, er\</w\> which means er\</w\> should join its all predecessors to form a complete word. And then \</w\> will be replaced with space

Decode: token ids were reversed to subwords, and them merge subwords should form a complete word.
2.  Autoregressive Inference process(Ignore residual and FFN, LN)
![image13](resources/a8cd225e6e5646c893b4907b601902a0.png)

![image14](resources/78fd473857de4bb18cd5f6e9e4502dec.png)

we calculate Q, K, V by

![image15](resources/950452ffa6c34b93a776ce0f6d7bdfda.png)

Applying self-attention, we get final output sequence

![image16](resources/6c5a735265d441ec982600c76b8301ae.png)

And then we get logits for next token

![image17](resources/f210880fe78b4fc19a820ae2eda35734.png)

To sample next token, we may apply a sampling pipeline including  
1.  Temperature Scaling (high temperature, more diverse generation, vice versa)
2.  Top-p Sampling or Top-K Filtering (Only look most likely choice add up to certain probability threshold, e.g. 90%)
3.  Beam search, this is for full output sequence generation
During each generation step, we maintain k best generation path with highest probability summation. And we choose the highest one when meet end.
3.  How to handle increased positional encoding for new generated token
    1.  Static Positional Encoding
![image18](resources/0d39da2f6f764df48ccbf412a03825b1.png)

Else

For Sliding Window Attention, with window size w

Mask out attention exceeds \[t-w,t\], right shift positional encoder by one offset

![image19](resources/6695ea1298fd464fab701695a6abdf1d.png)

For Interpolation, expand original positional encoding with longer length (more dense)
2.  Relative Positional Encoding
Using relative positional bias, with no constraint of max length

![image20](resources/b951951fee5d4e51a2aa3a6dc2cb881d.png)

It was added directly to attention: 〖QK〗^T+P (prior of nearby closer)
3.  RoPE (Rotary Positional Embedding)
Encoding relative position as rotation
4.  [K-V cache (Why not cache Q ?)](https://medium.com/@joaolages/kv-caching-explained-276520203249)
![image21](resources/924026b4ccf24a4eb4c40d84bf6f0bec.png)

![image22](resources/4ec9c76bf60f42019f7ec734472a70e1.png)

![image23](resources/07a1d1ab84e849eea61f3ae90f648efe.png)

![image24](resources/90a4a06d25604056bc4e06527d0ef3ef.png)

![image25](resources/6d52f02182224c22a508238bf549e3a7.png)

![image26](resources/80c456e91ce04fd9b25ef32c55473511.png)

So why don't we pre-cache K, V of each block and only compute their last output ? Also, since the last output independent of Q, we don't need to cache Q.

![image27](resources/a5cd368c8a9c464a9832689d6900922b.png)

![image28](resources/be9b480c42e441588523a672fdf2c874.png)

![image29](resources/d195a214b942486cb9363f95a02b69a9.png)

Also, the left-to-right connection (attention mask) makes output of t can only rely on that smaller or equal than t. Thus, there's no way O can have access to k and v, changing the decision already being made.

**[Bottleneck: Memory and Communication](https://zhuanlan.zhihu.com/p/663517415) (ZeRO-DP&R)**  

Issues:
1.  Huge memory consumption of LLM, including:
    1.  Model States Memory
        1.  Optimizer States (e.g. first and second FP32 moments of Adam, takes most of memory ! FP32 parameter backup (avoid error accumulation of FP16))
        2.  Mix precision: FP16 parameters and gradients
    2.  Residual States Memory
        1.  Activations used for gradient computation. (Can be cut by activation checkpoint, only store activations of high computation cost but with consume small memory, recompute others during backward.)
        2.  Temporary Buffers(FP32) which store all middle results and then do computation altogether (averaging gradients from different devices).
        3.  Memory Fragmentation: too much small discrete memory fragmentation caused by deleting activations, which makes memory allocation failed even the rest is enough.
2.  Data Parallelisms will copy model to all devices, cause redundance memory consumption
3.  Model partition splits model over different devices, but cost lots of communication
4.  DP and MP stores all model state during the whole training process, but not any of them are required during the whole time.
![image30](resources/89bb2f0e07e9410b9da417385a7887a0.png)

Solutions of ZeRO: Partition + ReduceScatter&AllGather
![image31](resources/4c0a9046b1ac4557867ff40c05379271.jpg)
Combine edges of DP and MP, while avoiding their disadvantages. For N_d devices, follow DP training process, we input different data into different devices and gather their averaged gradient to update parameters. Since update for paramters only execute onces, we can slice and dispatch it into different devices in charge of update of different parameters slice. Also, we still need to compute gradient w.r.t all parameters in each device, but in a stream way we don't need to store all of them, instead only the slice need to update parameters slice.

Optimizer State Partitioning, distribute optimizer state into different devices
![image32](resources/f69852f2fd6e4f7690da0a664b08f906.png)
Communication process (After calculating gradient of each devices)
1.  ![image33](resources/f0bd55b2ae364cf6bcb7bd8ed9454ac5.png)
2.  Use AllGather process to broadcast updated parameters to other devices
![image34](resources/b7ea0d3b532b4b8ca2a53f54582c3c63.png)

+Gradient Partitioning, distribute gradient into different devices
![image35](resources/aa8767080eed4095840c7c9e3568f6a1.png)
Communication process (After calculating gradient of each devices in a stream manner)
1.  ![image36](resources/e201bc76c9d04ed69c9591da6c1dc798.png)
2.  Use AllGather process to broadcast updated parameters to other devices
![image37](resources/2ea3fdc72788418580fc119433e81152.png)

+Parameter Partitioning, distribute parameter into different devices
![image38](resources/9738a25902f34475b7111ce5cb7b184f.png)  
Communication process  
1.  AllGather process for forward (Communication follow order of forward): since different devices need complete parameter to get loss, thus it needs other parameter slices from other devices. But note that once it finish computing middle activations, which will be stored, it will send the parameter slice to other devices and clean occupied memory space for receiving next layer's parameter from other device. So it will only takes 2 parameter slices of space at most.
2.  AllGather process for backward, similar to step 1 (use activations from step 1).
3.  ![image36](resources/e201bc76c9d04ed69c9591da6c1dc798.png)
![image39](resources/b0747429ded14f55960a6203cbc1195f.png)

[ZeRO-R](https://medium.com/@e0928021388/%E5%84%AA%E5%8C%96%E4%BD%A0%E7%9A%84-training-deepspeed-a-deep-learning-optimization-library-%E4%BB%8B%E7%B4%B9-b409eb4c9436)
![image40](resources/0bc9d6547ede4e70bdd87b34bc12bf64.jpeg)
Partitioned Activation Checkpointing, distributed activation checkpoints into different MP process(devices). For extreme large activation or limit device memory, they will be offload to CPU memory in trade of extra communication cost.
![image41](resources/d29364fde49c4379a68a4ecb00853e14.png)  
Communication process
(optional) load activation slices from CPU memory
1.  AllGather process for forward: activations act as input to deeper layers which sit in different devices
2.  AllGather process for backward: when activations was required to compute corresponding gradient, it will be replicated to different devices.
Note that in MP, model was split into different devices, thus we can dispatch and gather activation, as they belong to same model. (In contrast, DP has multiple model replica, thus we can not dispatch activation in that way.)

Constant Size Buffers, avoiding buffer size grow with model size.

Memory Defragmentation, long life circle of activation and gradient interleaving with short one cause lots memory fragmentation. Thus it is necessary to pre-allocate them in continuous memory blocks and organize memory fragment in time (e.g. activation.continuous() or gradient.continuous() )  
[**Why do we need positional encoding**](https://huggingface.co/blog/designing-positional-encoding)  
Self-attention is a set operation, which means it is Permutation Equivariant
It operate on a set and calculate their relationship without considering their presented order.
![image42](resources/208af588183e4c34a4c4b4296542235a.png)  
It means output has consistent order with permuted input, but no change in values
Proof:
![image43](resources/0eba48a6b89c40f7bfe878b2c084f806.png)

![image44](resources/409eea95bf7a471ea51b840d92276914.png)

![image45](resources/dcab1d56e3204d139d2a594bff7e7341.png)  
So self-attention is not sensitive to order of input, that's why a positional embedding was need.

RoPE (Encoding relative position as rotation)  
Intuition: Relative position information already hidden as rotation in Sinusoidal Encoding
Sinusoidal Encoding
![image46](resources/5d0757d8b29a4da089115f75375a5f73.png)
![image47](resources/6e9027cca5144603905174c4a871c041.png)

![image48](resources/af098931d5294d4baed530ab238800a0.png)

![image49](resources/7a44d0648b71454eb0501561cca4598c.png)

![image50](resources/4a05d5ecc0194a62bd98cfd93edc515d.png)

NTK-Aware RoPE: [High frequency interpolation, Low extrapolation](https://zhuanlan.zhihu.com/p/8306958113)
![image51](resources/fb928076d50b43a8b937f83dfa690432.png)

Thus smaller i, faster spinning. Take clock as a concrete example, second hand spins faster, hour hand spins lowest. Their combination makes a 60-based 3 digits code. One movement of hour hand requires 60 times spins of minute hand.

In that way, we can also take binary as 2-scale clock.

During training, every spot in circle of high frequency has been seen by model, thus for OOD input, we can directly extrapolate it instead of interpolation (which will higher the frequency, making model hard to distinguish nearby positions), but interpolate it for low frequent digit, as their slow motion makes mass spots unexplored so that model can not handle OOD spots.

Thus low frequent digit becomes lower so to keep position in explored region.

![image52](resources/0cb1c554c96e435d9427bc085e5de5d4.jpg)

Relative position: Relation between position p and p+k
![image53](resources/f90667aa21a2478c86688bf28c4b63cb.png)
Insights
1.  Relative information matters much, as we care more about relationship to the words around a specific word
2.  Simply adding positional embedding to token embedding pollution the intrinsic sematic information (by modifying its norm and decreasing SNR)
3.  Prior of attention: nearby words should have more influence than distant one
Attention weight calculated by dot product

![image54](resources/6ef8821c3f164d489b2c36dea98e1cbb.png)

We can find that Sinusoidal Encoding violates Insights due to destruction of long-term decay after applying linear transformation. Further, addition makes it worser.
![image55](resources/eed57ead2ce34f349c48385609806cf7.png)
![image56](resources/ed0dd1d8dd714d7795901a3f98f17da0.png)
![image57](resources/ef073187e20e490d84c200be08b85523.png)
![image58](resources/0f978ecf9a5c45d3bbc859243d8d35ca.jpg)

Thus we can encode the prior(relative position) as rotation apply to token embedding, without changing its norm, nearby words have relatively small rotation angle.
![image59](resources/8c3e10dd1ba44b6db77d9378baedf00c.png)
For N-D inputs, RoPE can be applied to each dimension independently.
As for the posterior attention pattern (e.g. high correlation between object and its distant pronoun) will learn through training.

[**Flash Attention**](https://zhuanlan.zhihu.com/p/642962397)
Most efficient transformer focus on reduction of FLOPS, while the bottleneck rest in memory access cost. Flash attention aims at cutting MAC by **chunking huge matrix into small blocks** which can be accessed through SRAM (which has fastest IO speed).

![image60](resources/9743c5f6ed9c4e00866e3ddd351b6a35.jpg)

IO of self-attention conduct in HBM, which has high IO delay than SRAM
![image61](resources/acfce23fd8c7482f9ecafea274c77b58.jpg)

Dynamic Incrementally Update Softmax  
Since the softmax operation involves summation of all elements, the main issue is to also chunking computation of softmax into blocks.

The traditional way of softmax
![image62](resources/41cc75640fff476caf385cfc69de2685.png)
In case of overflow, subtraction to maximum will be applied
![image63](resources/ffe783ee8ec1406c84e3ddcbb7c91691.png)

![image64](resources/9b4f23e3c59a4e2b8e3c95cb9ffb80de.png)

![image65](resources/ad7c1ec2fda54b7a8c321b6ddd523f35.png)

![image66](resources/258d4c896dec484ba96e054d4b961e30.png)
![image67](resources/55487cb84ab64494894dc4da8004286a.png)
![image68](resources/66c08a509d51491cb5b06279b22d5603.png)

![image69](resources/da3ad94c6f4947ba840a0d47fe74ee70.png)

![image70](resources/e023e0db40414628b5b6be0e0dd2be53.png)

![image71](resources/0b4b6ab741f04b15895d91c03a364cf4.png)
![image72](resources/8a89f06528b541f981592b9bbf8fa632.png)
![image73](resources/fab8708c0f294e468f5e9a9b79a5c1ff.png)
![image74](resources/c6c7bb197d0746fda86fc9124b93576a.png)

![image75](resources/a18604f6ea414353bec1408c4878d845.png)

![image76](resources/b128de721f87432391a9f4caadc3ef2f.png)

![image77](resources/b5d539703762479d9aa95c24c633e70f.png)
The same update rule for block 2
![image78](resources/6be59bf8f4ed451da0c94f6682614d4a.png)
And then update global maximum and summation, and store them into SRAM
![image79](resources/80280dfc2eb04221a91db8116d21c01a.png)
For case of more blocks, such update rule can be iteratively executed till getting global softmax result.
Also, in Flash Attention V2, divide to summation when calculate local softmax was cancelled since the denominator will be cancelled out in each update. Assume that in t update round,
![image80](resources/247c1592670f43468dfc3c164caefb04.png)
It causes redundant computation, thus we can modify it to no-divide-softmax, and only apply division until we get the global summation
![image81](resources/c791bcb4b29d4062bfb6e48db6a9866b.png)
During the updating, we only need to store 2 scalars in SRAM instead of a full vector.

![image82](resources/c9b7a413301e4cf8b112c97274bdb6c3.png)
Further, in Flash Attention V2, calculation of blocks of being masked will be skipped.

**Collective Operations**  

Distributed training of LLM can be abstract as collective operations. i.e. Split training computation into different GPUs, results of which will be gathered into a main site and reducing to final result, which in turn will be broadcasted to different GPUs to continue the collective circle. Thus the bottleneck rests in communication.

Such process is called All Reduce.
1.  Reduce(N to 1): reduce(sum) multiple computation from different sites results into one main site
2.  Broadcast(1 to N): Main site broadcasts reduced results to other sites
Generally, main site maybe the bottleneck since it takes too much word load.
Scatter-version of All Reduce: split computation into different slices, different sites handle All Reduce for different slices, i.e. every site share burden of main site.
1.  ![image83](resources/da66d585b3254f5786500aa2822ad525.png)
2.  AllGather(N to 1):
    1.  ![image84](resources/61a1fc8cfc23406a8f6ad6b24ddec088.png)
    2.  Broadcast: main site broadcast complete result to other sites

Ring-ReduceScatter / Ring-AllGather: High efficiency implementation
Core: Ring communication
1.  ![image85](resources/82281b9fc4ba41cd9bdfe6688a403905.png)
2.  ![image86](resources/9e5f367c1609405dadebbc4f36cd4086.png)
Computation of communication consumption = sending communication + receive communication
![image87](resources/b4231cb9916b4a97a7c26bbe4bcabce5.png)
![image88](resources/f482586e66264fd488dfbd4f6e906de6.png)
Total duration is
![image89](resources/c979d0f9d63d46b98145b6adec6169b4.png)
Duration of ring-based communication almost independent to number of devices, but its total communication correlates with number of devices.

![image90](resources/ad035b4280dc496c870ab5db5cbfd15f.jpeg)

**MoE (Mixture of Expert): Router + Multi-FFN**  
![image91](resources/18123cfad51e44d4beb70d118ca43f36.png)
1.  Routing function (choose top K and fusion) How to choose ? How to fusion ?
    1.  Top-K according to logits: calculate correlation between expert and token
![image92](resources/56523c47e0164ff99aabcf8ac506ea3c.png)

![image93](resources/48a4a027f133425aac419c9c2968b6c1.png)

Note that the Topk operation makes the factor summation less than 1, which shrinks the input, but such scale variant will be scaled back in later layers (Layer Norm)
2.  Hashing: map token to expert(FFN)
3.  RL-guided gating polices learning
4.  Solve a matching problem (Linear Assignment)
b,c,d have too much computation cost
2.  Expert sizes
Smaller( with smaller hidden dim), larger number of experts + a few shared experts(always activated), but too many fine-grained experts may cause more communication
3.  Training objectives: How to efficiently train a sparsity gating policy ? Considering that sparse decisions are not differentiable.
    1.  Reinforcement learning to optimize gating policies
    2.  Stochastic perturbations: competition mechanism
Shazeer et al 2017 – routing decisions are stochastic with gaussian perturbations.

![image94](resources/2aa490b52bb2406289cb7178e165ac94.png)

![image95](resources/63e536bcd56840a1a62219ea1d4730d8.png)

![image96](resources/8e490634f81f44608a690054d2f6d3a0.png)

Stochastic jitter in Fedus et al 2022

![image97](resources/bd9451895eb843329e26e87fa0c75436.png)

Such perturbation method can gain robust(conservative) expert, but also make them less profession (less sensitive to token), causing loss of efficiency.
3.  Heuristic 'balancing' losses: system efficiency requires that use experts evenly. We hope the decision panel won't only rely on few experts.
Switch Transformer \[Fedus et al 2022\] : auxiliary loss

![image98](resources/82b5ea5b325745868608ffc1b289bb3d.png)

![image99](resources/2bd79841b9e04181b8b1c3518afbb509.png)

![image100](resources/d3568e161539419ea963bcf09d9522f5.png)

![image101](resources/14d052653de94eb38e9f3ac7e1afd818.png)

Thus loss measure of Expectation of tokens handle by an expert, since we want them used evenly, thus leading to each expert handle as less token as possible, the optimal reach when each expert only handle T/N tokens

![image102](resources/4b6ea1c0a8c245a7ac8fdf4d0b373c31.png)

Such load balancing can also be extented to different expert groups in different devices to make sure even utilization on different devices

DeepSeek v3: per-expert biases, topk frequent, Set up a per-expert bias (making it more likely to get tokens) and use **online learning** (not necessarialy even, dynamic balancing during inference)

![image103](resources/a74e9d07e61e40479b2d211221ff1765.png)

Complementary sequence-wise balance loss (used in training)

![image104](resources/90afd7b5e68646709fda131a7cda31bd.png)

Normalized decision fusion from Topk experts

![image105](resources/bed7c8cf497f46d2812d45bfdd8988d3.png)

![image106](resources/77e4a80213434a5ba6bd273a2a919412.png)

![image107](resources/3c19797e7b0c4d48bca93cbc48492a91.png)  
4.  Training/finetuning stability
Using float32 for router and add aux z-loss (constraint denominator of softmax close to 1)

![image108](resources/e39e63f127dc4137b073a72267916d46.png)  
5.  Communication cost loss (DeepSeek v2)
Top-M devices select(touting), then do Top-K experts select on each selected device

![image109](resources/ce14ebc3f8c4484bb25508475564d400.png)

![image110](resources/5d98cc5e9d7a4cdcbec921e2a5509c0f.png)  
4.  System side: parallel MoE on more devices
Experts on different decices choose token: load balancing across devices  
5.  Up-cycling: turn dense model (with one FFN) to sparse one (add MoE)

