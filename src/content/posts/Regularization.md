---
title: Regularization
published: 2023-03-23
description: "How does regularization work and what is it used for?"
tags: ["L1 decay", "L2 decay"]
category: Optimization
draft: false
---

*Bayes MAP on weights*  
*with an regularized term over weights : an introducion of prior knowledge on weights*  
![image1](resources/284801d8f06f4b06ada2580a55f8e6f4.png)  
*Note: In Neural Network, regularization on bias is not considerd, otherwise may cause under-fitting*

*Recall that Bayes classification turn into a max-min estimation when considering prior distribution. Same as regularization, wrapping original optimization problem into a max-min one.*  
![image2](resources/caf88508c8694d6fb1e7bc9385b9079b.png)
![image3](resources/a78854291e474e2b865c02fbe526661f.png)  
*we may solve this formual by iterative optimization (like [SVM](onenote:#SVM&section-id={206D0DBC-E353-4C40-ABB7-20922DEC5824}&page-id={11A9696D-1BFF-4700-8B1D-CF78A9E2CCFA}&object-id={CE2703F7-A70F-0F36-1E79-A95AB13D5E0D}&12&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/机器学习.one) or EM), but may converge to local minimum*  
![image4](resources/0af9e31fc08f40f987fb61c816ed7d0b.png)
![image5](resources/c73ec5fb3a0a41f8b2d3d86a0a75c3a8.png)

*Q: why do we need regularization ?*  
*Regularization is aim at reducing generalization error, or a trade-off between bias and variance.*
1.  *Reducing overfitting (generalization error)*
2.  *It is providing a premise for model, so when premise is satisfied with desired model, then the predicted model will converge to desired model : A→B, A true → B true. Or we can say, we are introducing some prior knowledge into model.*
3.  [*Unbias hypothesis is useless*](onenote:#Machine%20Learning%20and%20Nerual%20Network&section-id={206D0DBC-E353-4C40-ABB7-20922DEC5824}&page-id={0120613B-6AA7-47C0-ABEE-002AB1B2FB47}&object-id={BA99CE90-478A-4536-B77E-0585FA97E540}&2B&base-path=https://d.docs.live.net/276cf4f2e18c3166/文档/寿枫%20的笔记本/机器学习.one)
4.  *Numeric steady, benifical to optimization*
*Q: How does it work? Or what exectlly is the process of regularization*
*regularization: Weights adjusted by sepcific rules*
*By analysing weights' gradient including **L2 regularization term***
![image6](resources/068646f862d646ce91ead3e1bfadce6d.png)  
*weight with big value will get more punishment*

![image7](resources/efcb4751d5794b62aa36fc908660834a.png)
![image8](resources/160b30dba53743929b643222fd5e3bbe.png)
![image9](resources/3d45f61624664856883cedfde1b6cfda.png)
![image10](resources/60449e9d3bf24a4eae78236ea2bf2c82.png)
![image11](resources/208f0ea5698a4db7a12a2d6762467840.png)
![image12](resources/5402651f49e44d2cb9ce5110a6a7b126.png)
![image13](resources/a95b6ca5a5b0410aa20d445d4520a11f.png)
![image14](resources/d7ed061016f144aca7106db4d9205864.png)
![image15](resources/21de06e7ecb54b9ba12b0a727fa57c04.png)  
*since weight aligned with large eigenvalue in **H** contributes most to gradient,*  
*it's better keep it still*
![image16](resources/da6664f688ae42559e4697b04a2d12f2.png)
*since weight aligned with small eigenvalue in **H** contributes almost nothing to gradient,*
*it will decay by regularization*

*Same way on L1 regularization will get*  
![image17](resources/735946e85ea74f83a78002c1a538882d.png)
![image18](resources/62330abf4b0b44f6bfa8fe57b60af2a8.png)
![image19](resources/b5aad70014f842519262dc8c20b489ea.png)
![image20](resources/b9963e811df84c14a37e6d134d435282.png)
![image21](resources/c38a9204d78c4599aafe20118256aa07.png)
![image22](resources/6ee7f86dbbb8430ebbc1917e4078bc12.png)
![image23](resources/c50d3b72a8bb486880965830de8951af.png)
![image24](resources/a4de4d73cf884132b996c9aec19af03e.png)
![image25](resources/984b4e77e12d468e99380d525ef583b0.png)  
*since weight aligned with large eigenvalue in **H** contributes most to gradient,*
*it's better keep it still*
![image26](resources/c0cc3c48c27443bcb450dce8b10b0703.png)
*since weight aligned with small eigenvalue in **H** contributes almost nothing to gradient,*
*it will directly pressed to 0, leading to a sparse solution*

*Same as L2 regularization correspond to **Gaussian prior** on weights, L1 regularization*
*is to the log-form of **isotropic Laplace prior** over weights*  
![image27](resources/cbd7e16e09d84b229061d803c3a5c673.png)
