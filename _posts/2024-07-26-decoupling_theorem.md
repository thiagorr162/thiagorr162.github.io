---
layout: post
title: 'The coolest proof you are going to learn today'
date: 2024-07-26
permalink: /posts/2024/07/decoupling_inequality/
tags:
  - inequality
  - concentration
  - probability
  - decoupling
---

We are interested in studying quadratic forms of the type:

$$
\langle X,AX \rangle = X^TAX,
$$

where $$X \in \mathbb{R}^d$$ is a random vector with i.i.d. coordinates and $$A$$ is a $$d \times d$$ matrix. Such quadratic forms are called chaos in probability. For simplicity, we will assume that $$X_i$$ have zero mean and unit variance.

Our main goal is to establish the following result: Given a convex function $$F: \mathbb{R} \to \mathbb{R}$$,

$$
F(X^TA_*X) \leq F(4X^T A X'),
$$

where $$X'$$ is an independent copy of $$X$$ and $$A_*$$ is the matrix $$A$$ with 0's on  its diagonal.

The advantage of the RHS is that it is linear in $$X$$ rather than quadratic. This implies, for example, that one can write

$$
\sum_{i=1}^d \left(\sum_{j=1}^d a_{ij}X_j'\right)X_i = \sum_{i=1}^d c_iX_i,
$$

which allows us to use results for sums of linear i.i.d. variables. 

Our goal is to make the $$X$$ on the right side of $$X^TAX$$ independent of the $$X$$ on the left side. Note that if we fix a subset $$I \subset [d]$$, then the sum

$$
\sum_{i \in I, j \in I^c} a_{ij} X_i X_j
$$

satisfies the idea of the left part ($$X_i$$) being independent of the right part ($$X_j$$).

The first cool trick in this proof is to notice that for a fixed vector $$x \in \mathbb{R}$$:

$$
\begin{align*}
x^TA_*x &= \sum_{i \neq j} a_{ij} x_i x_j \\
        &= 4\mathbb{E}_\delta\left[ \sum_{i \neq j} \delta_i(1-\delta_j)a_{ij}x_ix_j\right] \\ 
        &= 4\mathbb{E}_I\left[\sum_{i \in I, j \in I^c} a_{ij} x_i x_j\right],
\end{align*}
$$

where $$\delta_i = 1$$ with probability $$1/2$$ and the same for $$\delta_i=0$$. The $$4$$ in this expression appears because this is the expectation of $$\delta(1-\delta)$$.

Applying the expectation over $$X$$ on both sides, we get

$$
\mathbb{E}_X\left[F(X^TA_*X)\right] \leq \mathbb{E}_X\left[F\left(\mathbb{E}_I\left[4\sum_{i \in I, j \in I^c} a_{ij} X_i X_j\right]\right)\right].
$$

By Jensen and Fubini's theorems:

$$
\mathbb{E}_X\left[F(X^TA_*X)\right] \leq \mathbb{E}_I\mathbb{E}_X\left[F\left(4\sum_{i \in I, j \in I^c} a_{ij} X_i X_j\right)\right].
$$

Now, be prepared for the second trick! Note that if $$\mathbb{E}(Z) \geq a$$ for some random variable $$Z$$ and $$a \in \mathbb{R}$$, then there must exist a realization $$Z(\omega) \geq a$$ (think about this!). Hence, there exists a realization $$I$$, such that

$$
\mathbb{E}_X\left[F(X^TA_*X)\right] \leq \mathbb{E}_X\left[F\left(4\sum_{i \in I, j \in I^c} a_{ij} X_i X_j'\right)\right].
$$

From now on, we will work with this fixed $$I$$. Note that we have already changed the right term $$X_j$$ to its independent copy $$X_j'$$. We can do this because the terms $$i$$ and $$j$$ are in complementary sets, making $$X_i$$ and $$X_j$$ independent.

Now, we need to show that 

$$
 \mathbb{E}_X\left[F\left(4\sum_{i \in I, j \in I^c} a_{ij} X_i X_j'\right)\right] \leq \mathbb{E}_X\left[F\left(4\sum_{i,j=1}^n a_{ij} X_i X_j'\right)\right] .
$$

To do this, write  the sum in right expression as $$Y+Z_1+Z_2$$, where $$Y$$ is the sum over $$I \times I^c$$ (the sum in left expression), $$Z_1$$ is the sum over $$I \times I$$, and $$Z_2$$ is the sum over $$I^c \times [n]$$ (make a drawing!).

Now, condition on all variables appearing in the $$Y$$ term, that is, $$i\in I$$ and $$j\in I^c$$. This makes $$Y$$ fixed, $$Z_1$$ with randomness only over $$j \in I$$, and $$Z_2$$ only with randomness over $$i \in I^c$$ and $$j \in I$$. This makes $$Z_1$$ and $$Z_2$$ zero mean random variables, so

$$
F(4Y + 0 + 0) = F(4Y + \mathbb{E}_{Z_1,Z_2}(4Z_1 + 4Z_2)).
$$

Using Jensen again, we have

$$
F(4Y) = \mathbb{E}_{Z_1,Z_2}F(4Y + 4Z_1 + 4Z_2).
$$

Finally, taking the expectation over all random variables, we get

$$
\mathbb{E}(F(4Y)) \leq (\star),
$$

concluding the proof!

### References
- [High-Dimensional Probability](https://www.math.uci.edu/~rvershyn/papers/HDP-book/HDP-book.html) - R. Vershynin
