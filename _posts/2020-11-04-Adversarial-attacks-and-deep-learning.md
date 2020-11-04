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

## :blue_book: Benchmarking Neural Network Robustness to Common Corroptions and Perturbations [ICLR 2019]

## Comparison
> 1. Corruptions
> 2. Perturbations
> 3. Adversarial Perturbations

Introduces IMAGENET-C and IMAGENET-P

## :orange_book: Can You Trust your Model's Uncertainty? Evaluating Predictive Uncertainty under Dataset Shift [NeurIPS 2019]

1. Quantify uncertainty of the model : How much of the model output should be trusted? This paper proposes a benchmark to evaluate **uncertainty under distribution shift**, not limited to iid assumptions.
2. Which strategy performs the best for shifted data(with experiments on image, text, advertising data)
3. Be aware that calibration on validation set does not guarantee good performance on shifted data.

>## Dataset to measure uncertainty
>> - Shifted inputs by corruptions and perturbations
>> These inputs fall into one of the k classes of the true data generating distribution.
 >> - Completely different OOD dataset
 >> The label is not one of k classes. The model should have higher uncertainty with such dataset.
 >## Probablistic Models to measure uncertainty
> - Bayesian Models
> > Variational Inference, Laplace approximation, dropout-based variational inference, stochastic gradient MCMC
> - Non-Bayesian Models
> > Bootstrap or resembling, recalibration of probabilities on a validation set
> - Used in this paper are:
>> Temp Scaling, Monte-Carlo Dropout, Ensembles, Stochastic Variational Bayesian Inference, Bayesian Inference for the last layer only.
>## Metrics 
>>- Negetive log likelihood
>>- Brier Score
>>> - Squared Error of the true label vector(one hot vector) and a predicted probability vector
>>> - The Brier score can be decomposed into 3 additive components: <br>
-Uncertainty: Entropy of the data distribution, Highest when the data is uniform	<br>-Reliability:  How much the prediction deviates from the observed frequency<br>-Resolution: How sharp are the predictions? 
>>- Expected Calibration Error: Correspondence between the predicted and empirical probability.


 ![Desktop View](/assets/img/can-you-trust.jpeg) 
>- Validation dataset에 대해서 조정된 모델은 test dataset에 대해서도 높은 성능을 기록했지만 Shifted input에 대해 테스트를 한 성능은 저조할 수도 있다. 특히, SVI의 경우는 다른 모델과 비교해서 val/test 성능이 낮았지만 큰 shift에 대해서 더 높은 성능을 보였다.<br> 
>- 세 번째 그림을 보면 SVI는 accuracy가 높을 때 confidence가 높았다. **High Stakes** applications에 적합하다고 함.
 ![Desktop View](/assets/img/can-you-trust-1.jpeg)
 ![Desktop View](/assets/img/can-you-trust-2.jpeg)
 **Ensemble models** 는 5 단계의 쉬프팅에 대해서 항상 우수하다. k=5개의 앙상블도 충분히 우수한 성능을 보장한다.
 
## :green_book: Deep Anomaly Detection with Outlier Exposure [ICLR 2019]


## :closed_book: Augmix: A Simple Data Processing method to Improve Robustness and Uncertainty