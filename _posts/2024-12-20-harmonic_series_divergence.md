---
layout: post
title: "A Clever Trick to Prove the Divergence of the Harmonic Series"
date: 2024-12-21
permalink: /posts/2024/12/harmonic_series_divergence/
tags:
  - inequality
  - harmonic series
---

The inequality $$e^x \geq 1+x$$ offers a neat way to show that the harmonic series diverges. Applying it for $$x = \frac{1}{n}$$ we get:

$$
e^{1/n} \geq 1 + 1/n = \frac{n+1}{n}.
$$

Repeating this idea $$n$$ times gives:

$$
e^{1 + 1/2 + 1/3 + \dots + 1/n} \geq \frac{2}{1} \cdot \frac{3}{2} \cdot \dots \cdot \frac{n+1}{n} = n+1.
$$

Taking $$log$$ both sides shows that the harmonic sum $$H_n := 1 + 1/2 + \dots + 1/n$$ satisfies:

$$
H_n \geq \log(n+1),
$$

proving that the harmonic series diverges.

---

_Inspired by Ragib Zaman's comment on [Math Stack Exchange](https://math.stackexchange.com/questions/691807/proofs-of-am-gm-inequality), June 12, 2014._
