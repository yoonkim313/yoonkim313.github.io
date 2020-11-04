---
layout: category-post
title:  Out of Distribution Tasks
date:   2020-11-04 05:00:00 -0000
use_math: true
categories: paper_reviews
---
## :blue_book: Likelihood Ratios for Out-of-Distribution Detection [NeurIPS 2019]
[paper] <https://arxiv.org/abs/1906.02845>
> ## Detecting OOD inputs
> > - Should have predictions with **low** confidence ex.) medical diagnosis, autonomous driving
> > - How to **detect OOD Inputs**
>>> 1. Train a generative model and use that to detect OOD inputs -> Such method puts higher likelihood on OOD inputs  :x:
>>> 2. 이 논문에서는 "General Population level background statistics"를 Likelihood Ratio method과 함께 사용하여 OOD inputs를 구별하고자 한다
>## Likelihood Ratio Model
>> - PixelCNN, FLOW와 같은 generative model은 in-distributional data보다 OOD data에 더 높은 likelihood를 책정하는 경우가 생긴다. 
>> - $x = x_S + x_B$ where $x_B$ is for background info and $x_S$ is for semantic info
>> - When evaluating the generative model, we discard the background information to ensure that the LR is not dominated by $x_B$.
>> - 하지만 input을 background와 semantic으로 나누는 것은 어렵다. $\rightarrow$ 실제로는 인풋에 perturbation을 넣어서 모델 $p_{\theta_0}$이 **population level background statistics**를,   모델 $p_{\theta}$이 in-distribution 데이터에서 semantic 위주로 배우도록 한다.
	
	Perturbation을 넣는 방법은 genetic mutations에서 착안함. 이미지의 경우 임의의 픽셀값을 [0,255] 중에서 원래의 값과 동일한 확률을 가지고 있는 다른 값으로 대체한다. 이 과정을 거친 이미지는 semantic 정보는 잃지만 background 정보는 여전히 가지고 있다.
>> - $LLR = log \frac{P_{\theta_0}}{P_{\theta}}=log \frac{P_{\theta_0}(x_B)P_{\theta_0}(x_S)}{P_{\theta}(x_B)P_{\theta}(x_S)} 
>> \approx log P_{\theta_0}(x_S) - log P_{\theta}(x_S)$ 
>> ($\because$ Both models capture the background information equally well, that is $p_θ (x_B ) ≈ p_{θ_0} (x_B )$)
>> - 모델 p_{\theta}의 경우 semantic information을 더 잘 가지고 있다

> ## Likelihood Ratio for AR models
>> - 같은 방식으로 probability distribution을 background와 semantic으로 분해 가능하다.
>> - $LLR(x) \approx \sum{log p_\theta(x_d|x_{<d})} - \sum{log p_{\theta_0}(x_d|x_{<d})} = \sum {log \frac{p_\theta(x_d|x_{<d})}{p_{\theta_0}(x_d|x_{<d})}}$


## :green_book: Deep Anomaly Detection with Outlier Exposure [ICLR 2019]
> ## Outlier Exposure
> > - Out of Distribution에 해당하는 데이터를 모델에 학습시켜서 OOD detection의 성능을 높이는 방식
> > 


## :closed_book: Augmix: A Simple Data Processing method to Improve Robustness and Uncertainty
