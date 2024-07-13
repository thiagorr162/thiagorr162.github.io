---
title: "BlockBoost: Scalable and Efficient Blocking through Boosting"
collection: publications
permalink: /publication/blockboost
excerpt: "We introduce BlockBoost, a novel boosting-based method that generates compact binary hash codes for database entries, through which blocking can be performed efficiently"
date: 2024-04-18
venue: 'AISTATS'
paperurl: 'https://proceedings.mlr.press/v238/ramos24a.html'
author_profile: false
---

As datasets grow larger, matching and merging entries from different databases has become a costly task in modern data pipelines. To avoid expensive comparisons between entries, blocking similar items is a popular preprocessing step. In this paper, we introduce BlockBoost, a novel boosting-based method that generates compact binary hash codes for database entries, through which blocking can be performed efficiently. The algorithm is fast and scalable, resulting in computational costs that are orders of magnitude lower than current benchmarks. Unlike existing alternatives, BlockBoost comes with associated feature importance measures for interpretability, and possesses strong theoretical guarantees, including lower bounds on critical performance metrics like recall and reduction ratio. Finally, we show that BlockBoost delivers great empirical results, outperforming state-of-the-art blocking benchmarks in terms of both performance metrics and computational cost.

![BlockBoost](/images/publications_preview/blockboost.png 'BlockBoost')

## References
- [Main Paper](https://proceedings.mlr.press/v238/ramos24a.html)
- [Github Repo](https://github.com/thiagorr162/blockboost)
