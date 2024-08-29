---
layout: post
title: 'Introduction to isoperimetric inequalities and concentration of measure'
date: 2024-07-13
permalink: /posts/2024/07/isoperimetric_concentration_1/
tags: 
    - isoperimetric 
    - concentration 
    - probability
---

Consider a metric space $$(\mathcal{X},d)$$ and a 1-Lipschitz function $$f:\mathcal{X}\to \mathbb{R}$$. Given a probability $$P$$ and a random variable $$X\sim P$$, we are interested in bounding the following quantity:

$$
P\left(f(X)\geq M(f) + t\right)\quad (\star),
$$

where $$M(f)$$ is the median of the function $$f$$ given $$P$$, that is, $$M(f)$$ is a real number such that

$$
P\left( f(X)\geq M(f) \right)\geq 1/2\quad \textrm{and} \quad P\left( f(X)\leq M(f) \right)\geq 1/2.
$$

First, given $$t\in\mathbb{R}$$, define the t-blowup of $$A$$ as 

$$
A_t := \{x\in\mathcal{X}: d(x,A)<t\}
$$

Note that, if  $$B=\left\lbrace x\in\mathcal{X}: f(x)\leq M(f)\right\rbrace$$, then for any $$x\in B$$ and $$y\in \mathcal{X}$$ such that $$d(x,y)< t$$, since $$f$$ is 1-Lipschitz,

$$
f(y)-f(x)\leq d(x,y) \Rightarrow f(y)\leq t + f(x)\Rightarrow f(y)< t + M(f).
$$

That is, we have that $$B_t\subset \left\lbrace x\in\mathcal{X}: f(x)< t + M(f)\right\rbrace.$$ Taking the complement, we conclude that:

$$
P\left(f(X)\geq M(f) + t \right)\leq P(\mathcal{X}\backslash B_t) = P\left(d(X,B)\geq t\right).
$$

Therefore, we reduce the problem of estimating $$(\star)$$ to estimating the quantity $$P(d(X,B)\geq t)$$ where $$B$$ is an event with probability at least $$1/2$$ by the definition of  $$M(F)$$. Indeed, we can upper bound the above expression as

$$
P\left(f(X)\geq M(f) + t \right)\leq P(\mathcal{X}\backslash B_t) \leq \alpha(t)
$$

where 

$$
\alpha(t):= \sup_{A\subset \mathcal{X}, P(A)\geq 1/2} P(d(X,A)\geq t).
$$

At first glance, the function $$\alpha(t)$$ seems harder to bound than the probability $$(\star)$$. However, note that studying $$\alpha(t)$$ is equivalent to study the quantity

$$
1 - \inf_{A\subset \mathcal{X}, P(A)\geq 1/2} P(d(X,A)< t).
$$

That is, we are interested in studying maximal big sets (probability larger than 1/2), with small surface area (small blowup probability). But this is exactly what isoperimetric results try to understand!  

### References

- [Concentration Inequalities](https://academic.oup.com/book/26549) - S. Boucheron, G. Lugosi, P. Massart 
- [Concentration of Measure for the Analysis of Randomized Algorithms](http://wwwusers.di.uniroma1.it/~ale/Papers/master.pdf) - D. Dubhashi, A. Panconesi
