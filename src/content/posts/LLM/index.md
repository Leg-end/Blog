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
1. Reduce computation cost from O(${\mathrm{L}}^{2}$) to O($\mathrm{L}\mathrm{log}L$)
Block QQV self-attention using LSH(Locality Sensitivity Hashing) to distribute key into different blocks(buckets)
![](image_1.e3cb7eb4.png)
![](image_2.dbe38b44.png)
2. Activation Checkpoints: Avoid storing key and values which cost quantity of memory consumption (when backpropagate)  
Reversible Residual Network (store ${\mathrm{Y}}_{1}$ to reconstruct ${\mathrm{X}}_{1},{X}_{2}$)  
![](image_3.546cad00.png)
```
def forward_pass(x1, x2, Wf, Wg):
""" Need an extra node in the computational graph because the gradient of the loss with respect to z1 # differs from the gradient of loss with respect to y1 x1: one half of layer input x2: other half of layer input Wf: weights that parameterize function f Wg: weights that parameterize function g """
  z1 \= x1 + f(Wf, x2)
  y2 \= x2 + g(Wg, z1)
  y1 \= z1

def backward_pass(y1, y2, d\_y1, d\_y2, Wf, Wg):
""" Pseudocode for RevNet of backward pass y1: one half of layer output y2: second half of layer output d_y1: derivative of y1 d_y2: derivative of y2 Wf: weights that parameterize function f Wg: weights that parameterize function g """
  z1 \= y1 # middle checkpoint to reconstruct input(key and value)  
  # Extra computation -- the price we pay for memory # complexity that doesn't scale with n_layers # Importantly this means we don't have to store x1 or x2!
  x2 \= y2 \- g(Wg, z1)
  x1 \= y1 \- f(Wf, x2)
  # Standard backprop: # vjp --> Vector Jacobian Product
  d\_Wf, partial\_x2 \= jax.vjp(f, Wf, x2)(d\_z1)
  d\_Wg, partial\_z1 \= jax.vjp(g, Wg, z1)(d\_y2)
  d\_z1 \= d\_y1 + partial\_z1 # d_x1 also follows reisudal connection
  d\_x2 \= d\_y2 + partial\_x2 # d_x2 also follows residual connection
  d\_x1 \= d\_z1
  return x1, x2, d\_x1, d\_x2, d\_Wf, d\_Wg
```

3. Avoid large memory consumption with long positional encoding
Axial positional encoding: split L x D positional encoding matrix into ${\mathrm{E}}_{1}\in {R}^{{L}_{1}\times {D}_{1}}$ and ${\mathrm{E}}_{2}\in {R}^{{L}_{2}\times {D}_{2}}$
  Where ${\mathrm{L}}_{1}\times {L}_{2}=L,{D}_{1}+{D}_{2}=D$
Position encoding at time t = $\left[{\mathrm{E}}_{1}\left[t\%L1\right],{E}_{2}\left[\lfloor t/{L}_{2}\rfloor \right]\right]$

Longformer  
Reduce computation cost from O(${\mathrm{L}}^{2}$) to O(wL), w is window size
1. Local attention (Dilated Conv-style attention)
For each token in sequence, only compute attentions with tokens within fixed window center around it.
Similar to Convolutional network, deeper layer can have larger vision field
2. Global attention
Only allow few specific tokens (e.g. CLS token) have global attention to other tokens

MQA(Muti-query attention)  
Keep all attention heads share same key and value matrixes, but different query matrixes
![](image_4.786db1a9.png)

Goods:
1. Reduce consumption of memory of KV-cache
2. Less I/O for Key/Value matrixes

Bads:
1. Performance drop due to loss of representation capability, can be amended by increase scale of FFN or do further training
2. Unstable training, requiring hyperparameter tuning
GQA(Group query attention)
It can be seem as multi-group MQA, heads in same group share same Key/Value matrixes
![](image_5.6ca5eb73.png)

Attention with prior structure to cut computation
1. Sparse attention, sparse correlate relationship between Q and K
2. Sliding window attention, fixed attention in small scope by defining sliding mask (note it is similar to convolutional network, the receptive field will be expanded as depth increasing)
![](image_6.603635ec.png)
3. Interleave 'full' and 'LR' attention, e.g. every 4th layer is a full attention, others are sliding window attention  

**Details when do LLM Inference**  
1. [Tokenization](https://huggingface.co/docs/transformers/tokenizer_summary#wordpiece) (BPE, Byte-BPE, WordPiece)
Mostly used is subword tokenization which rely on the principle that frequently used words should not be split into smaller subwords, but rare words should be decomposed into meaningful subwords. In this way, a reasonable vocabulary won't cause huge token embedding and quantity computation of softmax.
Thus in general, tokenization contains two phase
1) First, train a vocabulary containing the smallest subwords, which are also most common one according to some statistical metrics  
Take BPE as example:  
(1) pre-tokenization: split training data into words and count their frequencies
  SentencePiece (+Unigram(remove rule) ) for languages use different separation rules  
(2) create a base vocabulary consisting of symbols that occur in unique words  
(3) learn merge rules to expand vocabulary by merging two unique symbold with highest frequency til reaching expected vocabulary size or the new merged subword has frequency below certain threshold.
WordPiece take similar steps as BPE, but with likelihood as metric

$$
\underset{i,j}{\mathrm{max}}\left\{\frac{\#\left(subwor{d}_{i}+subwor{d}_{j}\right)}{\#\left(subwor{d}_{i}\right)\#\left(subwor{d}_{j}\right)}\right\}
$$

2) Encode a string into token ids or decode them back to human readable string.  
Encode: Split sentence into subwords according vocabulary, and then convert them to token ids
  Note: for a long word splitting into couple subwords, there will be special token for their connection
  e.g. transformer -> trans form, er</w> which means er</w> should join its all predecessors to form a complete word. And then </w> will be replaced with space
Decode: token ids were reversed to subwords, and them merge subwords should form a complete word.  
2. Autoregressive Inference process(Ignore residual and FFN, LN)  
Given Input token Sequence $\mathrm{X}=\left[{x}_{1},\dots ,{x}_{t}\right]\in {R}^{t}$, we turn it into embedding and add positional encoding

$$
{\mathrm{X}}_{input}=E+P\left[:t,:\right]\in {R}^{t\times d}
$$

we calculate Q, K, V by

$$
\mathrm{Q}={{\mathrm{X}}_{input}\mathrm{W}}_{Q}\in {R}^{t\times d},\ \ \mathrm{K}={{\mathrm{X}}_{input}\mathrm{W}}_{K}\in {R}^{t\times d},\ \ \mathrm{V}={{\mathrm{X}}_{input}\mathrm{W}}_{V}\in {R}^{t\times d}
$$

Applying self-attention, we get final output sequence

$$
\mathrm{O}={\mathrm{QK}}^{\mathrm{T}}\mathrm{V}\in {R}^{t\times d}
$$

And then we get logits for next token

$$
{\mathrm{logits}}_{t+1}=O{W}_{lm}
$$

To sample next token, we may apply a sampling pipeline including
1) Temperature Scaling (high temperature, more diverse generation, vice versa)
2) Top-p Sampling or Top-K Filtering (Only look most likely choice add up to certain probability threshold, e.g. 90%)
3) Beam search, this is for full output sequence generation
During each generation step, we maintain k best generation path with highest probability summation. And we choose the highest one when meet end.
3. How to handle increased positional encoding for new generated token
  1) Static Positional Encoding  
  Else
    For Sliding Window Attention, with window size w
      Mask out attention exceeds \[t-w,t\], right shift positional encoder by one offset
      e.g. if w = 512, ${\mathrm{x}}_{0}$ will not be atten for ${\mathrm{x}}_{512}$, ${\mathrm{x}}_{1}$ has position 0, ${\mathrm{x}}_{512}$ has position 511
    For Interpolation, expand original positional encoding with longer length (more dense)
  2) Relative Positional Encoding
  Using relative positional bias, with no constraint of max length
  $\mathrm{P}\in {R}^{L\times L},P[i,j]$indicates token i 's relative postion after token j
  It was added directly to attention: ${\mathrm{QK}}^{\mathrm{T}}+\mathrm{P}$ (prior of nearby closer)
  3) RoPE (Rotary Positional Embedding)
  Encoding relative position as rotation
4. [K-V cache (Why not cache Q ?)](https://medium.com/@joaolages/kv-caching-explained-276520203249)
Follow the Autoregressive Inference process, we yield new token ${\mathrm{x}}_{t+1}$, which will append to $\mathrm{X}$
The traditional way will recompute self-attention on new input with length t+1, which further require $\mathrm{O}\left({\left(\mathrm{t}+1\right)}^{2}\right)$, costing over redundance computation of K and V.

$$
{\mathrm{Q}}_{new}=\left[Q,q\right],\ \ {K}_{new}=\left[K,k\right],\ \ {V}_{new}=\left[V,v\right]
$$

$$
{\mathrm{Q}}_{new}{K}_{new}^{T}{V}_{new}=\left[\begin{array}{c}Q{K}^{T}V+Q{k}^{T}v\\ q{K}^{T}V+q{k}^{T}v\end{array}\right]=\left[\begin{array}{c}O\\ o\end{array}\right]
$$

By treating $\mathrm{o}$ as new token ${\mathrm{x}}_{t+1}$ for next transformer block, we still have same format of output. So the final output looks like the same way. But to predict next token, we only need last output, i.e. $q{K}^{T}V+q{k}^{T}v$
Thus, calculation of $Q{K}^{T}V+Q{k}^{T}v$ in each layer cause tremendous waste of computation.
So why don't we pre-cache K, V of each block and only compute their last output ? Also, since the last output independent of Q, we don't need to cache Q.
In that sense, we can pre-cache K,V when generating ${\mathrm{x}}_{t+1}$. Then when compute ${\mathrm{x}}_{t+2}$, we update K-V cache

$$
{K}_{new}=\left[K,k\right],\ \ {V}_{new}=\left[V,v\right]
$$

And get last output $o=q{K}^{T}V+q{k}^{T}v=q{K}_{new}^{T}{V}_{new}$ of First transformer block, follow the same way, take o as 'q' for next transformer block, we can get its last output … til the top of model, we get final last output to predict next token. Thus the computation complex is reduce to $\mathrm{O}\left(t\right)$ for each block.
Also, the left-to-right connection (attention mask) makes output of t can only rely on that smaller or equal than t. Thus, there's no way O can have access to k and v, changing the decision already being made.

[**Bottleneck: Memory and Communication**](https://zhuanlan.zhihu.com/p/663517415)** (ZeRO-DP&R)**
Issues:
1. Huge memory consumption of LLM, including:
  1) Model States Memory
    i. Optimizer States (e.g. first and second FP32 moments of Adam, takes most of memory ! FP32 parameter backup (avoid error accumulation of FP16))
    ii. Mix precision: FP16 parameters and gradients
  2) Residual States Memory
    i. Activations used for gradient computation. (Can be cut by activation checkpoint, only store activations of high computation cost but with consume small memory, recompute others during backward.)
    ii. Temporary Buffers(FP32) which store all middle results and then do computation altogether (averaging gradients from different devices).
    iii. Memory Fragmentation: too much small discrete memory fragmentation caused by deleting activations, which makes memory allocation failed even the rest is enough.
2. Data Parallelisms will copy model to all devices, cause redundance memory consumption
3. Model partition splits model over different devices, but cost lots of communication
4. DP and MP stores all model state during the whole training process, but not any of them are required during the whole time.  
That cause baseline Model States Memory(bytes) = $\begin{array}{c}Param\\ \stackrel{\text{has}}{2\times \mathrm{\Psi}}\end{array}+\begin{array}{c}Gradient\\ \stackrel{\text{has}}{2\times \mathrm{\Psi}}\end{array}+\begin{array}{c}Adam:moments,\ backup\\ \stackrel{\text{has}}{3\times 4\times \mathrm{\Psi}}\end{array},$ $\mathrm{\Psi}$ is paramters storage
Solutions of ZeRO: Partition + ReduceScatter&AllGather
![](image_7.c8f36a92.jpg)
Combine edges of DP and MP, while avoiding their disadvantages. For ${\mathrm{N}}_{d}$ devices, follow DP training process, we input different data into different devices and gather their averaged gradient to update parameters. Since update for paramters only execute onces, we can slice and dispatch it into different devices in charge of update of different parameters slice. Also, we still need to compute gradient w.r.t all parameters in each device, but in a stream way we don't need to store all of them, instead only the slice need to update parameters slice.
Optimizer State Partitioning, distribute optimizer state into different devices

$$
{P}_{os}=\begin{array}{c}Param\\ \stackrel{\text{has}}{2\times \mathrm{\Psi}}\end{array}+\begin{array}{c}Gradient\\ \stackrel{\text{has}}{2\times \mathrm{\Psi}}\end{array}+\begin{array}{c}Adam:moments,\ backup\\ \stackrel{\text{has}}{\frac{12\times \mathrm{\Psi}}{N_d}}\end{array}\approx 4\mathrm{\Psi},\ \ N_d\to \infty 
$$

Communication process (After calculating gradient of each devices)
1. Use process of ReduceScatter to get averaged gradient slice $i$ for device $i$, then use it to update optimizer states slice $i$, and then use it to update corresponding paramter slice $i$
2. Use AllGather process to broadcast updated parameters to other devices
The total communication cost is $2\mathrm{\Psi}$, note that to update optimizer states slice $i$*, *we don't need to store all gradient. Thus we can further only store gradient related to optimizer states.  
+Gradient Partitioning, distribute gradient into different devices

$$
{P}_{os+g}=\begin{array}{c}Param\\ \stackrel{\text{has}}{2\times \mathrm{\Psi}}\end{array}+\begin{array}{c}Gradient+Optimizer\\ \stackrel{\text{has}}{\frac{14\times \mathrm{\Psi}}{N_d}}\end{array}\approx 2\mathrm{\Psi},\ \ {N}_{d}\to \infty 
$$

Communication process (After calculating gradient of each devices in a stream manner)
1. Use process of ReduceScatter to get averaged gradient slice $i$ for device $i$, then use it to update optimizer states slice $i$, and then use it to update corresponding paramter slice $i$
2. Use AllGather process to broadcast updated parameters to other devices
The total communication cost is $2\mathrm{\Psi}$, note that at step 1, we still calculate gradients w.r.t all parameters, but we will send its slice $j\left(j\ne i\right)$ to other devices(thus won't occupy memory to store them) and only keep slice $i$  
+Parameter Partitioning, distribute parameter into different devices

$$
{P}_{os+g+p}=\begin{array}{c}Param+Gradient+Optimizer\\ \stackrel{\text{has}}{\frac{16\times \mathrm{\Psi}}{{N}_{d}}}\end{array}\approx 0,\ \ {N}_{d}\to \infty 
$$

Communication process
1. AllGather process for forward (Communication follow order of forward): since different devices need complete parameter to get loss, thus it needs other parameter slices from other devices. But note that once it finish computing middle activations, which will be stored, it will send the parameter slice to other devices and clean occupied memory space for receiving next layer's parameter from other device. So it will only takes 2 parameter slices of space at most.
2. AllGather process for backward, similar to step 1 (use activations from step 1).
3. Use process of ReduceScatter to get averaged gradient slice $i$ for device $i$, then use it to update optimizer states slice $i$, and then use it to update corresponding paramter slice $i$
The total communication cost is $3\mathrm{\Psi}$, note that since parameters were sliced into different devices, it won't need to broadcast updated parameters to other devices.  
[ZeRO-R](https://medium.com/@e0928021388/%E5%84%AA%E5%8C%96%E4%BD%A0%E7%9A%84-training-deepspeed-a-deep-learning-optimization-library-%E4%BB%8B%E7%B4%B9-b409eb4c9436)  
![](image_8.adb1d58b.jpg)
Partitioned Activation Checkpointing, distributed activation checkpoints into different MP process(devices). For extreme large activation or limit device memory, they will be offload to CPU memory in trade of extra communication cost.

$$
{P}_{a}=\frac{Activation\ memory}{R},R=C{N}_{d},\ \ {P}_{a+CPU}\to 0
$$

Communication process
  (optional) load activation slices from CPU memory
1. AllGather process for forward: activations act as input to deeper layers which sit in different devices
2. AllGather process for backward: when activations was required to compute corresponding gradient, it will be replicated to different devices.
Note that in MP, model was split into different devices, thus we can dispatch and gather activation, as they belong to same model. (In contrast, DP has multiple model replica, thus we can not dispatch activation in that way.)
Constant Size Buffers, avoiding buffer size grow with model size.
Memory Defragmentation, long life circle of activation and gradient interleaving with short one cause lots memory fragmentation. Thus it is necessary to pre-allocate them in continuous memory blocks and organize memory fragment in time (e.g. activation.continuous() or gradient.continuous() )
-----  
[**Why do we need positional encoding**](https://huggingface.co/blog/designing-positional-encoding)  
Self-attention is a set operation, which means it is Permutation Equivariant
It operate on a set and calculate their relationship without considering their presented order.
i.e. $X=\left\{{x}_{1},\dots ,{x}_{n}\right\},f\left(\mathit{\pi}\left(X\right)\right)=\mathit{\pi}\left(f\left(X\right)\right),\ \mathit{\pi}\ is\ permutation\ operation$
It means output has consistent order with permuted input, but no change in values
Proof:

$$
X=\left\{{x}_{1},\dots ,{x}_{n}\right\}\in {R}^{L\times D},\mathit{\pi}\left(X\right)=\mathrm{\Pi}X,\mathrm{\Pi}\ is\ permuted\ Identity\ matrix
$$

$$
{\mathrm{Q}}_{\mathit{\pi}}=\mathrm{\Pi}X{W}_{Q}=\mathrm{\Pi}\mathrm{Q},\ \ {\mathrm{K}}_{\mathit{\pi}}=\mathrm{\Pi}X{W}_{K}=\mathrm{\Pi}\mathrm{K},\ \ {\mathrm{V}}_{\mathit{\pi}}=\mathrm{\Pi}X{W}_{V}=\mathrm{\Pi}\mathrm{V}
$$

$$
{\mathrm{A}}_{\mathit{\pi}}={\mathrm{Q}}_{\mathit{\pi}}{\mathrm{K}}_{\mathit{\pi}}^{T}=\mathrm{\Pi}{\mathrm{QK}}^{\mathrm{T}}{\mathrm{\Pi}}^{\mathrm{T}}=\mathrm{\Pi}\mathrm{A}{\mathrm{\Pi}}^{\mathrm{T}}
$$

$$
{\mathrm{A}}_{\mathit{\pi}}{V}_{\mathit{\pi}}=\mathrm{\Pi}\mathrm{A}{\mathrm{\Pi}}^{\mathrm{T}}\mathrm{\Pi}\mathrm{V}=\mathrm{\Pi}\mathrm{AV}=\mathrm{\Pi}\mathrm{O}
$$

$$
\Rightarrow \mathrm{Attention}\left({\mathrm{Q}}_{\mathit{\pi}},{\mathrm{K}}_{\mathit{\pi}},{\mathrm{V}}_{\mathit{\pi}}\right)=\mathit{\pi}\left(Attention\left(Q,K,V\right)\right)
$$

So self-attention is not sensitive to order of input, that's why a positional embedding was need.
RoPE (Encoding relative position as rotation)
Intuition: Relative position information already hidden as rotation in Sinusoidal Encoding
Sinusoidal Encoding
![](image_9.eecf3b8e.png)

$$
{\mathrm{PE}}_{\left(pos,2i\right)}=\mathrm{sin}\left(\frac{pos}{{10000}^{2i/d}}\right),\ \ {\mathrm{PE}}_{\left(pos,2i+1\right)}=\mathrm{cos}\left(\frac{pos}{{10000}^{2i/d}}\right)
$$

  [In fact](https://kexue.fm/archives/9675#%E4%BD%8D%E7%BD%AE%E7%BC%96%E7%A0%81) ${\mathrm{PE}}_{\left(pos,\bullet \right)}$ encodes a base-${10000}^{2/d}$ code for pos, thus ${\mathrm{PE}}_{\left(pos,2i\right)}$ is ith base-${10000}^{2/d}$ number of pos
  e.g. 17:${\left(10001\right)}_{2}$ 's 2nd binary number is $\lfloor 17/{2}^{1}\rfloor\ mod\ 2=0$  
   $\lfloor\frac{n}{{\mathit{\beta}}^{i}}\rfloor mod\ \mathit{\beta}\Rightarrow \mathrm{cos}\left(\frac{n}{{\mathit{\beta}}^{i}}\right)$ ,mod operation corresponding to periodic function  
NTK-Aware RoPE: [High frequency interpolation, Low extrapolation](https://zhuanlan.zhihu.com/p/8306958113)  
  Imagine that each sinusoidal function represent a spinning circle with frequency ${10000}^{2i/d}$,
  Thus smaller i, faster spinning. Take clock as a concrete example, second hand spins faster, hour hand spins lowest. Their combination makes a 60-based 3 digits code. One movement of hour hand requires 60 times spins of minute hand.
  In that way, we can also take binary as 2-scale clock.  
  During training, every spot in circle of high frequency has been seen by model, thus for OOD input, we can directly extrapolate it instead of interpolation (which will higher the frequency, making model hard to distinguish nearby positions), but interpolate it for low frequent digit, as their slow motion makes mass spots unexplored so that model can not handle OOD spots.
  Thus low frequent digit becomes lower so to keep position in explored region.
  ![](image_10.409b56b2.jpg)

Relative position: Relation between position p and p+k

$$
\mathrm{M}\left[\begin{array}{c}\mathrm{sin}\left({\mathit{\omega}}_{i}p\right)\\ \mathrm{cos}\left({\mathit{\omega}}_{i}p\right)\end{array}\right]=\left[\begin{array}{c}\mathrm{sin}\left({\mathit{\omega}}_{i}\left(p+k\right)\right)\\ \mathrm{cos}\left({\mathit{\omega}}_{i}\left(p+k\right)\right)\end{array}\right],{\mathit{\omega}}_{i}=\frac{1}{{10000}^{2i/d}}
$$

$$
\Rightarrow M=\left[\begin{array}{cc}\mathrm{cos}\left({\mathit{\omega}}_{i}k\right)& \mathrm{sin}\left({\mathit{\omega}}_{i}k\right)\\ -\mathrm{sin}\left({\mathit{\omega}}_{i}k\right)& \mathrm{cos}\left({\mathit{\omega}}_{i}k\right)\end{array}\right],a\ Rotation\ Matrix
$$

Insights
1. Relative information matters much, as we care more about relationship to the words around a specific word
2. Simply adding positional embedding to token embedding pollution the intrinsic sematic information (by modifying its norm and decreasing SNR)
3. Prior of attention: nearby words should have more influence than distant one
Attention weight calculated by dot product

$$
{\mathrm{A}}_{i,j}=\left|{q}_{i}\right|\left|{k}_{j}\right|\mathrm{cos}\mathit{\theta}
$$


We can find that Sinusoidal Encoding violates Insights due to destruction of long-term decay after applying linear transformation. Further, addition makes it worser.

$$
{\mathrm{q}}_{t}{k}_{t+\Delta t}^{T}=\left({x}_{t}+{p}_{t}\right){W}_{Q}{W}_{K}^{T}\left({x}_{t+\Delta t}^{T}+{p}_{t+\Delta t}^{T}\right)
$$

$$
={x}_{t}{W}_{Q}{W}_{k}^{T}{x}_{t+\Delta t}^{T}+{x}_{t}{W}_{Q}{W}_{K}^{T}{p}_{t+\Delta t}^{T}+{p}_{t}{W}_{Q}{W}_{K}^{T}{x}_{t+\Delta t}^{T}+{p}_{t}{W}_{Q}{W}_{K}^{T}{p}_{t+\Delta t}^{T}
$$

Long-term decay of ${p}_{t}{W}_{Q}{W}_{K}^{T}{p}_{t+\Delta t}^{T}$ fail after applying linear transformation
![](image_11.c8855578.jpg)

Thus we can encode the prior(relative position) as rotation apply to token embedding, without changing its norm, nearby words have relatively small rotation angle.

$$
\mathrm{R}\left(q,p\right)=\left[\begin{array}{ccc}{M}_{i}& \cdots & 0\\ \vdots & \ddots & \vdots \\ 0& \cdots & {M}_{d/2}\end{array}\right]\left[\begin{array}{c}{q}_{1}\\ {q}_{2}\\ \begin{array}{c}\vdots \\ {q}_{d}\end{array}\end{array}\right],{M}_{i}=\left[\begin{array}{cc}\mathrm{cos}\left({\mathit{\omega}}_{i}p\right)& \mathrm{sin}\left({\mathit{\omega}}_{i}p\right)\\ -\mathrm{sin}\left({\mathit{\omega}}_{i}p\right)& \mathrm{cos}\left({\mathit{\omega}}_{i}p\right)\end{array}\right]
$$

For N-D inputs, RoPE can be applied to each dimension independently.
As for the posterior attention pattern (e.g. high correlation between object and its distant pronoun) will learn through training.

[**Flash Attention**](https://zhuanlan.zhihu.com/p/642962397)  
Most efficient transformer focus on reduction of FLOPS, while the bottleneck rest in memory access cost. Flash attention aims at cutting MAC by **chunking huge matrix into small blocks** which can be accessed through SRAM (which has fastest IO speed).
![](image_12.5da1ec60.jpg)

IO of self-attention conduct in HBM, which has high IO delay than SRAM
![](image_13.15da4b9d.jpg)
Dynamic Incrementally Update Softmax
Since the softmax operation involves summation of all elements, the main issue is to also chunking computation of softmax into blocks.
The traditional way of softmax

$$
\mathrm{softmax}\left({x}_{i}\right)=\frac{{e}^{{x}_{i}}}{{\sum}_{i}{e}^{{x}_{i}}}
$$

In case of overflow, subtraction to maximum will be applied

$$
\mathrm{m}=\mathrm{max}\left\{{x}_{1},\dots ,{x}_{B}\right\}
$$

$$
f\left(x\right)=\left[{e}^{{x}_{i}-m},\dots ,{e}^{{x}_{B}-m}\right]
$$

$$
l\left(x\right)=sum\left(f\left(x\right)\right)
$$

$$
\mathrm{softmax}\left(x\right)=\frac{f\left(x\right)}{l\left(x\right)}
$$

For chunking version, considering chunk $x$ into 2 blocks $x=\left[{x}^{\left(1\right)},{x}^{\left(2\right)}\right]$, and apply softmax on block 1

$$
{\mathrm{m}}_{1}=\mathrm{max}\left\{{x}_{1}^{\left(1\right)},\dots ,{x}_{B}^{\left(1\right)}\right\}
$$

$$
f\left({x}^{\left(1\right)}\right)=\left[{e}^{{x}_{i}^{\left(1\right)}-{m}_{1}},\dots ,{e}^{{x}_{B}^{\left(1\right)}-{m}_{1}}\right]=\left[{e}^{{x}_{i}^{\left(1\right)}},\dots ,{e}^{{x}_{B}^{\left(1\right)}}\right]\bullet {e}^{-{m}_{1}}
$$

$$
l\left({x}^{\left(1\right)}\right)=sum\left(f\left({x}^{\left(1\right)}\right)\right)={e}^{-{m}_{1}}\bullet {\sum}_{i}{e}^{{x}_{i}^{\left(1\right)}}
$$

$$
\mathrm{softmax}\left({x}^{\left(1\right)}\right)=\frac{f\left({x}^{\left(1\right)}\right)}{l\left({x}^{\left(1\right)}\right)}
$$

And mark global maximum and summation as ${{m}_{max}={m}_{1},\ \ \ l}_{all}=l\left({x}^{\left(1\right)}\right)$
Without knowing of full elements, the results may different from the real one. But we can use another block to update it. In the same way, we have ${\mathrm{m}}_{2},f\left({x}^{\left(2\right)}\right),l\left({x}^{\left(2\right)}\right),\mathrm{softmax}\left({x}^{\left(2\right)}\right)$

$$
{\mathrm{m}}_{max}^{new}=\mathrm{max}\left\{{m}_{max},{m}_{2}\right\}
$$

$$
{l}_{all}^{new}=l\left({x}^{\left(1\right)}\right)\bullet {e}^{{m}_{max}-{m}_{max}^{new}}+l\left({x}^{\left(2\right)}\right)\bullet {e}^{{m}_{2}-{m}_{max}^{new}}
$$

$$
{f}^{new}\left({x}^{\left(1\right)}\right)=f\left({x}^{\left(1\right)}\right)\bullet {e}^{{m}_{max}}\bullet {e}^{-{m}_{max}^{new}}=f\left({x}^{\left(1\right)}\right)\bullet {e}^{{m}_{max}-{m}_{max}^{new}}
$$

$$
{\mathrm{softmax}}^{\mathrm{new}}\left({x}^{\left(1\right)}\right)=\mathrm{softmax}\left({x}^{\left(1\right)}\right)\bullet {e}^{{m}_{max}-{m}_{max}^{new}}\bullet \frac{l\left({x}^{\left(1\right)}\right)}{{l}_{all}^{new}}
$$

The same update rule for block 2

$$
{\mathrm{softmax}}^{\mathrm{new}}\left({x}^{\left(2\right)}\right)=\mathrm{softmax}\left({x}^{\left(1\right)}\right)\bullet {e}^{{m}_{2}-{m}_{max}^{new}}\bullet \frac{l\left({x}^{\left(1\right)}\right)}{{l}_{all}^{new}}
$$

And then update global maximum and summation, and store them into SRAM

$$
{\mathrm{m}}_{max}={m}_{max}^{new},\ \ {l}_{all}={l}_{all}^{new}
$$

For case of more blocks, such update rule can be iteratively executed till getting global softmax result.
Also, in Flash Attention V2, divide to summation when calculate local softmax was cancelled since the denominator will be cancelled out in each update. Assume that in t update round,

$$
{\mathrm{softmax}}^{\mathrm{t}}\left({x}^{\left(i\right)}\right)=\frac{{f}^{t}\left({x}^{\left(i\right)}\right)}{l\left({x}^{\left(i\right)}\right)}\bullet \frac{l\left({x}^{\left(i\right)}\right)}{{l}_{all}^{1}}\bullet \frac{{l}_{all}^{1}}{{l}_{all}^{2}}\dots \frac{{l}_{all}^{t-1}}{{l}_{all}^{t}}
$$

It causes redundant computation, thus we can modify it to no-divide-softmax, and only apply division until we get the global summation

$$
\mathrm{softmax}\left({x}^{\left(i\right)}\right)={f}^{new}\left({x}^{\left(i\right)}\right)
$$

During the updating, we only need to store 2 scalars in SRAM instead of a full vector.
In conclusion, Flash Attention splits Q, K, V into small blocks ${\mathrm{Q}}_{b},{K}_{b},{V}_{b}$ and do self attention on them. And then using the incremental updating rule to get global softmax.
Further, in Flash Attention V2, calculation of blocks of being masked will be skipped.  
**Collective Operations**  
Distributed training of LLM can be abstract as collective operations. i.e. Split training computation into different GPUs, results of which will be gathered into a main site and reducing to final result, which in turn will be broadcasted to different GPUs to continue the collective circle. Thus the bottleneck rests in communication.
Such process is called All Reduce.
1. Reduce(N to 1): reduce(sum) multiple computation from different sites results into one main site
2. Broadcast(1 to N): Main site broadcasts reduced results to other sites
Generally, main site maybe the bottleneck since it takes too much word load.
Scatter-version of All Reduce: split computation into different slices, different sites handle All Reduce for different slices, i.e. every site share burden of main site.
1. ReduceScatter(N to N): for computation slice $i$, its results in different sites will be reduced in site $\mathrm{i}$
2. AllGather(N to 1):
  a. Gather: site $\mathrm{i}$ broadcast its reduced result of slice $\mathrm{i}$ to main site
  b. Broadcast: main site broadcast complete result to other sites

Ring-ReduceScatter / Ring-AllGather: High efficiency implementation
Core: Ring communication
1. ReduceScatter: Site $i$ sends slice $\mathrm{j}\left(j\ne i\right)$ to its next site in ring*, *in the same time, it will receive slice from predecessor site in ring. After #(slices) - 1 times send-and-receive, site $i$ get reduced version of slice $i$
2. AllGather: Site $i$ sends slice $\mathrm{i}$ to its next site in the ring*, *in the same time, it will receive slice from predecessor site in the ring. After #(slices) - 1 times send-and-receive, site $i$ complete reduced result
Computation of communication consumption = sending communication + receive communication
Give data of size $\mathrm{\Psi}$, N devices, each devices has band width $\mathit{\beta}$ and splits data into slice of $\mathrm{\Psi}/N$, AllReduce takes N-1 rounds of send-and-receive, total communication is (send and receive parallelly)

$$
\left(\mathrm{N}-1\right)\bullet \frac{\mathrm{\Psi}}{N}
$$

Total duration is

$$
\frac{\left(\mathrm{N}-1\right)\bullet \mathrm{\Psi}}{N\mathit{\beta}}\to \frac{\mathrm{\Psi}}{\mathit{\beta}},\ N\to \infty 
$$

Duration of ring-based communication almost independent to number of devices, but its total communication correlates with number of devices.
![](image_14.b8f316af.jpg)

**MoE (Mixture of Expert): Router + Multi-FFN**  
![](image_15.9d09fada.png)
1. Routing function (choose top K and fusion) How to choose ? How to fusion ?
  a. Top-K according to logits: calculate correlation between expert and token

$$
{\mathrm{h}}_{t}^{l}={\sum}_{i=1}^{N}\left({g}_{i,t}FF{N}_{i}\left({u}_{t}^{l}\right)\right)+{u}_{t}^{l}
$$

$$
{g}_{i,t}=\left\{\begin{array}{c}{s}_{i,t},\ \ {s}_{i,t}\in Topk\left(\left\{{s}_{j,t}|1\le j\le N\right\},K\right)\\ 0,\ \ otherwise\end{array}\right.,\ \ {s}_{i,t}=Softma{x}_{i}\left({{u}_{t}^{l}}^{T}{e}_{i}^{l}\right)
$$

  Note that the Topk operation makes the factor summation less than 1, which shrinks the input, but such scale variant will be scaled back in later layers (Layer Norm)
  b. Hashing: map token to expert(FFN)
  c. RL-guided gating polices learning
  d. Solve a matching problem (Linear Assignment)
b,c,d have too much computation cost
2. Expert sizes
Smaller( with smaller hidden dim), larger number of experts + a few shared experts(always activated), but too many fine-grained experts may cause more communication
3. Training objectives: How to efficiently train a sparsity gating policy ? Considering that sparse decisions are not differentiable.
  a. Reinforcement learning to optimize gating policies
  b. Stochastic perturbations: competition mechanism
  Shazeer et al 2017 – routing decisions are stochastic with gaussian perturbations.

$$
\mathrm{G}\left(x\right)=Softmax\left(KeepTopK\left(H\left(x\right),k\right)\right)
$$

$$
\mathrm{H}{\left(x\right)}_{i}={\left(x{W}_{g}\right)}_{i}+StandardNormal\left(\right)\bullet Softplus\left({\left(x{W}_{noise}\right)}_{i}\right)
$$

$$
\mathrm{KeepTopK}{\left(v,k\right)}_{i}=\left\{\begin{array}{c}{v}_{i},\ \ if\ {v}_{i}\ is\ in\ the\ top\ k\ elements\ of\ v\\ -\infty ,\ \ otherwise\end{array}\right.
$$

  Stochastic jitter in Fedus et al 2022

$$
{\mathrm{logits}}_{router}+\ \epsilon,\ \epsilon\sim U\left(1-eps,\ 1+eps\right)
$$

  Such perturbation method can gain robust(conservative) expert, but also make them less profession (less sensitive to token), causing loss of efficiency.
  c. Heuristic 'balancing' losses: system efficiency requires that use experts evenly. We hope the decision panel won't only rely on few experts.
  Switch Transformer \[Fedus et al 2022\] : auxiliary loss

$$
\mathrm{loss}=\alpha N{\sum}_{i=1}^{N}{f}_{i}{P}_{i},\ \ \left\{\begin{array}{c}{f}_{i}=\frac{1}{T}{\sum}_{x\in \mathrm{{\rm B}}}1\left[\mathrm{argmax}p\left(x\right)=i\right]\\ {P}_{i}=\frac{1}{T}{\sum}_{x\in \mathrm{{\rm B}}}{p}_{i}\left(x\right),\ \ {p}_{i}\left(x\right)={s}_{i}\end{array}\right.
$$

  Given N experts and a batch $\mathrm{{\rm B}}$ with T tokens
     ${f}_{i}$ is the fraction of tokens (from 1 to T) dispatched to expert i (mean along row)
     ${\mathrm{P}}_{i}$ is the fraction of the router probability allocated for expert i (mean of row made of $1\left[\mathrm{argmax}p\left(x\right)=i\right]$ of each column)  
    Thus loss measure of Expectation of tokens handle by an expert, since we want them used evenly, thus leading to each expert handle as less token as possible, the optimal reach when each expert only handle T/N tokens  
    The derivative w.r.t ${\mathrm{p}}_{i}\left(x\right)\ $ is $\alpha N/{T}^{2}\bullet {\sum}_{x\in \mathrm{{\rm B}}}1\left[\mathrm{argmax}p\left(x\right)=i\right]$, so more frequent use means stronger downweighting  
    Such load balancing can also be extented to different expert groups in different devices to make sure even utilization on different devices
  DeepSeek v3: per-expert biases, topk frequent, Set up a per-expert bias (making it more likely to get tokens) and use **online learning** (not necessarialy even, dynamic balancing during inference)

$$
{f}_{i}=\frac{1}{T}{\sum}_{x\in \mathrm{{\rm B}}}1\left[{p}_{i}\left(x\right)+{b}_{i}\in Topk\left(p\left(x\right)+b,k\right)\right]
$$

  Complementary sequence-wise balance loss (used in training)

$$
{f}_{i}=\frac{1}{T}{\sum}_{x\in \mathrm{{\rm B}}}1\left[{p}_{i}\left(x\right)\in Topk\left(p\left(x\right),k\right)\right]
$$

  Normalized decision fusion from Topk experts

$$
{g}_{i,t}=\frac{{g}_{i,t}^{\prime}}{\sum {g}_{j,t}^{\prime}}
$$

$$
{g}_{i,t}^{\prime}=\left\{\begin{array}{c}{s}_{i,t},\ \ {s}_{i,t}\in Topk\left(\left\{{s}_{j,t}|1\le j\le N\right\},K\right)\\ 0,\ \ otherwise\end{array}\right.
$$

$$
{\mathrm{s}}_{i,t}=Sigmoid\left({u}_{t}^{T}{e}_{i}\right)
$$

  d. Training/finetuning stability
  Using float32 for router and add aux z-loss (constraint denominator of softmax close to 1)

$$
{L}_{z}\left(x\right)=\frac{1}{B}{\sum}_{i=1}^{B}{\left(\mathrm{log}{\sum}_{j=1}^{N}{e}^{{x}_{j}^{\left(i\right)}}\right)}^{2}
$$

  e. Communication cost loss (DeepSeek v2)
  Top-M devices select(touting), then do Top-K experts select on each selected device
  Here ${f}_{i}$ turns into frquent of tokens been send to sepecific device

$$
{f}_{i}=\frac{D}{MT}{\sum}_{t=1}^{T}1\left[Token\ t\ is\ sent\ to\ Device\ i\right]
$$

4. System side: parallel MoE on more devices
Experts on different decices choose token: load balancing across devices
5. Up-cycling: turn dense model (with one FFN) to sparse one (add MoE)
