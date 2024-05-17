---
title: "ExactBoost: Directly Boosting the Margin in Combinatorial and Non-decomposable Metrics"
collection: publications
permalink: /publication/exactboost
excerpt: "This paper introduces a fast and exact stagewise optimization algorithm, dubbed ExactBoost, that boosts stumps to the actual loss function. ![ExactBoost](/images/publications_preview/exactboost.png 'ExactBoost')"
date: 2022-05-03
venue: 'AISTATS'
paperurl: 'https://proceedings.mlr.press/v151/csillag22a.html'
---

Many classification algorithms require the use of surrogate losses when the intended loss function is combinatorial or non-decomposable. This paper introduces a fast and exact stagewise optimization algorithm, dubbed ExactBoost, that boosts stumps to the actual loss function. By developing a novel extension of margin theory to the non-decomposable setting, it is possible to provably bound the generalization error of ExactBoost for many important metrics with different levels of non-decomposability. Through extensive examples, it is shown that such theoretical guarantees translate to competitive empirical performance. In particular, when used as an ensembler, ExactBoost is able to significantly outperform other surrogate-based and exact algorithms available.

Download [here.](https://proceedings.mlr.press/v151/csillag22a.html)
