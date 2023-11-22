---
layout: post
<<<<<<< HEAD
title: Suficiência estatística w 
date: 2023-11-10
description: an example of a blog post with some code
=======
title: Suficiência estatística
date: 2023-11-21
<<<<<<< HEAD
description: 
<<<<<<< HEAD
>>>>>>> Initial suf_esta text
tags: statistics
=======
tags: statistics, inference
>>>>>>> Add preliminary text
=======
description: Vamos aprender o que é uma estatística suficiente
tags: statistics, inference, sufficiency 
>>>>>>> Test adding bib references
categories: statistics
---

Nosso objetivo ao realizar inferência estatística é aprender um parâmetro desconhecido $$\theta$$ a partir de uma amostra $$X$$ desses dados, supondo que esses dados vieram de uma distribuição $$P_\theta.$$

Para a maioria das aplicações, $$X$$ será um vetor aleatório. O parâmetro $$\theta$$ pode ser uma constante única ou assumir valores em algum **subconjunto** de $$\mathbb{R}^p$$. O parâmetro $$\theta$$ e os dados $$X$$ estão relacionados por meio de um modelo no qual a distribuição de $$X$$ é determinada por $$\theta$$. A distribuição quando o parâmetro é $$\theta$$ é denotada por $$P_\theta$$, e escrevemos $$X \sim P_\theta$$. Em geral, um modelo é escrito como o conjunto de distribuições  $$\mathcal{P} = \{P_\theta : \theta \in \Omega\}$$, onde o espaço de parâmetros $$\Omega$$ é o conjunto de todos os valores possíveis para $$\theta$$.

Nossa estratégia para obter informações sobre o parâmetro $$\theta$$, por enquanto, envolve a exploração de funções $$\delta$$ aplicadas aos dados $$X$$, que serão referidas como **estatísticas** ou **estimadores**. Essas funções são concebidas de modo a proporcionar uma representação significativa do parâmetro não observável $$\theta$$. A busca por uma função $$\delta(X)$$ próxima de $$\theta$$ é o que chamamos de **estimação**.

## Exemplo: Lançamento de moeda

Como exemplo, suponha que estamos modelando o lançamento de $$n$$ moedas indenpendentes, tal que a probabilidade da face observada após o lançamento ser "cara" é $$\theta$$ e da face "coroa" ser observada é de $$1-\theta$$, com $$\theta\in[0,1]$$.  Nesse caso, podemos modelar a variável aleatória $$\mathbf{X} = (X_1,\dots,X_n)$$ que nos diz se a $i$-ésima moeda  caiu "cara" ou "coroa", através de uma distribuição Bernoulli, isto é:

$$
\mathbf{X} = (X_1,\dots,X_n) \sim \textrm{Bernoulli}(\theta)^{\otimes n},\ \theta\in[0,1].
$$

Nesse caso então, teríamos que:

- $$X_i$$ nos diz se a moeda caiu "cara" ($$X=1$$) ou "coroa" ($$X=0$$);

- $$\Omega = [0,1]$$ já que $$\theta$$ representa uma probabilidade e portanto seus valores devem estar entre 0 e 1;

- Juntando tudo, temos que, para cada $$i=1,\dots,n:$$
  
  $$
  \mathbf{X}\sim P_\theta,\ \textrm{com}\  P_\theta\in\mathcal{P} = \{\textrm{Bernoulli}(\theta)^{\otimes n} : \theta \in [0,1]\}.
  $$

Nesse exemplo, uma **estatística** $$\delta$$ dos dados $$\mathbf{X} = (X_1,\dots,X_n)$$ que parece natural para nos dar informação sobre o parâmetro $$\theta$$ que queremos estimar seria, por exemplo:

$$
\delta(\mathbf{X}) = \frac{X_1 + \dots + X_n}{n},
$$

isto é, a proporção (%) de "caras" observadas após os $$n$$ lançamentos. 

# Suficiência estatística

Suponha agora que dois estatísticos, **A** e **B**, estão trabalhando para estimar o parâmetro $$\theta$$ do exemplo anterior de lançamentos de moedas. Cada um dos estatísticos se encontra no seguinte cenário:

1. O estatístico **A**, tem a informação completa sobre a variável $$\mathbf{X}$$, isto é, ele sabe os valores de todas as varáveis $$X_1,\dots,X_n$$. 
2. Já o estatístico **B**, tem apenas a informação da soma $$T$$ dos valores $$X_1,\dots,X_n$$, isto é, 

$$
T(X) = X_1+\dots+X_n
$$

Note que estatístico **B**, a princípio, tem menos informação que o **A**. Por exemplo, suponha que $$\mathbf{X} = (0,1,1,1,0,1,0,0,0,1)$$, então **A** saberia exatamente o que aconteceu em cada lançamento de moeda, enquanto **B** teria apenas a informação de que  foram observadas 5 "caras" em $$n=10$$ lançamentos. Mas isso realmente é verdade? Ou seja, **o estatístico *A* tem mais informação que *B*?**

Para respondermos isso, vamos calcular a densidade conjunta de $$\mathbf{X}$$. Isto é, para $$x =(x_1,\dots,x_n)\in[0,1]^n$$:

$$
\begin{align*}
p_{\theta}(x)=p_{\theta}(x_1,\dots,x_n) &= \prod_{i=1}^n\theta^{x_i} (1-\theta)^{1-x_i}\\
& = \theta^{\sum_{i=1}^n x_i} (1-\theta)^{\sum_{i=1}^n (1-x_i)}\\
& = \theta^{\sum_{i=1}^n x_i} (1-\theta)^{n-\sum_{i=1}^n x_i}\\
& = \theta^{T(x)} (1-\theta)^{n-T(x)}.
\end{align*}
$$


# Referências
