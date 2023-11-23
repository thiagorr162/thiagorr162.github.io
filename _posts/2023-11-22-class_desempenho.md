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

Intuitivamente, conseguimos imaginar qual seria o melhor classificador possível $$g_*(X)$$. Suponha por um instante que você tem acesso à distribuição real dos dados $$p(x,y)$$, e portanto, tem acesso à $$p(y\mid x)$$. Se alguém te desse um valor $$X_0$$ e perguntasse qual o melhor chute possível para a respectiva saída $$Y_0$$ você poderia raciocinar da seguinte forma: 

> Dado que  $$X_0=x$$, vou chutar que $$Y_0=1$$ se esse resultado for mais provável, isto é, $$P(Y=1|X)>1/2$$; ou chuatar $$Y_0=0$$ caso esse resultado for mais provável, isto é,  $$P(Y=1|X)\leq 1/2$$.

Note que isso pode ser reescrito de forma mais geral como:

$$
g_*(x) = \arg\max_{d\in\{0,1\}} P(Y=d\mid x)
$$

Esse estimador $$g_*$$ é conhecido como estimador de Bayes e conseguimos provar que ele de fato é o melhor possível através do seguinte teorema:

> **Teorema:** O estimador $$g_*$$ que minimiza o risco $$R(g)$$ é dado por
> $$
> g_*(x) = \arg\max_{d\in\{0,1\}} P(Y=d\mid x).
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

A função $$\eta(x)= P(Y=1\mid X=x)$$ é comummente chamada de **função regressora**. Em geral, em aprendizado de máquinas, as funções que minimizam algum risco tem sempre essa cara. Por exemplo, quando estamos trabalhando com problema de regressão ao invés de classificação (i.e. $$Y\in\mathbb{R}$$ ao invés de $$Y\in\{0,1\}$$) e utilizamos o risco quadrático como critério de otimização (i.e. $$R(f) = \mathbb{E}[(f(X)-Y)^2]$$), a função $$f_*$$ que otimiza esse critério é dada por$$f_*(x) = \mathbb{E}[Y\mid X=x]$$, semelhante ao classificador de Bayes. Não vou entrar em muitos mais detalhes sobre isso por enquanto, já que esse vai ser o assunto de um futuro post.

Voltando ao problema de como escolher o melhor classificador, na prática dois problemas acontecem:

1. Não temos acesso à distribuição real dos dados $$P$$, e portanto não conseguimos construir o classificador de Bayes como acima;
2. Como não temos a distribuição real dos dados $$P$$, também não conseguimos minimizar o risco $$R(g)$$, já que ele depende do cálculo de um valor esperado sobre $$P$$.

Para resolver o problema (1), o que fazemos é treinar algum modelo $$g(x)$$ para aproximar o comportamento do classificador de Bayes, isto é,

$$
\tilde{g}(x) \approx \eta(x),
$$

e daí construímos um classificador final $$g$$, tal que $$g(x)=1$$ se $$\tilde{g}(x)>1/2$$ e $$g(x)=0$$ caso contrário.

Para resolvermos o problema (2), utilizamos o fato de que 

$$
P(Y\neq g(X)) \approx \frac{1}{N}\sum_{i=1}^N\mathbb{1}[Y_y\neq g(X_i)].
$$

Esse fato é intuitivo utilizando a lei dos grandes números, por exemplo. Entretanto, essas ferramentas estatísticas assimptóticas não funcionam muito bem na teoria "moderna" de aprendizado estatístico, já que o comum em problema reais é termos acesso à um número muito limitado de dados (i.e. $$N$$ não é tão grande), e portanto a hipótese assintótica desses resultados deixa de ser razoável.  O que é utilizado hoje em dia são resultados probabilísticos de **amostra finita**, que nos dão estimativas do erro $$\textrm{erro}_N$$:

$$
\textrm{erro}_N = \left| P(Y\neq g(X)) - \frac{1}{N}\sum_{i=1}^N\mathbb{1}[Y_y\neq g(X_i)]\mid \right|
$$

em função do tamanho da amostra $$N$$. A teoria básica que encapsula esses resultados é a de **concentração de medida**. Não entrarei em detalhes sobre isso agora, já que esse será um tema futuro no nosso blog.

# Métricas de avaliação alternativas

Com base na análise realizada na seção anterior, conseguimos estabelecer uma métrica de desempenho bastante intuitiva para classificadores.

## Acurácia

Dado um classificador $$g$$, denotamos por **Acurácia** a seguinte métrica:
$$
\textrm{Acurácia}(g)=1 - \frac{1}{N}\sum_{i=1}^N\mathbb{1}[Y_y\neq g(X_i)]=\frac{1}{N}\sum_{i=1}^N\mathbb{1}[Y_y= g(X_i)]
$$

Essencialmente, a Acurácia mede a proporção de observações para as quais o modelo $$g$$ prevê corretamente a classe em relação às observações totais.





# Referências

1. Aprendizado de máquina: uma abordagem estatística. (2020). (n.p.): Rafael Izbicki.
2. Mohri, M., Rostamizadeh, A., Talwalkar, A. (2018). Foundations of Machine Learning. United Kingdom: MIT Press.
3. Hastie, T., Tibshirani, R., Friedman, J. (2013). The Elements of Statistical Learning: Data Mining, Inference, and Prediction. Germany: Springer New York.
4. https://web.eecs.umich.edu/~cscott/past_courses/eecs598w14/notes/02_bayes_classifier.pdf
