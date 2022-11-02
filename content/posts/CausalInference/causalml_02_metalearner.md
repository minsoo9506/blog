---
title: "[Causality] Metalearners (X-learner)"
date: 2022-11-03T09:00:00+00:00
draft: false
categories: ["Causality"]
tags: ["Metalearners", "X-learner", "Causal Inference"]
---

heterogeneous treatment effect를 추정하는 metalearners방법론들 중에서 X-learner에 대해 알아보자.

<!--more-->

heterogeneous treatment effect를 추정하기 위한 다른 알고리즘들이 있다. metalearner에서 S, T-learner와 causalforest가 대표적인 그 예이다. 하지만 X-learner를 소개하는 논문에서는 X-learner가 가장 좋다고 소개한다. X-learner를 사용하는 주 목적은 CATE를 구하는 것이다. CATE는

$$\tau(x) = E[Y(1) - Y(0) | X=x]$$

## X-learner

1. 아래의 response functions를 ML 모델을 통해서 estimate한다. treatment group과 control group을 나눠서 각각 ML 모델을 fit하면 된다.

$$\mu_0 (x) = E[Y(0)|X=x] \\ \mu_1 (x) = E[Y(1)|X=x]$$

2. treatment, control group 각각 실제 outcome과 위에서 구한 ML 모델을 이용하여 treatment effect를 구한다. 논문에서는 이를 imputed treatment effect라고 부른다.

$$\tilde{D}_i^1 = Y_i^1 - \hat{\mu}_0(X_i^1) \\ \tilde{D}_i^0 = \hat{\mu}_1(X_i^0)- Y_i^0$$

- 만약에 $\hat{\mu}_0=\mu_0,\hat{\mu}_1=\mu_1$이면 (잘 추정했으면) $\tau(x)=E[\tilde{D}^1|X=x]=E[\tilde{D}^0|X=x]$이다.

3. $\tau(x)$를 estimate하기 위해 imputed treatment effect를 reponse variable로 해서 treatment, control group 각각 $\hat{\tau}_1(x),\hat{\tau}_0(x)$을 구한다. 이 또한 ML 모델을 fit해서 구한다.

4. CATE estimate를 weighted average하여 구한다. weight는 주로 propensity score를 사용한다.

$$\hat{\tau}(x)=g(x)\hat{\tau}_0(x) + (1-g(x))\hat{\tau}_1(x)$$

<center>
    <img src="https://github.com/minsoo9506/blog/blob/master/static/blog-imgs/causality_x_learner.png?raw=true"  width="500">
</center>

## Code

## Reference

- [Metalearners for estimation heterogeneous treatment effects using machine learning, 2019](https://www.pnas.org/doi/epdf/10.1073/pnas.1804597116)
- https://matheusfacure.github.io/python-causality-handbook/21-Meta-Learners.html
