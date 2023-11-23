---
layout: post
title: Medidas de desempenho para classificação
date: 2023-11-22
description: Vamos aprender algumas medidas de desempenho para problemas de classificação
tags: machine-learning, classification, performance-metrics
categories: machine-learning
---

Considere uma amostra i.i.d. de pares $$\{(X_1,Y_1),\dots,(X_n,Y_n)\}$$, em que  $$X_i\in\mathbb{R}^p$$ é um vetor que contém informações sobre um indivíduo$$i$$ e $$Y_i\in\{0,1\}$$ é a saída com respeito ao vetor $$X_i$$. Nosso objetivo é encontrar um classificador $$g:\mathbb{R}^p\to \{0,1\}$$ de modo que, para um novo par $$(X,Y)$$,  temos que $$g(X)$$  está "próximo" em algum sentido de $$Y$$.


Para exemplificar o cenário anterior, $$X_i$$ poderia representar uma série de fatores socioeconômicos de um estudante, $$Y_i$$ representar se esse estudante passou $$(Y_i=1)$$ ou não passou $$(Y_i=0)$$ no ENEM e $$g_0(X_i)=1$$ se a renda familiar desse estudante for maior que 5 salários mínimos e $$g_0(X_i)=0$$ caso contrário.

Note que no exemplo anterior, a escolha do classificador $$g_0$$ foi, de certa forma, arbitrária. Ao invés de utilizarmos 5 salários mínimos para classificar os alunos, poderíamos ter usado 4 ou 6. Além disso, ao invés de  $$g_0$$, poderíamos ter treinado algum modelo de Machine Learning, como uma rede neural, um boosting, etc. 

No final, o que queremos entender é: 

> **Dentre as várias possibilidades de classificadores, como podemos escolher o melhor?**

# Função de risco

Para respondermos a questão anterior, precisamos criar algum critério para podermos comparar os vários possíveis classificadores. Esse critério é dado pela função de risco que atribuímos ao problema. No nosso caso, o que gostaríamos é de ter **um classificador que comete a menor quantidade de erros na média**, isto é, dado um classificador $$g$$, queremos que o risco $$R(g)$$:

$$
R(g) = \mathbb{E}[\mathbb{1}[Y\neq g(X)]] = P(Y\neq g(X)),
$$

seja o menor possível. 

Intuitivamente, conseguimos imaginar qual seria o melhor classificador possível $$g_*(X)$$. Suponha por um instante que você tem acesso à distribuição real dos dados $$P$$. Se alguém te desse um valor $$X_0$$ e perguntasse qual o melhor chute possível para a respectiva saída $$Y_0$$ você poderia raciocinar da seguinte forma: 

> Dado que estou vendo esse valor para $$X_0$$, a probabilidade de $$Y_0$$ ser igual à 0 é maior que a probabilidade de ser igual à $$1$$? Se sim, meu melhor chute é dizer que $$Y_0$$ é 0. Caso contrário, meu melhor chute é dizer que é igual à 1.

Isto é.

$$
g_*(x) = \arg\max_{d\in\{0,1\}} P(Y=d\mid x)
$$

Esse estimador $$g_*$$ é conhecido como estimador de Bayes e conseguimos provar que ele de fato é o melhor possível através do seguinte teorema:

> **Teorema:** O estimador $$g_*$$ que minimiza o risco $$R(g)$$ é dado por
> $$
> g_*(x) = \arg\max_{d\in\{0,1\}} P(Y=d\mid x)
> $$

**Prova:** Defina $$\eta(x) = P(Y=1\mid X=x)$$, então para um classificador qualquer $$g$$, temos que


$$
\begin{align*}
R(g) &= \mathbb{E}[Y\neq g(X)]\\
&= \mathbb{E}_X[\mathbb{E}_{Y\mid X}[Y\neq g(X)]]\\
&= \mathbb{E}_X[\eta(X)\mathbb{1}[1\neq g(X)]+(1-\eta(X))\mathbb{1}[0\neq g(X)]]\\
&= \mathbb{E}_X[\underset{A}{\eta(X)\mathbb{1}[g(X)=0}]+\underset{B}{(1-\eta(X))\mathbb{1}[g(X)=1]}]\\
\end{align*}
$$


Para minimizarmos a expressão acima, basta minimizarmos a função dentro do valor esperado. Note que apenas um dos lados **A** ou **B** será não-nulo na expressão acima, já que ou $$g(x)=0$$ ou $$g(x)=1$$. Se $$\eta(x)>1/2$$, então como queremos minimizar $$R(g)$$, gostaríamos que o lado direito (B) fosse o não-nulo, já que nesse caso $$1-\eta(x)<\eta(x)$$ . Logo, se $$\eta(x)>1/2$$ o classificador que minimiza a expressão deve ser igual à 1. Caso contrário, ele deve ser 0. Mas isso é exatamente o classificador de Bayes que descrevemos anteriormente. $$\blacksquare$$

