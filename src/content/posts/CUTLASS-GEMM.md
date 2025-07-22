---
title: CUTLASS-GEMM
published: 2023-06-21
description: "Matrix Multiplication using CUDA"
tags: ["CUDA", "Matrix Multiplication", "Parallel Programming"]
category: CUDA
draft: false
---

**Conclusion**  
1.  **Style of CUDA programming**  
!Important: codes in kernel fucntion will be executed by every thread in same block. So you have to make sure the code will not collide with itself when runing on multi-threads.

Each thread consumes its own isolated part.

2.  **layout of memory, distribution on threads**  
Kernel function often involve IO operation on memory, each thread will handle an isolated area of memory by its indices mapping. Generally, threads following its incremental indices iterativily consume memory units in row-major order, i.e.

![image1](resources/08fdbab33ba84fe986f9ff287cf890db.png)

To avoid bank conflicts, we can also take hierarchica layout of memory and its mapping threads, i.e. split memory into small blocks, and do the same linear distribution on that block.

3.  **key elements of indices mapping**  
To retrive each memory units from a thread's coverage, we need to provide:

\(1\) start position of this piece of memory region

\(2\) stride(offset) to next unit

But most of important is to figure out the unit of coordinate system, and make all indices be calculated under same unit. e.g.

![image2](resources/5cd7cf193f4b4e618ced60d7bf2c106b.png)

![image3](resources/2f31ea1123c24238bcf9cfa1019ba6ee.png)

start position = (a, b), threadX = 2, threadY=3 strideX = 2, strideY = 1, traverse:

for i in 0…threadY:

for j in 0…threadX:

x = i \* strideX;

y = j \* strideY;

…..

(a+x, b+y) is the position of memory element

4.  **strategy for dealing with out of boundary elements**  
Such case happens when data size can not even divided by number of threads, then there are threads on data border have part of their thread tiles cross the effective data

see more detail at <https://nichijou.co/cuda3-thread-divergence/>

So the most important thing is to mark out which part of thread's tile is ineffective.

We can first imagine a virtual memory block is larger than real data, which is evenly divided by number of threads, then the rest is to mark memory positions which overcross the edge of real data. i.e. we generate a bit map, cell with value 1 indicates effective, while 0 indicates out of boundary which is ineffective.

Further, we can split the map into thread tile map to hold the information of each thread's effective about data.

**Source codes**  

**block_loader_wmma.h**  
[空白（横排） 4.pdf](https://onedrive.live.com/embed?resid=276CF4F2E18C3166%214519&filename=%E7%A9%BA%E7%99%BD%EF%BC%88%E6%A8%AA%E6%8E%92%EF%BC%89%204.pdf&authkey=!AKHrJVxLpStEbys)
Load block tile from global memory, and store them into shared memory

**keypoints explanation**  
1.  congruous : whether the block tile is k-major (K axis is stride axis ?)
congruousA = {TransformA = NonTranspose ?}

congruousB = {TransformB = Transpose ?}
2.  MatrixAlignBytes: n X sizeof(value_t)
3.  coordinate system unit
there exist 2 type of units

\(1\) value_t (alas: item), also unit of matrix, including

BlockItemsL, BlockItemsK, block_begin_item_coords

\(2\) ldg_vector_t (alas: ldgVectors), = n X value_t, including

Blcok tile size: BlockLdgVectorsL, BlockLdgVecorsK = BlockItemsX / n,

Blcok start: block_base_l = block_begin_item_coords.x / n, block_base_k

thread relevant (block threads are 1-dim)

Thread start: thread_offset_l = tid % BlockLdgVectorsL,

thread_offset_k = tid / BlockLdgVectorsL

Thread tile size: ThreadLdgVectorsL (distribution : Conculsion 3)

ThreadLdgVectorsK

Thread stride:

ThreadLdgVectorsL (stride on axis L, strip-mining distance between two elements of thread along L-axis) , e.g.

![image4](resources/39e6a0ccaac645a48a112d06102fe83e.png)

![image5](resources/66659008c8f941acb5393514440c9895.png)

BlockLdgVectorStrideK = max(1, BlockThreads / BlockLdgVectosL)(stride on axis K, strip-mining distance between two elements of thread along K-axis), e.g.

![image6](resources/bea49f3a40964e49806fe622a6597149.png)

**Processing frame**  
1.  Constructor
Calculate start position from block id and thread id

Generate data effective bit map
2.  request
According to data effective flag, each thread request its thread tile from source memory, all threads parallely request the block tile from source memory
3.  next
Advance to the next block tile, offset is the number of items in block
4.  commit
store each thread tile from global memory into shared memory

**wmma_accumulator.h**  

Compute warp-wide output tile by using wmma api, since wmma supports matrix multiplication of 16 X {16 X 16} X {16 X 16} X 16, i.e. per warp thread

![image7](resources/003396dcd8f24dd5abde386c6c2b465a.png)

![image8](resources/d0731a80dacc4558829f927b4c2eab86.png)

![image9](resources/e4e47c5c94de4a0f949f722f4d3f311b.png)

wmmaItemsK = 16 X wmmaItemsX

so wmma will automatically do 16 times {16 X 16} X {16 X 16} matrix multiplications, then sum them into output tile of 16 X 16

**keypoints explanation**  

unit is value_t, also can be seen from suffix of "items"

literally, it can be showed as

fragment_a \* fragment_b = accumulator

fragment = {X × Y × K}, accumulator = {X × Y} = wmmaBlock

unit is wmmaBlock, how many wmma blocks inside a warp tile

wmmaBlocksY = WarpItemsY / WmmaItemsY

wmmaBlocksX = WarpItemsX / WmmaItemsX

**block_task_wmma.h**  

Compute block output tile warp by warp, or wmmaBlock by wmmaBlock

also, store computing results from shared memory into global memory warp by warp, or wmmaBlock by wmmaBlock

**keypoints explanation**  
1.  PadItems =16
since wmma's calculation unit is 16 x 16, so a pad of 16 is added to leading dimension (i.e. non-stride axis) for alignment
2.  page_storage_t
block tile occupation on shared memory, with size StridedSmem x LdmSmem, i.e. BlockItemsK x (BlockItemsY(X) + PadItems)

PS, if UseDoubleScrathTiles = 1, there will be dual occupation on shared memory to plays as double-buffers-style of IO
3.  wmma api∷ load_matrix_sync(fragment, value\*, LdmSmem)
Notify that the third argument is the stride imformation of next wmmaBlock inside fragment, i.e.(column-major)

![image10](resources/d3e91fb3493c49e5b08e29a592083932.png)

![image11](resources/509c8a1f328940e487eff4c996ea3f16.png)

*so the second F1's postion is first F1's postion + LdmSmem, so as Fi*

**Processing frame**  
1.  Constructor
Configurate all parameters "block_loader_wmma.h" and "wmma_accumulator.h" need into \<block_task_policy\>
2.  run
\(1\) request first global prefectch by loaders

\(2\) commit first global prefectch into shared memory by loaders

\(3\) load fragment slice from shared memory, used for multiplication

each slice is a fragment it can be told from third argument of function∷request_local_prefetch,

tile_offset_k = (iteration \* WmmaItemsK + WmmaItemsK) % BlockItemsK,

which means its stride is wmmaItemsK, so an element of

local_slices_a\[WmmaBlocksY\] is exactly a fragment (see more detail in Keypoints explanation 3), and WmmaBlocksY times of loading forms a fragment slice.

So each fragment slice's stride along K axis is WmmaItemsK, but WmmaItemsY at Y axis, and each fragment is a row in the slice, i.e

so start of a fragement is (tile_offset_k, block_warp_item_coords.y + WmmaItemsX \* i) = (fk, fy)

since tile_offset_k includes % operation, so it can automatically handle mult-rows of warps. i.e

fk indicates K axis of warp, fy indicates Y axis of warp

\(4\) (dimK + BlockItemsK) / BlockItemsK times consumption

each consumption deals BlockItemsK / WmmaItemsK times multiplication, and all these results are added to corresponding accumulators. i.e, each grid is a warp, WmmaItemsK long at K axis

![image12](resources/ccfb964db947434d851e707380985da5.png)

![image13](resources/bbfe6003ac73474e819c676c8e85ada4.png)

![image14](resources/3794fd9847f24fafb20fd1789fa6c538.png)

*different row of warp is indicated by fy*

if UseDoubleScratchTiles is set, then multiplication and prefetch next fragment slice will run parallel.

PS: commit next block tile into shared memory will execute in the last warp.

\(5\) epilogue, store accumulator tile to global memory, for each wmmaBlock in warp output tile, read and write data by thread lane id

lane_id = threadIdx.x % 32, column(K)-major

lane start = (lane_id / WmmaItemsY, lane_id % WmmaItemsY)=(lx, ly)

\|ItemX\|

![image15](resources/ebd32f868f2d45798020b96186eed908.png)

![image16](resources/c0c7c4c206e74d66b176817e13823b87.png)

ItemX = 32 / WmmaItemsY, IterationX = WmmaItemsX / ItemX

IterationX indicates thread i's iteration on wmmaBlock

![image17](resources/0bea4ff4ce794def9223a494443557a1.png)

by the same start-stride method, item of unit accumulator's postion in the matrix C(in global memory, c_ptr) can be achieved

**PS: k_slpit_control.h**  

this module add parallel along K axis,

shortage of original

primary strategy directly makes threadblock do dim_k / BlockItemsK iteration along K axis of matrix, the concurrency will not be fully used when dim_k is huge.

advance

k_split_control instead split dim_k into couples of smaller slices, each slices with length split_k at K axis, and apply original strategy on this split_k slices with different threadblocks. This add concurrency factor with dim_k / split_k, i.e.

![image18](resources/44c1360923e248648d861493d5ab6edb.png)

\_\_\_\_\_\_\_\_\_\_\_\_

![image19](resources/2df63746ca974c24942a3b7e03abcec5.png)

\_\_\_\_\_\_\_\_\_\_\_\_

![image19](resources/2df63746ca974c24942a3b7e03abcec5.png)

\_\_\_\_\_\_\_\_\_\_\_\_

![image20](resources/ad0965d4d9c74d59a74420ee3c53e924.png)

\|split_k \| \_\_\_\_\_\_\_\_\_\_\_

![image21](resources/16980685cf214532b5e878cc7c41b9ae.png)

*block output tile*

*from here, we **surprisily found out** this strategy is **hierachically** used in different tile level, from block to warp to wmmablock!*

*But in block level, we need to manually update accumulator from different threadblocks, since threads only share same shared memory in same threadblock, so here k_split_control apply machnism of signals to synchronizing accumulators from different threadblocks, i.e.*

*after each threadblock concurrently generate their results,*

*predecessor threadblcok's result will be loaded from global memory as addend to next one to update its result, then updated result will be stored into global memory, repeat this process til the last threadblock, see the picture below:*

![image22](resources/c6ce41c03d5c40179d05e3fe1606a107.png)

![image23](resources/19119d31df61402c9e91793684300d12.png)

![image24](resources/40e9582a6a804e449168dac08c389f92.png)

![image25](resources/def37b7c52cc4db089f4c0d4b21ee48d.png)

![image26](resources/17a67593c1dd4a0b83e60e6bc9830aa1.png)
