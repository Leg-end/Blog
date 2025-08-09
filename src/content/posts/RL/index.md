---
title: "RL & PPO & RLHF"
published: 2025-08-09
description: "Introduction to Reinforcement Learning, Proximal Policy Optimization, and Reinforcement Learning with Human Feedback"
tags: ["LLM", "RL"]
category: RL
draft: false
---

## [The RL Process](https://zhuanlan.zhihu.com/p/7461863937)  
[![](image_1.fbaab6eb.jpg)](https://zhuanlan.zhihu.com/p/677607581)  
Sample initial state from a prior distribution

$$
{s}_{0} \sim {p}_{0}\left(s\right)
$$

According to current env state, sample an action from a policy

$$
{\mathit{\alpha}}_{t} \sim {\mathit{\pi}}_{\mathit{\theta}}\left(s|{s}_{t}\right)
$$

Apply action on env, yielding new env state and corresponding reward. Since the process is a Markov decision process, next state only depends on previous state (Markov property)

$$
{s}_{t+1} \sim p\left(s|{\mathit{\alpha}}_{t},{s}_{t}\right)
$$


$$
{r}_{t}=R\left({s}_{t},{\mathit{\alpha}}_{t},{s}_{t+1}\right)
$$

After a rollout of interaction, the process outputs a trajectory of state-action and corresponding return

$$
\mathit{\tau}=\left({s}_{0},{\mathit{\alpha}}_{0},{s}_{1},{\mathit{\alpha}}_{1},\dots ,{s}_{T},{\mathit{\alpha}}_{T}\right)
$$


$$
R\left(\mathit{\tau}\right)=\sum _{t=0}^{T}{r}_{t}
$$

Avoid divergent return and control degree of reward across time, we use discount return

$$
R\left(\mathit{\tau}\right)=\sum _{t=0}^{T}{\mathit{\gamma}}^{t}{r}_{t},\ \ \mathit{\gamma}\in \left(0,\ 1\right)
$$

Also, the probability of such trajectory conditional on given policy

$$
p\left(\mathit{\tau}|{\mathit{\pi}}_{\mathit{\theta}}\right)={p}_{0}\left({s}_{0}\right)\prod _{t=0}^{T}p\left({s}_{t+1}|{s}_{t},{\mathit{\alpha}}_{t}\right)p\left({\mathit{\alpha}}_{t}|{s}_{t}\right)
$$

To learn a good policy, we want to maximize the total expected reward of policy on any trajectory

$$
\underset{{\mathit{\pi}}_{\mathit{\theta}}}{argmax}J\left({\mathit{\pi}}_{\mathit{\theta}}\right)
$$


$$
J\left({\mathit{\pi}}_{\mathit{\theta}}\right)={E}_{\mathit{\tau} \sim {\mathit{\pi}}_{\mathit{\theta}}}\left[R\left(\mathit{\tau}\right)\right]=\sum _{\mathit{\tau}}R\left(\mathit{\tau}\right)p\left(\mathit{\tau}|{\mathit{\pi}}_{\mathit{\theta}}\right)
$$

Following gradient ascend, it can be simplified as

$$
J\left({\mathit{\pi}}_{\mathit{\theta}}\right)={E}_{\mathit{\tau} \sim {\mathit{\pi}}_{\mathit{\theta}}}\left[\sum _{t=0}^{T}R\left(\mathit{\tau}\right)log{\mathit{\pi}}_{\mathit{\theta}}\left({\mathit{\alpha}}_{t}|{s}_{t}\right)\right]
$$

The optimization process involves adjust policy so that yielding larger return, but it's hard to catch the influence of return on each single step's decision, as  
  A good return doesn't mean each action performs perfectly. (similar to beam-search)  
  Simply maximize probability of action leading to largest immediate reward won't guarantee maximized return thus fail to promise good policy.  
A naïve idea is to find another measurement (Value Function) to estimate return of action at time step t, in such way can we maximize probability of action bringing **Expected** larger "return"

$$
J\left({\mathit{\pi}}_{\mathit{\theta}}\right)={E}_{\mathit{\tau} \sim {\mathit{\pi}}_{\mathit{\theta}}}\left[\sum _{t=0}^{T}{\mathrm{\Psi}}_{t}log{\mathit{\pi}}_{\mathit{\theta}}\left({\mathit{\alpha}}_{t}|{s}_{t}\right)\right]
$$

According to MDP property, the discount return at time step t can be (given determined trajectory)

$$
{G}_{t}=\sum _{{t}^{\prime}=t}^{T}{\mathit{\gamma}}^{t-{t}^{\prime}}{r}_{{t}^{\prime}}
$$

The Expected larger "return" means that across different trajectories, return of preferred action often greater than mean of that across different actions (with greater advantage)

$$
{\mathrm{\Psi}}_{t}={A}_{\mathit{\pi}}\left({s}_{t},{\mathit{\alpha}}_{t}\right)={Q}_{\mathit{\pi}}\left({s}_{t},{\mathit{\alpha}}_{t}\right)-{V}_{\mathit{\pi}}\left({s}_{t}\right)
$$

Action / value function is Expectation of discount return across trajectories

$$
{V}_{\mathit{\pi}}\left({s}_{t}\right)={E}_{\mathit{\pi}}\left[{G}_{t}|{s}_{t}\right]={E}_{{\mathit{\alpha}}_{t} \sim \mathit{\pi}\left(a|{s}_{t}\right)}\left[{E}_{{s}_{t+1} \sim p\left(s|{s}_{t},{a}_{t}\right)}\left[{r}_{t}+{V}_{\mathit{\pi}}\left({s}_{t+1}\right)\right]\right]
$$


$$
{Q}_{\mathit{\pi}}\left({s}_{t},{\mathit{\alpha}}_{t}\right)={E}_{\mathit{\pi}}\left[{G}_{t}|{s}_{t},{\mathit{\alpha}}_{t}\right]={E}_{{s}_{t+1} \sim p\left(s|{s}_{t},{a}_{t}\right)}\left[{r}_{t}+\mathit{\gamma}{V}_{\mathit{\pi}}\left({s}_{t+1}\right)\right]
$$


$$
{V}_{\mathit{\pi}}\left({s}_{t}\right)={E}_{{\mathit{\alpha}}_{t} \sim \mathit{\pi}\left(a|{s}_{t}\right)}\left[Q\left({s}_{t},{\mathit{\alpha}}_{t}\right)\right]
$$


$$
{A}_{\mathit{\pi}}\left({s}_{t},{\mathit{\alpha}}_{t}\right)={E}_{{s}_{t+1} \sim p\left(s|{s}_{t},{a}_{t}\right)}\left[{r}_{t}+\mathit{\gamma}{V}_{\mathit{\pi}}\left({s}_{t+1}\right)-{V}_{\mathit{\pi}}\left({s}_{t}\right)\right]
$$

Here, ${r}_{t}+\mathit{\gamma}{V}_{\mathit{\pi}}\left({s}_{t+1}\right)-{V}_{\mathit{\pi}}\left({s}_{t}\right)$ stands estimation of advantage, which is a random variable. ${r}_{t}+\mathit{\gamma}{V}_{\mathit{\pi}}\left({s}_{t+1}\right)$ is effective return at time step t (immediate reward + discount future return, both current and future reward were considered), ${V}_{\mathit{\pi}}\left({s}_{t}\right)$ is estimated return at time step t

$$
J\left({\mathit{\pi}}_{\mathit{\theta}}\right)=\underset{{\mathit{\pi}}_{\mathit{\theta}}}{argmax}{E}_{\mathit{\tau} \sim {\mathit{\pi}}_{\mathit{\theta}}}\left[\sum _{t=0}^{T}\left({r}_{t}+\mathit{\gamma}{V}_{\mathit{\pi}}\left({s}_{t+1}\right)-{V}_{\mathit{\pi}}\left({s}_{t}\right)\right)log{\mathit{\pi}}_{\mathit{\theta}}\left({\mathit{\alpha}}_{t}|{s}_{t}\right)\right]
$$

Maximization over different time step can be simplified as maximization on each time step

$$
\Rightarrow J\left({\mathit{\pi}}_{\mathit{\theta}}\right)=\underset{{\mathit{\pi}}_{\mathit{\theta}}}{argmax}{E}_{t}\left[\left({r}_{t}+\mathit{\gamma}{V}_{\mathit{\pi}}\left({s}_{t+1}\right)-{V}_{\mathit{\pi}}\left({s}_{t}\right)\right)log{\mathit{\pi}}_{\mathit{\theta}}\left({\mathit{\alpha}}_{t}|{s}_{t}\right)\right]
$$

To get its gradient , we need to model its function with learnable parameters (e.g. using Neural Network)  
  If only policy was modeled, it's a policy-based method, return can be evaluated after multi-round of trajectory sampling  
  If only value function was modeled, it's a value-based method, action can be chosen according to its value,  
  If both were modeled, it’s an actor-critic(value) method, return of action sampled from policy can be evaluated by value function, which in turn will be used to update policy, further new policy will required updated value function.  
![](image_2.5202b977.jpg)  
Optimization objectives
Actor, learning policy, given fixed value function

$$
\underset{{\mathit{\pi}}_{\mathit{\theta}}}{argmax}J\left({\mathit{\pi}}_{\mathit{\theta}}\right)
$$


$$
J\left({\mathit{\pi}}_{\mathit{\theta}}\right)={E}_{t}\left[\left({r}_{t}+\mathit{\gamma}{V}_{\mathit{\phi}}\left({s}_{t+1}\right)-{V}_{\mathit{\phi}}\left({s}_{t}\right)\right)log{\mathit{\pi}}_{\mathit{\theta}}\left({\mathit{\alpha}}_{t}|{s}_{t}\right)\right]
$$

Critic, learning value function, given fixed policy

$$
\underset{{V}_{\mathit{\phi}}}{argmin}L\left({V}_{\mathit{\phi}}\right)
$$


$$
L\left({V}_{\mathit{\phi}}\right)={E}_{t}\left[{\left({r}_{t}+\mathit{\gamma}{V}_{\mathit{\phi}}\left({s}_{t+1}\right)-{V}_{\mathit{\phi}}\left({s}_{t}\right)\right)}^{2}\right]
$$

### Optimization Issues
1. Each optimization process requires multiple round of trajectory sampling, which is slow and at risk of large variance samples may misguide learning. And the costly sampling only update models once.
2. Generally, return evaluated from value function is biased (variance-bias trade-off)
### Solution: PPO
#### For issue 1: [importance sampling](https://1drv.ms/o/c/276cf4f2e18c3166/EmYxjOHy9GwggCdzAgAAAAAB6fDrDuRs-oHUmzbGW8JBhw?wd=target%28Blog.one%7C7C05A5A2-335F-4120-B309-F2C7D1ABD289%2FSampling%20Method%7C4F341C3A-CF66-4855-B9B3-DA4571AC8699%2F%29&wdpartid=%7b1088E25E-311D-07C3-0397-93DC717CFA97%7d%7b1%7d&wdsectionfileid=276CF4F2E18C3166!4466)  
  Off-policy: Reuse sampled trajectories multiple times to get iteratively updated policies: ${\mathit{\pi}}_{{\mathit{\theta}}_{1}},{\mathit{\pi}}_{{\mathit{\theta}}_{2}},\dots ,{\mathit{\pi}}_{{\mathit{\theta}}_{k}}$
  Since update new policy with old data equivalents to estimate objective with new policy on samples from old one, thus an importance weight was need

$$
{E}_{x \sim p\left(x\right)}\left[f\left(x\right)\right]={E}_{x \sim q\left(x\right)}\left[\frac{p\left(x\right)}{q\left(x\right)}f\left(x\right)\right]
$$


$$
\Rightarrow J\left({\mathit{\pi}}_{\mathit{\theta}}\right)=\underset{\mathit{\tau} \sim {\mathit{\pi}}_{{\mathit{\theta}}_{old}}}{{E}_{t}}\left[\frac{{\mathit{\pi}}_{\mathit{\theta}}\left({a}_{t}|{s}_{t}\right)}{{\mathit{\pi}}_{{\mathit{\theta}}_{old}}\left({a}_{t}|{s}_{t}\right)}\left({r}_{t}+\mathit{\gamma}{V}_{\mathit{\phi}}\left({s}_{t+1}\right)-{V}_{\mathit{\phi}}\left({s}_{t}\right)\right)log{\mathit{\pi}}_{\mathit{\theta}}\left({\mathit{\alpha}}_{t}|{s}_{t}\right)\right]
$$

  But the diversity between new and old policies still necessitate more sampling, a remedy is to keep new policy close to old one
  e.g. add constraint of KL-divergent between old and new policies

$$
J\left({\mathit{\pi}}_{\mathit{\theta}}\right)=\underset{\mathit{\tau} \sim {\mathit{\pi}}_{{\mathit{\theta}}_{old}}}{{E}_{t}}\left[\frac{{\mathit{\pi}}_{\mathit{\theta}}\left({a}_{t}|{s}_{t}\right)}{{\mathit{\pi}}_{{\mathit{\theta}}_{old}}\left({a}_{t}|{s}_{t}\right)}\left({r}_{t}+\mathit{\gamma}{V}_{\mathit{\phi}}\left({s}_{t+1}\right)-{V}_{\mathit{\phi}}\left({s}_{t}\right)\right)log{\mathit{\pi}}_{\mathit{\theta}}\left({\mathit{\alpha}}_{t}|{s}_{t}\right)-\mathit{\beta}KL\left({\mathit{\pi}}_{\mathit{\theta}}\left({a}_{t}|{s}_{t}\right)|{\mathit{\pi}}_{{\mathit{\theta}}_{old}}\left({a}_{t}|{s}_{t}\right)\right)\right]
$$

  Bound new policy and new value function in nearby region of old one

$$
J\left({\mathit{\pi}}_{\mathit{\theta}}\right)={E}_{t}\left[min\left[{r}_{t}\left(\mathit{\theta}\right){A}_{\mathit{\phi}}\left({s}_{t},{\mathit{\alpha}}_{t}\right),clip\left({r}_{t}\left(\mathit{\theta}\right),1-\mathit{\epsilon},1+\mathit{\epsilon}\right){A}_{\mathit{\phi}}\left({s}_{t},{\mathit{\alpha}}_{t}\right)\right]\right]
$$


$$
{r}_{t}\left(\mathit{\theta}\right)=\frac{{\mathit{\pi}}_{\mathit{\theta}}\left({a}_{t}|{s}_{t}\right)}{{\mathit{\pi}}_{{\mathit{\theta}}_{old}}\left({a}_{t}|{s}_{t}\right)}
$$


$$
\nabla f(x) = f(x) \nabla \log f(x), \quad \text{Thus we can remove } \log \pi_\theta(\alpha_t \mid s_t)
$$


$$
L\left({V}_{\mathit{\phi}}\right)={E}_{t}\left[max\left[{\left({V}_{\mathit{\phi}}^{new}\left({s}_{t}\right)-{R}_{t}\right)}^{2},{\left({V}_{\mathit{\phi}}^{CLIP}\left({s}_{t}\right)-{R}_{t}\right)}^{2}\right]\right]
$$


$$
{V}_{\mathit{\phi}}^{CLIP}=clip\left({V}_{\mathit{\phi}}^{new},{V}_{\mathit{\phi}}^{old}-\mathit{\epsilon},{V}_{\mathit{\phi}}^{new}+\mathit{\epsilon}\right)
$$


$$
{R}_{t}={A}_{\mathit{\phi}}\left({s}_{t},{\mathit{\alpha}}_{t}\right)+{V}_{\mathit{\phi}}^{old}={r}_{t}+\mathit{\gamma}{V}_{\mathit{\phi}}^{old}\left({s}_{t+1}\right)+\mathit{\gamma}\mathit{\lambda}{A}_{\mathit{\phi}}\left({s}_{t+1},{\mathit{\alpha}}_{t+1}\right),\ if\ use\ GAE
$$

  Sine ${A}_{\mathit{\phi}}\left({s}_{T+1},{\mathit{\alpha}}_{T+1}\right)=0$ , advantage at different time step can be computed using dynamic programming
#### For issue 2: GAE
  To reduce bias of value function, we may take more sampled reward into account

$$
{r}_{t}+\mathit{\gamma}{V}_{\mathit{\phi}}\left({s}_{t+1}\right)-{V}_{\mathit{\phi}}\left({s}_{t}\right)=\sum _{l=0}^{\infty}{\mathit{\gamma}}^{l}{r}_{t+l}-{V}_{\mathit{\pi}}\left({s}_{t}\right)
$$

  But which will introduce more variance, since ${\mathrm{r}}_{t}$ is random variable

$$
Var\left({r}_{t}\right)\to Var\left({r}_{t}+{r}_{t+1}+\dots \right)
$$

  GAE introduce a balance hyperparameter to control bias-variance trade-off

$$
{A}_{\mathit{\phi}}\left({s}_{t},{\mathit{\alpha}}_{t}\right)=\sum _{l=0}^{\infty}{\left(\mathit{\gamma}\mathit{\lambda}\right)}^{l}{\mathit{\delta}}_{t+l},\ \ {\mathit{\delta}}_{t}={r}_{t}+\mathit{\gamma}{V}_{\mathit{\phi}}\left({s}_{t+1}\right)-{V}_{\mathit{\phi}}\left({s}_{t}\right)
$$

  With smaller $\mathit{\lambda}$, comes greater bias, vice versa
  Recall that return of current time step includes immediate reward and future one, so is GAE advantage, controlled by $\mathit{\lambda}$

$$
{A}_{\mathit{\phi}}\left({s}_{t},{\mathit{\alpha}}_{t}\right)=\left({r}_{t}+\mathit{\gamma}{V}_{\mathit{\phi}}\left({s}_{t+1}\right)-{V}_{\mathit{\phi}}\left({s}_{t}\right)\right)+\mathit{\gamma}\mathit{\lambda}{A}_{\mathit{\phi}}\left({s}_{t+1},{\mathit{\alpha}}_{t+1}\right)
$$

-----  
## [RLHF](https://zhuanlan.zhihu.com/p/677607581)  
![](image_3.6650dafc.jpg)
### Mapping RL concept on NLP entity  
Action: next predicted token $\alpha_t$, action set = vocabulary  
State: input prompt($s_0$) + generated output (tokens) (${\mathrm{s}}_{t+1}=\left[{s}_{t},{\mathit{\alpha}}_{t}\right]$)  
Agent/policy/actor: (SFT) LLM, ${\mathit{\pi}}_{\mathit{\theta}}\left({a}_{t}|{s}_{t}\right)$  
Reward model: human rank preference, predict immediate reward at time step t

$$
\left\{\begin{array}{c}{r}_{t}=-k{l}_{ctl}log\frac{{\mathit{\pi}}_{\mathit{\theta}}\left({a}_{t}|{s}_{t}\right)}{{\mathit{\pi}}_{{\mathit{\theta}}_{ref}}\left({a}_{t}|{s}_{t}\right)},\ \ t\ne T\\ {r}_{t}=-k{l}_{ctl}log\frac{{\mathit{\pi}}_{\mathit{\theta}}\left({a}_{t}|{s}_{t}\right)}{{\mathit{\pi}}_{{\mathit{\theta}}_{ref}}\left({a}_{t}|{s}_{t}\right)}+{r}_{t},\ \ t=T\end{array}\right.
$$

  Only reward at last time step was used, as it represent reward for complete conversation (prompt + response). While reward at other time step evaluated by reference constraint (deepseed-chat)
  Note that reward at different time step can be customized
Reference model: (SFT) LLM constraint actor through KL divergent,
Critic (Value) model: predict return of specific time step t
### Optimization objectives
![](image_4.070f8271.jpg)  
Actor loss

$$
J\left({\mathit{\pi}}_{\mathit{\theta}}\right)={E}_{t}\left[min\left[{r}_{t}\left(\mathit{\theta}\right){A}_{\mathit{\phi}}\left({s}_{t},{\mathit{\alpha}}_{t}\right),clip\left({r}_{t}\left(\mathit{\theta}\right),1-\mathit{\epsilon},1+\mathit{\epsilon}\right){A}_{\mathit{\phi}}\left({s}_{t},{\mathit{\alpha}}_{t}\right)\right]\right]
$$

Critic loss

$$
L\left({V}_{\mathit{\phi}}\right)={E}_{t}\left[max\left[{\left({V}_{\mathit{\phi}}^{new}\left({s}_{t}\right)-{R}_{t}\right)}^{2},{\left({V}_{\mathit{\phi}}^{CLIP}\left({s}_{t}\right)-{R}_{t}\right)}^{2}\right]\right]
$$

