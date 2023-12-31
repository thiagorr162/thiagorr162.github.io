---
layout: post
title: Métricas de desempenho em classificação
date: 2023-11-22
description: Vamos aprender o que é acurácia, precisão, recall e f1-score
tags: machine-learning, classification, performance-metrics
categories: machine-learning
---

Considere uma amostra i.i.d. de pares $$\{(X_1,Y_1),\dots,(X_n,Y_n)\}$$, em que  $$X_i\in\mathbb{R}^p$$ é um vetor que contém informações sobre um indivíduo $$i$$ e $$Y_i\in\{0,1\}$$ é a saída com respeito ao vetor $$X_i$$. Nosso objetivo é encontrar um classificador $$g:\mathbb{R}^p\to \{0,1\}$$ de modo que, para um novo par $$(X,Y)$$,  temos que $$g(X)$$  está "próximo" em algum sentido de $$Y$$.


Para exemplificar o cenário anterior, $$X_i$$ poderia representar uma série de fatores socioeconômicos de um estudante, $$Y_i$$ representar se esse estudante passou $$(Y_i=1)$$ ou não passou $$(Y_i=0)$$ no ENEM e $$g_0(X_i)=1$$ se a renda familiar desse estudante for maior que 5 salários mínimos e $$g_0(X_i)=0$$ caso contrário.

Note que no exemplo anterior, a escolha do classificador $$g_0$$ foi, de certa forma, arbitrária. Ao invés de utilizarmos 5 salários mínimos para classificar os alunos, poderíamos ter usado 4 ou 6. Além disso, ao invés de  $$g_0$$, poderíamos ter treinado algum modelo de Machine Learning, como uma rede neural, um boosting, etc. 

No final, o que queremos entender é: 

> **Dentre as várias possibilidades de classificadores, como podemos escolher o melhor?**

# Função de risco e classificador de Bayes

Para respondermos a questão anterior, precisamos criar algum critério para podermos comparar os vários possíveis classificadores. Esse critério é dado pela função de risco que atribuímos ao problema. No nosso caso, o que gostaríamos é de ter **um classificador que comete a menor quantidade de erros na média**, isto é, dado um classificador $$g$$, queremos que o risco $$R(g)$$:

$$
R(g) = \mathbb{E}[\mathbb{1}[Y\neq g(X)]] = P(Y\neq g(X)),
$$

seja o menor possível. 

Intuitivamente, conseguimos imaginar qual seria o melhor classificador possível $$g_*(X)$$. Suponha por um instante que você tem acesso à distribuição real dos dados $$p(x,y)$$, e portanto, tem acesso à $$p(y\mid x)$$. Se alguém te desse um valor $$X_0$$ e perguntasse qual o melhor chute possível para a respectiva saída $$Y_0$$ você poderia raciocinar da seguinte forma: 

> Dado que  $$X_0=x$$, vou chutar que $$Y_0=1$$ se esse resultado for mais provável, isto é, $$P(Y=1\mid X)>1/2$$; ou chutar $$Y_0=0$$ caso esse resultado for mais provável, isto é,  $$P(Y=1\mid X)\leq 1/2$$.

Note que isso pode ser reescrito de forma mais geral como:

$$
g_*(x) = \arg\max_{d\in\{0,1\}} P(Y=d\mid x)
$$

Esse estimador $$g_*$$ é conhecido como estimador de Bayes e conseguimos provar que ele de fato é o melhor possível através do seguinte teorema:

> **Teorema:** O estimador $$g_*$$ que minimiza o risco $$R(g)$$ é dado por
> 
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

Note que a análise anterior já nos fornece uma métrica de avaliação para problemas de classificação, isto é, encontrar um classificador $$g$$ que **minimiza**

$$
\frac{1}{N}\sum_{i=1}^N\mathbb{1}[Y_y\neq g(X_i)].
$$

Na próxima seção, veremos outras alternativas de métricas de avaliação.

# Métricas de avaliação

Antes de apresentarmos novas métricas para avaliação de desempenho em problemas de classificação, é fundamental compreender o conceito de matrizes de confusão. 

## Matriz de confusão

Dado um classificador $$g$$ e uma amostra de dados $$\{(X_1,Y_1),\dots,(X_n,Y_n)\}$$  separada para avaliação de modelos (e.g. conjunto de teste ou validação), considere as previsões feitas pelo classificador $$g(X_1),\dots,g(X_n)\in \{0,1\}$$.

Essas previsões podem ser separadas em quatro classes disjuntas: 

- Verdadeiros positivos (TP): O valor real é 1 e nosso classificador acertou. Isto é, $$Y_i=1=g(X_i)$$; 
- Falsos positivos (FP): O valor real é 0 e nosso classificador errou. Isto é, $$Y_i=0\neq g(X_i)=1$$;
- Verdadeiros negativos (TN) : O valor real é 0 e nosso classificador acertou. Isto é, $$Y_i=0=g(X_i)$$;
- Falsos negativos (FN): O valor real é 1 e nosso classificador errou. Isto é, $$Y_i=1\neq g(X_i)=0$$.

Podemos organizar essas classes de previsões em formato de matriz, resultando no que chamamos de **matriz de confusão**.

{% include figure.html path="assets/img/posts/class_metrics/matrix_confusao.png" class="img-fluid rounded z-depth-1" %}    

Como veremos a seguir, sempre vamos conseguir representar as métricas de classificação usando as classes acima.

## Acurácia

A primeira métrica que veremos já foi discutida na seção **Função de risco e classificador de Bayes**. Dado um classificador $$g$$, denotamos por **Acurácia** a seguinte métrica:

$$
\textrm{Acurácia}(g)=1 - \frac{1}{N}\sum_{i=1}^N\mathbb{1}[Y_y\neq g(X_i)]=\frac{1}{N}\sum_{i=1}^N\mathbb{1}[Y_y= g(X_i)].
$$

Essencialmente, a Acurácia mede a proporção de observações para as quais o modelo $$g$$ prevê corretamente a classe em relação às observações totais. 

Há uma pequena diferença entre essa expressão e a função de risco que  definimos no início do texto, pois agora subtraímos expressão de 1.  Fizemos isso apenas para manter consistência com a definição de acurácia na literatura. Observe que, para qualquer função de risco $$R$$ que desejamos **minimizar**, podemos usar $$1−R$$, transformando-a em uma métrica de avaliação que agora buscamos **maximizar**. Em outras palavras, as expressões são equivalentes, e a única mudança é que, em um caso, enfrentamos um problema de maximização, enquanto, no  outro, é de minimização."

Além disso, note que conseguimos escrever a expressão da acurácia em termos das classes da matriz de confusão, e dessa forma temos o seguinte:

$$
\textrm{Acurácia} = \frac{\textrm{TP}+\textrm{TN}}{\textrm{TP}+\textrm{TN}+\textrm{FP}+\textrm{FN}}.
$$

**Resumindo:** Quantas previsões corretas tivemos no total?

## Precisão

Precisão é uma métrica que mede a proporção de instâncias  verdadeiramente positivas (TP) entre as instâncias previstas como  positivas pelo modelo. Em outras palavras, a precisão mede a precisão  das previsões positivas feitas pelo modelo. Uma pontuação de alta  precisão indica que o modelo é capaz de identificar com precisão as  instâncias positivas, enquanto uma pontuação de baixa precisão indica  que o modelo está fazendo muitas previsões falsas positivas (FP).

$$
\textrm{Precisão} = \frac{\textrm{TP}}{\textrm{TP}+\textrm{FP}}.
$$

Note que um TP é um valor positivo que foi corretamente classificado como positivo. Já um FP era um valor negativo que foi erroneamente classificado como positivo. **Então o quociente está contando quantos valores foram classificados como positivos.**

**Resumindo:** De todas as previsões positivas, quantas acertamos?

## Recall

Recall é uma métrica de desempenho que mede a proporção de instâncias positivas corretamente identificadas por um modelo de classificação binária **em relação a todas as instâncias positivas reais**.  Em outras palavras, o recall mensura a capacidade do modelo de identificar corretamente instâncias positivas. Uma pontuação de recall alta indica que o modelo é capaz de identificar uma grande proporção de instâncias positivas, enquanto uma pontuação baixa de recall indica que o modelo está deixando de identificar muitas instâncias positivas.

$$
\textrm{Recall} = \frac{\textrm{TP}}{\textrm{TP}+\textrm{FN}}.
$$

Note que um TP é um valor positivo que foi corretamente classificado como positivo. Já um FN era um valor positivo que foi erroneamente classificado como negativo. **Então o quociente está contando quantos valores são de fato positivos.**

**Resumindo:** De todos os valores realmente positivos, quantos acertamos?

## F1-score

E se tanto a Precisão quanto o Recall são importantes  e você precisa que o classificador se saia bem em ambos os aspectos? A resposta é usar a média harmônica entre as duas medidas, que chamamos de F1-score:

$$
\textrm{F1-score} = \frac{2\cdot \textrm{Recall} \cdot \textrm{Precisão}}{\textrm{Recall}+\textrm{Precisão}}
$$

Essa métrica é altamente eficaz para equilibrar os efeitos de recall e precisão, uma vez que, se os valores de Recall ou Precisão forem muito baixos, o valor de F1 também será reduzido, dado que as métricas são multiplicadas.

**Resumindo:** Tenta balancear Recall e Precisão sem dar prioridade para nenhum deles.

# Qual métrica usar?

Agora podemos nos perguntar, dentre todas essas métricas, qual devemos usar? Existe alguma métrica que é melhor para avaliar modelos? A resposta dessas perguntas depende muito do problema que estamos estudando.

Por exemplo, suponha que estamos tentando prever se um indivíduo tem $$(Y=1)$$ ou não $$(Y=0)$$ uma doença muito rara que acontece apenas em 1% da população. Note que o estimador que sempre diz que a pessoa **não tem a doença**, teria uma **acurácia** de 99%! Mas isso, principalmente no âmbito médico, seria desastroso, já que não queremos correr o risco de deixar de diagnosticar doença, que pode muitas vezes ser fatal. Logo, acurácia não seria nada apropriada. Isso se deve ao fato do conjunto de dados ser muito desbalanceado, isto é, existe muito mais casos negativos que casos positivos. 

Agora, imagine um cenário no qual um falso negativo acarreta custos significativos. Para ilustrar, consideremos o caso em que desejamos evitar o risco de diagnosticar erroneamente alguém como portador de câncer quando, na verdade, está saudável. Essa situação poderia resultar em considerável estresse emocional para a pessoa afetada. Nesse caso, é mais apropriado usarmos a **Precisão** com métrica, já que queremos estar bem certos do nosso diagnóstico.

Outro cenário bastante plausível é o da prevenção de fraudes financeiras. Nesse contexto, o custo associado à não identificação de uma fraude é significativo. Portanto, nesse caso, seria apropriado empregar o **Recall** como métrica de avaliação. Isso se justifica pelo fato de que a classificação errônea de uma transação como fraudulenta pode ser facilmente verificada, e podemos tolerar alguns falsos positivos em vez de correr o risco de ter falsos negativos.

Entretanto, há uma pegadinha nos exemplos dados acima. Um estimador que queira evitar qualquer estresse de um falso negativo, poderia, por exemplo, sempre dizer que ninguém tem câncer. Já um estimador que quisesse capturar toda fraude financeira, poderia simplesmente classificar todas as transações como fraudulentas. Dessa forma, é sempre bom fazermos uma análise geral dos casos possíveis usando a matriz de confusão e potencialmente fazer uso de métricas que combinam outras métricas, como é o caso do **F1-Score**.

# Referências

1. Aprendizado de máquina: uma abordagem estatística. (2020). (n.p.): Rafael Izbicki.
2. Mohri, M., Rostamizadeh, A., Talwalkar, A. (2018). Foundations of Machine Learning. United Kingdom: MIT Press.
3. Hastie, T., Tibshirani, R., Friedman, J. (2013). The Elements of Statistical Learning: Data Mining, Inference, and Prediction. Germany: Springer New York.
4. [https://web.eecs.umich.edu/~cscott/past_courses/eecs598w14/notes/02_bayes_classifier.pdf](https://web.eecs.umich.edu/~cscott/past_courses/eecs598w14/notes/02_bayes_classifier.pdf)
5. [https://medium.com/@impythonprogrammer/evaluation-metrics-for-classification-fc770511052d](https://medium.com/@impythonprogrammer/evaluation-metrics-for-classification-fc770511052d)
6. [https://txt.cohere.com/classification-eval-metrics/](https://txt.cohere.com/classification-eval-metrics/)
7. [https://www.kdnuggets.com/understanding-classification-metrics-your-guide-to-assessing-model-accuracy](https://www.kdnuggets.com/understanding-classification-metrics-your-guide-to-assessing-model-accuracy)

```
Next:
falar de AUC e ROC
```