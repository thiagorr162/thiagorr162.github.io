---
layout: post
title: Suficiência estatística
date: 2023-11-21
description: Vamos aprender o que é uma estatística suficiente
tags: statistics, inference, sufficiency 
categories: statistics
bibliography: references.bib
link-citations: true
---

Nosso objetivo ao realizar inferência estatística é aprender um parâmetro desconhecido $$\theta$$ a partir de uma amostra $$X$$ desses dados, supondo que esses dados vieram de uma distribuição $$P_\theta.$$

Para a maioria das aplicações, $$X$$ será um vetor aleatório. O parâmetro $$\theta$$ pode ser uma constante única ou assumir valores em algum **subconjunto** de $$\mathbb{R}^p$$. O parâmetro $$\theta$$ e os dados $$X$$ estão relacionados por meio de um modelo no qual a distribuição de $$X$$ é determinada por $$\theta$$. A distribuição quando o parâmetro é $$\theta$$ é denotada por $$P_\theta$$, e escrevemos $$X \sim P_\theta$$. Em geral, um modelo é escrito como o conjunto de distribuições  $$\mathcal{P} = \{P_\theta : \theta \in \Omega\}$$, onde o espaço de parâmetros $$\Omega$$ é o conjunto de todos os valores possíveis para $$\theta$$.

Nossa estratégia para obter informações sobre o parâmetro $$\theta$$, por enquanto, envolve a exploração de funções $$\delta$$ aplicadas aos dados $$X$$, que serão referidas como **estatísticas** ou **estimadores**. Essas funções são concebidas de modo a proporcionar uma representação significativa do parâmetro não observável $$\theta$$. A busca por uma função $$\delta(X)$$ próxima de $$\theta$$ é o que chamamos de **estimação**.

## Exemplo: Lançamento de moeda

Como exemplo, suponha que estamos modelando o lançamento de $$n$$ moedas indenpendentes, tal que a probabilidade da face observada após o lançamento ser "cara" é $$\theta$$ e da face "coroa" ser observada é de $$1-\theta$$, com $$\theta\in[0,1]$$.  Nesse caso, podemos modelar a variável aleatória $$X_i$$ que nos diz se a $i$-ésima moeda  caiu "cara" ou "coroa", através de uma distribuição Bernoulli, isto é:

$$
X_i\sim \textrm{Bernoulli}(\theta),\ \theta\in[0,1].
$$

Nesse caso então, teríamos que:

- $$X_i$$ nos diz se a moeda caiu "cara" ($$X=1$$) ou "coroa" ($$X=0$$);

- $$\Omega = [0,1]$$ já que $$\theta$$ representa uma probabilidade e portanto seus valores devem estar entre 0 e 1;

- Juntando tudo, temos que:
  
  $$
  X\sim P_\theta,\ \textrm{com}\  P_\theta\in\mathcal{P} = \{\textrm{Bernoulli}(\theta) : \theta \in [0,1]\}.
  $$

Nesse exemplo, uma **estatística** $$\delta$$ dos dados $$X$$ que parece natural para nos dar informação sobre o parâmetro $$\theta$$ que queremos estimar seria, por exemplo:

$$
\delta(X) = \frac{X}{100},
$$

isto é, a proporção (%) de "caras" observadas após os 100 lançamentos. 

# Suficiência estatística

<d-cite key="keener"></d-cite>
