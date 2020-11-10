
---
layout: category-post
title:  Non-Auto Regressive Model
date:   2020-11-10 05:00:00 -0000
categories: paper_reviews
use_math: true
---

## :blue_book: An EM Approach to Non-autoregressive Conditional Sequence Generation [ICML 2020]
[paper] <https://arxiv.org/abs/2006.16378>
> ## AR vs NAR
> - AR model has SOTA performance but very slow in inference
> - NAR model has lower performance but faster in inference
NAR model removes the dependency between $y_i$ and $y_{>i}$ 
> - AR --> $P(y_i|X, y_{>i})$
> - NAR --> $P(y_{>i}|X,T_i)$


> ## Multi-Modality of NAR models
> 1. Multi-modality is a phenomenon in which the input sequence has multiple cases of output sentences
>- This arises because AR model depends on the previous output tokens recursively produced by input sequence and the output sequence but NAR model is only provided with the input sentence.
2. One of the related works used knowledge distillation by training a **teacher AR model** with ground-truth data. Then NAR model is trained with input sequence $X$ and pretriained-AR model-predicted output sequence $\hat y$
> - However such single-pass distillation method is sub-optimal
> - This paper addresses optimality by using EM algorithm on NAR model

> ## EM approach on training NAR model
> 1. Train student (NAR) on teacher (AR) with closed loop.
>  2. The models are **guaranteed to converge to a local optimum**
>  3. Removes duplicate output tokens using plug and play decoding module.
>  4. Experiments on three NMT benchmarks $\rightarrow$ Best NAR model performance

> ## Given input sequence $X$  infer target data $Y$ 
> $$Y^* = arg min CM_X(Y)$$ 
> $$= arg min E_{(x,y)} \sim [-\log P^{NAR}(y|x;\theta)]$$
> - Multiple trivial solutions to $Y^*$ could exist therefore apply a constraint on $y^*$
> ### Use **Posterior Regularization** 
> - The objective Function: $min_{q \in Q }$$KL(q(Y)||P^{NAR}(Y|X;\theta))$
> $q$ is the posterior distribution of y and $Q$ is a constraint posterior set that control the quality of parallel data with a given threshold b.
>  ### E-step : $p^{NAR}$ is fixed / update posterior $q(Y)$
>  - $q^{t+1}$ = $arg min$ $KL(q(Y)||p^{NAR}(Y|X;\theta))$
>  ### M-step : posterior $q(Y)$ is fixed / update $p_\theta^{NAR}$
>  - $\theta^{t+1}$ = $arg max$ $E_q^{t+1}[\log P^{NAR}(Y|X;\theta)]$
