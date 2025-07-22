---
title: Tensor Product
published: 2025-03-01
description: "How to represent structured objects in connectionist models using tensor product"
tags: ["Data encode", "Connectionist models", "PDP", "Data decode"]
category: Top-Design
draft: false
---

Tensor Product (Generalization of outer product to higher order products)  
![image1](resources/bb6c60ab86974a6ea8efcf109ca99c0f.png)  
Connectionist representations are patterns of activity over connectionist networks

Main topics
1.  Distributed representation of Symbolic Structures in Connectionist Systems  
![image2](resources/5e8a40337e2d4770b343f883457b7864.png)

Mapping structured objects to vector space  
2.  Variable Binding  
Binding a value(filler) to a variable(role, or placeholder, slot)

Representing structured objects  
Analysis of Structure
1.  (Structure)Role Decomposition  
![image3](resources/adeadc738498452d83656237bd5e64a8.png)

![image4](resources/647491ae81944d649ee84ef501bbd4aa.png)

![image5](resources/0e1bbacd06f54913b1941f231f74f17e.png)

![image6](resources/1a8b4dddfa5c4951b76805dc46ca6e03.png)

![image7](resources/515fab68ca0d47cba84e06d4fddd2b9b.png)

![image8](resources/1b2ebdbec4fa4dcabcc300a912d410f9.png)

![image9](resources/23c38ad3b945412698c909266069dede.png)

![image10](resources/33df199f79cb454cb7a75597f7e786ea.png)

So the filler/role representation of S **induced** by the role decomposition can be

![image11](resources/c08f93a51fff47a2a7947269bae4fb42.png)

![image12](resources/652734d08d2a421e9c759b1f2573c9fd.png)

![image13](resources/3e589126db284db0bc607caa45039ef9.png)

![image14](resources/b37adf35b2f448b9801920095445da31.png)

![image15](resources/33674d128983439fbc65cdc10d8dbbe8.png)  
2.  Representing conjunctions, predicate of role decomposition for structure  
![image16](resources/000317dbf65c45a6b667a8e94c2bd945.png)

![image17](resources/cbc89d9af282424dbdad7b1462c9035b.png)

![image18](resources/8bfbb0be1bb84274bdc4f09360ccf712.png)

Conjunction in connectionist models is pattern superposition, i.e. vector addition

![image19](resources/d522adfe79364378bfc4a6a940b934a1.png)  
3.  Representing variable/value bindings in Connectionist model  
![image20](resources/ed1da16958c140cf8f708d4d3fcc5b51.png)

![image21](resources/bdf6b790f1cb4eaea8374ab9b69a5d7c.png)

![image22](resources/0979878a7aa64593b990a807bf1b09aa.png)

![image23](resources/aec405df26b442449181e0f12a4225d3.png)

Tensor product representation for filler/role bindings

![image24](resources/39b798f8d3b44a10b156fad2804873f4.png)

![image25](resources/1d85bf1281134272b3a19739af05bb23.png)

![image26](resources/500bef6c202646fba0e90163b957672c.png)

Putting all together

![image27](resources/2a79469f567446d59ba56537f805f7ce.png)

From local representation to distributed representation  
1.  Local representations  
![image28](resources/3a239c824b88409da2c4d24afa4b6247.png)

![image29](resources/18a56de9ba2e4dbf93624f6a27c2cf90.png)  
2.  Semi-local (or role register) representations  
![image30](resources/c59ac1d6f9384109bd429ae5e3e2d8d7.png)  
3.  Fully distributed representations  
![image31](resources/1b431aba19d74034b1ac05f77caa4b78.png)

For composite role, which is also a symbolic object

![image32](resources/b99a3b28667d417c9bc497caf943f7ea.png)

![image33](resources/4f8623251f584ce7a1d4253316a321a0.png)  
4.  Their relations  
[Isomorphism under linearity](onenote:#PDP%20(Parallel%20distributed%20processing)&section-id={7C05A5A2-335F-4120-B309-F2C7D1ABD289}&page-id={1D6B13CF-A9E2-4773-A853-3E16E748BA28}&object-id={43DA6FD2-BC44-0926-369A-4EC96652250D}&E7&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/Blog.one) (PDP)

Properties of tensor product Representation  
Unbinding: extract filler for a particular role from tensor product representation

![image34](resources/acefebc0811c41ac855bea2ed278d3c8.png)

![image35](resources/e3698c7f89684977bb763c9dcfa1a226.png)

![image36](resources/82779be349c44668a085ed6a8b4a6513.png)

![image37](resources/9a4193282a7d42deaa55f27d50cb89c8.png)

![image38](resources/5782efb45b134452a12bb9ee4e3320da.png)

![image39](resources/49de9a2bce554a6db0fc02a960dd9c5b.png)

For linear dependent case, there will be intrusion from other roles

![image40](resources/20ce89ab05424907a0eece19199aaba5.png)

The intrusion of role j into role i, is

![image41](resources/c8439db311854276b7f813b656dde40e.png)

Unbinding result will be

![image42](resources/6d166f4d1b9442cda2985174aa55377e.png)

![image43](resources/ec83bf57bc574447913367a4843f2148.png)

For no-single-valued case, unbinding result will be superposition of all fillers bound to that role, and vice versa

Unbounded size of structures represented in fixed connectionist network leads to saturate gracefully e.g. collapse of K-V cache

First let's define case of unbounded sensitivity(capacity)

![image44](resources/2caec644bfa245dca437353888eb41f9.png)

![image45](resources/46db8f1f9e2c464e8cc5f37d35f08a70.png)

![image46](resources/d14fcd22ca244a08bec3da75b5aba559.png)

Extension from continuous and infinite to discrete and finite cases

Properties of Variable Binding
Binding operation performed in a connectionist network

Generating independent to maintaining bindings

Extraction of constituents of structure in a connectionist network

Recursive variable binding: using value as variable

Representation can be used recursively

Retrieval of representation of structured data stored in connectionist memories

Optimality of representation and learning algorithm

