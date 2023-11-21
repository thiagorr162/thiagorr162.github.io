---
layout: post
<<<<<<< HEAD
title: Suficiência estatística w 
date: 2023-11-10
description: an example of a blog post with some code
=======
title: Suficiência estatística
date: 2023-11-21
description: 
<<<<<<< HEAD
>>>>>>> Initial suf_esta text
tags: statistics
=======
tags: statistics, inference
>>>>>>> Add preliminary text
categories: statistics
---

# Estatística suficiente

## Introdução do problema

Nosso objetivo ao realizar inferência estatística é aprender um parâmetro desconhecido $\theta$ a partir dos dados $X$, supondo que esses dados vieram de uma distribuição $P_\theta.$

Para a maioria das aplicações, $X$ será um vetor aleatório. O parâmetro $\theta$ pode ser uma constante única ou assumir valores em algum **subconjunto** de $\mathbb{R}^p$. O parâmetro $\theta$ e os dados $X$ estão relacionados por meio de um modelo no qual a distribuição de $X$ é determinada por $\theta$. A distribuição quando o parâmetro é $\theta$ é denotada por $P_\theta$, e escrevemos $X \sim P_\theta$. Em geral, um modelo é escrito como o conjunto de distribuições  $\mathcal{P} = \{P_\theta : \theta \in \Omega\}$, onde o espaço de parâmetros $\Omega$ é o conjunto de todos os valores possíveis para $\theta$.

Nosso objetivo principal é identificar funções $\delta$ dos dados $X$, que denominaremos **estatísticas** ou **estimadores**, capazes de nos fornecer informações sobre quantidades não observáveis.

### Exemplo: Lançamento de moedas

Como exemplo, suponha que estamos modelando o lançamento de uma moeda, tal que a probabilidade da face observada após o lançamento ser "cara" é $\theta$ e da face "coroa" ser observada é de $1-\theta$, com $\theta\in[0,1]$.  Suponha que lançamos essa mesma moeda 100 vezes de forma independente.  Nesse caso, podemos modelar a variável aleatória $X$ que conta a quantidade de faces "cara" que vamos observar após os 100 lançamentos, através de uma distribuição Binomial, isto é:

$$
X\sim \textrm{Bin}(100,\theta),\ \theta\in[0,1].
$$

Nesse caso então, teríamos que:

- $X$ é a variável aleatória que conta a quantidade de "caras" após 100 lançamentos;

- $\Omega = [0,1]$ já que $\theta$ representa uma probabilidade e portanto seus valores devem estar entre $0$ e $1$;

- Portanto:
  $$
  X\sim P_\theta,\ \textrm{com}\  P_\theta\in\mathcal{P} = \{\textrm{Bin}(100, \theta) : \theta \in [0,1]\}.
  $$

Nesse exemplo, uma **estatística** $\delta$ dos dados $X$ que parece natural para nos dar informação sobre o parâmetro $\theta$ que queremos estimar seria, por exemplo:
$$
\delta(X) = \frac{X}{100},
$$
isto é, a proporção de "caras" observadas após os 100 lançamentos. 
