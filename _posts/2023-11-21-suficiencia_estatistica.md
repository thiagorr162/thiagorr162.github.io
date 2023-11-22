---
layout: post
title: Suficiência estatística
date: 2023-11-21
description: Vamos aprender o que é uma estatística suficiente
tags: statistics, inference, sufficiency 
categories: statistics
---

Nosso objetivo ao realizar inferência estatística é aprender um parâmetro desconhecido $$\theta$$ a partir de uma amostra $$X$$ desses dados, supondo que esses dados vieram de uma distribuição $$P_\theta.$$

Para a maioria das aplicações, $$X$$ será um vetor aleatório. O parâmetro $$\theta$$ pode ser uma constante única ou assumir valores em algum **subconjunto** de $$\mathbb{R}^p$$. O parâmetro $$\theta$$ e os dados $$X$$ estão relacionados por meio de um modelo no qual a distribuição de $$X$$ é determinada por $$\theta$$. A distribuição quando o parâmetro é $$\theta$$ é denotada por $$P_\theta$$, e escrevemos $$X \sim P_\theta$$. Em geral, um modelo é escrito como o conjunto de distribuições  $$\mathcal{P} = \{P_\theta : \theta \in \Omega\}$$, onde o espaço de parâmetros $$\Omega$$ é o conjunto de todos os valores possíveis para $$\theta$$.

Nossa estratégia para obter informações sobre o parâmetro $$\theta$$, por enquanto, envolve a exploração de funções $$\delta$$ aplicadas aos dados $$X$$, que serão referidas como **estatísticas**. Quando essas funções são concebidas de modo a proporcionar uma representação significativa do parâmetro não observável $$\theta$$,  vamos chama-las de  de **estimadores** e esse processo de busca por uma função $$\delta(X)$$ próxima de $$\theta$$ é o que chamamos de **estimação**.

## Exemplo 1: Lançamento de moeda

Como exemplo, suponha que estamos modelando o lançamento de $$n$$ moedas indenpendentes, tal que a probabilidade da face observada após o lançamento ser "cara" é $$\theta$$ e da face "coroa" ser observada é de $$1-\theta$$, com $$\theta\in[0,1]$$.  Nesse caso, podemos modelar a variável aleatória $$X = (X_1,\dots,X_n)$$ que nos diz se a $$i$$-ésima moeda  caiu "cara" ou "coroa", através de uma distribuição Bernoulli, isto é:

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

Nesse exemplo, uma **estatística** $$\delta$$ dos dados $$X = (X_1,\dots,X_n)$$ que parece natural para nos dar informação sobre o parâmetro $$\theta$$ que queremos estimar seria, por exemplo:

$$
\delta(X) = \frac{X_1 + \dots + X_n}{n},
$$

isto é, a proporção (%) de "caras" observadas após os $$n$$ lançamentos. 

# Suficiência estatística

Suponha agora que dois estatísticos, **A** e **B**, estão trabalhando para estimar o parâmetro $$\theta$$ do exemplo anterior de lançamentos de moedas. Cada um dos estatísticos se encontra no seguinte cenário:

1. O estatístico **A**, tem a informação completa sobre a variável $$X$$, isto é, ele sabe os valores de todas as varáveis $$X_1,\dots,X_n$$. 
2. Já o estatístico **B**, tem apenas a informação da soma $$T$$ dos valores $$X_1,\dots,X_n$$, isto é, 

$$
T(X) = X_1+\dots+X_n
$$

Note que estatístico **B**, a princípio, tem menos informação que o **A**. Por exemplo, suponha que $$X = (0,1,1,1,0,1,0,0,0,1)$$, então **A** saberia exatamente o que aconteceu em cada lançamento de moeda, enquanto **B** teria apenas a informação de que  foram observadas 5 "caras" em $$n=10$$ lançamentos. Mas isso realmente é verdade? Ou seja, **no problema de estimação de $$\theta$$, o estatístico *A* tem mais informação que *B*?**

Para respondermos isso, vamos calcular a distribuição conjunta de $$X$$. Isto é, para $$x =(x_1,\dots,x_n)\in[0,1]^n$$:

$$
\begin{align*}
p_{\theta}(x)=p_{\theta}(x_1,\dots,x_n) &= \prod_{i=1}^n\theta^{x_i} (1-\theta)^{1-x_i}\\
& = \theta^{\sum_{i=1}^n x_i} (1-\theta)^{\sum_{i=1}^n (1-x_i)}\\
& = \theta^{\sum_{i=1}^n x_i} (1-\theta)^{n-\sum_{i=1}^n x_i}\\
& = \theta^{T(x)} (1-\theta)^{n-T(x)}.
\end{align*}
$$

No fim das contas, o valor individual de cada $$x_i$$ não importa. A única informação realmente relevante para calcularmos a probabilidade conjunta dos dados é a soma $$T(x)$$ das coordenadas! Portanto, **o estatístico B teria a mesma informação que o estatístico A em sua tarefa de estimar $$\theta$$**.

Perceba que, existem $${n\choose t}$$ sequências de lançamentos de moedas cuja a quantidade de ocorrência de "caras" é igual à $$t$$, e para todas elas são atribuídas as mesmas probabilidades $$\theta^t(1-\theta)^{n-t}$$, o que nos faz suspeitar que condicionado ao evento $$T(X)=t$$, a probabilidade conjunta de $$X$$ deveria ser uniforme e independente do parâmetro $$\theta$$. De fato, podemos verificar isso na prática:

$$
\begin{align*}
P_{\theta}(X=x\mid T=t) &= \frac{\theta^t (1-\theta)^{n-t}}{\theta^{t} (1-\theta)^{n-t}}\mathbb{1}\{T(x)=t\}{n \choose t}^{-1}\\
&= \mathbb{1}\{T(x)=t\} {n \choose t}^{-1}.
\end{align*}
$$

Esse fenômeno pode ser resumido da seguinte forma:

> **A distribuição de $$X$$ condicional ao evento $$T(X)=t$$ não depende do parâmetro $$\theta$$. Quando isso acontece, dizemos que a estatística $$T(X)$$ é suficiente para $$\theta$$.**

Antes de continuarmos, vamos analisar um caso em que uma estatística $$\tilde{T}$$ não é suficiente para $$\theta$$ para criarmos um pouco mais de intuição sobre a definição acima. Para isso, considere por exemplo, a estatística 

$$
\tilde{T} = X_1+\dots+X_{n-1},
$$

isto é, vamos somar a quantidade de "caras", porém vamos ignorar o que aconteceu no último lançamento. Temos então que, 

$$
\begin{align*}
p_{\theta}(x) &= \theta^{T(x)+x_n} (1-\theta)^{n-T(x)-x_n}\\
&= \theta^{T(x)} (1-\theta)^{n-T(x)}\theta^{x_n} (1-\theta)^{n-x_n}
\end{align*}
$$

Note que nesse caso, quando condicionamos sobre o evento $$T(X)=t$$, não conseguimos "isolar" as $${n-1 \choose t}$$ sequências em que foram observadas $$t$$ "caras" do efeito de $$\theta$$. De fato, quando calculamos a probabilidade condicionada em tal evento, vemos que seu valor final depende de $$\theta$$ através de um fator de $$\theta^{x_n}(1-\theta)^{x_n}$$ .

No próximo exemplo, tentarei dar mais intuição sobre esse processo de "isolar" a distribuição de probabilidade através do condicionamento de estatísticas suficientes.

## Exemplo 2: Distribuição uniforme

Suponha que temos $$X=(X_1,\dots,X_n)$$ onde cada coordenada é i.i.d. e $$X_i\sim \textrm{Uniform}([0,\theta]).$$ **Nosso objetivo é encontrar uma estatística suficiente para $$\theta$$**. Note que,

$$
\begin{align*}
p_{\theta}(x)&= \frac{1}{\theta^n}\prod_{i=1}^n \mathbb{1}\{\theta\leq x_1\leq \theta\}\\
&=\frac{1}{\theta^n}\mathbb{1}\{\theta\leq x_1,\dots,x_n\leq \theta\}\\
& =\frac{1}{\theta^n} \mathbb{1}\{0\leq  \min\{x_1,\dots,x_n\}\}\mathbb{1}\{\max\{x_1,\dots,x_n\}\leq \theta\}
\end{align*}
$$


Seguindo a mesma intuição do exemplo das moedas, a expressão acima nos parece dizer que tudo o que realmente precisamos saber sobre a expressão acima **quando a tarefa é estimar $$\theta$$** é saber o valor de $$T(X)=\max\{X_1,\dots,X_n\}$$ e que  condicionar a distribuição de $$X$$ no evento $$T(X)=t$$ é suficiente para isolarmos a aleatoriedade da expressão acima do parâmetro $$\theta$$.

De fato, é fácil provar que $$T(X)$$ é suficiente utilizando a definição que demos anteriormente (**FAZER**).

# Teorema de Fatorização

Perceba que em todos os exemplos anteriores, a intuição para encontrarmos uma estatística suficiente foi:

1. Escrever a expressão da distribuição de probabilidade $$p_\theta(x)$$;
2. Tentar isolar expressões que envolvem $$\theta$$ de outros fatores que não envolvem o parâmetro que queremos estimar.

De fato, essa intuição que criamos analisando os exemplos anteriores pode ser formalizada através do seguinte teorema:

> **Teorema de Fatorização:** Seja $$\mathcal{P}$$ um modelo com densidades $$p_\theta$$ absolutamente contínuas com relação à uma medida $$\mu$$. Então, $$T(X)$$ é suficiente para $$\mathcal{P}$$ se, e somente se,  existirem funções não negativas $$g_\theta$$ e $$h$$ para as quais
> 
> $$
> p_\theta(x) = g_\theta(T(x))h(x),
> $$
>
> para $$\mu$$-q.t.p $$x$$.

Note que isso facilita muito nosso trabalho em descobrir se uma estatística $$T(X)$$ é suficiente. Por exemplo, no exemplo das distribuições uniformes, tomando $$T(X)=\max\{X_1,\dots,X_n\}$$,  $$h(x) =\min\{X_1,\dots,X_n\} $$ e $$g_\theta(x) = \frac{1}{\theta^n} \mathbb{1}\{0\leq  x\}$$, temos que:

$$
\begin{align*}
p_{\theta}(x)&= \frac{1}{\theta^n} \mathbb{1}\{0\leq  \min\{x_1,\dots,x_n\}\}\mathbb{1}\{\max\{x_1,\dots,x_n\}\leq \theta\}\\
&= g_\theta(x)h(x).
\end{align*}
$$

Além de ser uma ferramenta ótima para encontrarmos estatística suficientes, o teorema de fatorização ainda nos fornece uma excelente explicação sobre o porquê da intuição que utilizamos anteriormente de fato funciona na prática. 

**Prova do teorema (caso discreto):** $$(\Leftarrow)$$Primeiro, vamos supor que $$p_\theta(x) = g_\theta(T(x))h(x)$$ e provar que de fato $$T(X)$$ é suficiente para $$\theta$$, isto é, queremos provar que quando condicionado à $$T(X)=t$$, a distribuição de probabilidade de $$X$$ não depende de $$\theta$$. De fato, temos que

$$
\begin{align*}
P_\theta(X=x\mid T(X)=t ) & \overset{\textrm{hip}}{=} \frac{p_\theta(x)\mathbb{1}\{T(x)=t\}}{P_\theta(T(X)=t)}\\
& = \frac{p_\theta(x)\mathbb{1}\{T(x)=t\}}{\sum_{T(x)=t} p_\theta(x)}\\
& = \frac{g_\theta(T(x))h(x)\mathbb{1}\{T(x)=t\}}{\sum_{T(x)=t} g_\theta(T(x))h(x)}\\
& = \frac{g_\theta(t)h(x)\mathbb{1}\{T(x)=t\}}{\sum_{T(x)=t} g_\theta(t)h(x)}\\
& = \frac{h(x)\mathbb{1}\{T(x)=t\}}{\sum_{T(x)=t} h(x)},
\end{align*}
$$

e essa última expressão **não depende** de $$\theta.$$ Perceba que isso explica muito bem nossa intuição de escrever $$p_\theta$$ e isolar os fatores que contém $$\theta$$, já que quando escrever a probabilidade condicional, os fatores isolados se cancelam no quociente acima.

$$(\Rightarrow)$$ Agora vamos supor que $$T(X)$$ é suficiente para $$\theta$$ e mostrar que conseguimos fatorar $$p_\theta$$ como no enunciado. De fato, note que:

$$
\begin{align*}
p_\theta(x) &= P_\theta(X=x)\\
& \overset{(i)}{=} P_\theta(X=x, T(X)=T(x))\\
& = P_\theta(X=x\mid T(X)=T(x))P_\theta(T(X)=T(x))\\
& \overset{(ii)}{=}P(X=x\mid T(X)=T(x))P_\theta(T(X)=T(x))
\end{align*}
$$

onde (i) vale já que $$T(x)=T(x)$$ é completamente determinado por $$X=x$$ (pense sobre isso!) e (ii) vale pela hipótese de suficiência. Portanto basta tomarmos $$h(x) =P(X=x\mid T(x)=t) $$ e $$g_\theta(t) = P_\theta(T(x)=t)$$.

```
NEXT:
- fazer mais exemplos com e sem fatorização
- colocar refs
- colocar footnote para abs continua
- famílias expos
```
