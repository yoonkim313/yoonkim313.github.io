---
layout: category-post
title:  Shifted Data and Robust Models
date:   2020-11-04 05:00:00 -0000
use_math: true
categories: paper_reviews
---
## :blue_book: Benchmarking Neural Network Robustness to Common Corruptions and Perturbations [ICLR 2019]

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
 