
---
layout: category-post
title:  Adversarial Attacks and Deep Learning
date:   2020-11-04 09:00:00 -0000
categories: paper_reviews
use_math: true
---
## :closed_book: Towards Deep Learning Models Resistant to Adversarial Attacks
 적대적 공격에 대해서 robust한 모델을 훈련시킬 수 있을까?


## A. Adversarial Attacks
>1. Saddle Point minmax optimization
>> - Inner Maximization : Find adversarial input that has high loss
>> - Outer maximization : Find model parameter to minimize the adversarial loss
> 2. Types of Adversarial Inputs
>> - FGSM(Fast Gradient Sign Method)
>> - PGD(Projected Gradient Descent)
>>> **PGD from Conditioned Optimization Problems**
>>> - $min_{x \in X} f(x), X$ is a convex set, $f(x)$ is a convex function
>>> - Our target point $x_t$ might not be in the convex set therefore let $x_{t+1} = x_t - \frac{\nabla f(x_t)}{L}$ where $x_{t+1}$ is a projection of $x_t$ onto the set $X$
>>> - $\rightarrow$ Above methods are used to create a **_good attack_**. <br>PGD is the strongest attack with local First Order information of the network. Therefore the paper suggests that **if we train a model robust against the PGD adversaries**, then it is robust against wide variety of _first order adversaries_.
    
  
-------------------------------------------------------------------

## B. Adversarial Defense
>> 1. Including FGSM/PGD inputs
>>> - Might not learn the _universal representation_ and overfitting to the perturbation 
>>> - Larger network capability needed
>>> ![Desktop View](/assets/img/adversarialattacksMNIST.jpeg)<br>세번째 플랏에서 PGD를 training에 포함한 결과 모델이 충분히 큰 경우에 adversarial attack에 대해서 robust model을 만들어낼 수 있다.
>>> - Related works focused on particular attacks while this paper had a broader perspective
>> 2. Optimization on adversarial robustness
