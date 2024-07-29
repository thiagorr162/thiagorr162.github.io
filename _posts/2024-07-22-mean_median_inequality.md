---
title: 'Mean-median inequality'
date: 2024-07-22
permalink: /posts/2024/07/mean_median_inequality/
tags:
  - inequality
  - mean-media
  - concentration of measure
  - probability
---

When studying the concentration of measure phenomenon, and its [relation with isoperimetric inequality](/posts/2024/07/isoperimetric_concentration_1/), we show that under regularity assumptions, some functions of random variables concentrate around their median. However, it is often common (and very useful) to write such results using the mean instead of the median. In this post, we show that these two points of view are comparable.

To this end, we will use the fact that the median $M(X)$ of $X$ minimizes 

$$
\min_{c \in \mathbb{R}} \mathbb{E}(|X - c|).
$$ 

But then, using Jensen's Inequality and the fact that $x \mapsto \sqrt{x}$ is concave:

$$
\begin{align}
|E(X) - M(X)| &=  |E(X) - M(X)| \\
              &\leq  E|X - M(X)| \\
              &\leq E|X - E(X)| \\
              & = E((X - E(X))^2)^{1/2} \\
              & \leq (E(X - E(X))^2)^{1/2} \\
              &= \sqrt{\textrm{Var}(X)}. 
\end{align}
$$

If for example $X = \frac{1}{n}\sum_{i=1}^n Z_i$ with $Z_i$ i.i.d. variables, then this result shows that $E(X)$ gets very close to $M(X)$ as $n$ grows. 


### References

- [Concentration Inequalities](https://academic.oup.com/book/26549) - S. Boucheron, G. Lugosi, P. Massart 
- [Concentration of Measure and Isoperimetric Inequalities in Product Spaces](https://arxiv.org/abs/math/9406212) - M. Talagrand
