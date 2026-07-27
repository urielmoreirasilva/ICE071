---
layout: default
title: "Tópico 10 – Probabilidade"
parent: "Aulas"
nav_order: 10
---
# Tópico 10 – Probabilidade [<img src="images/colag_logo.svg" style="float: right; vertical-align: middle; width: 42px; height: 42px;">](https://colab.research.google.com/github/urielmoreirasilva/urielmoreirasilva.github.io/blob/main/aulas/T%C3%B3pico%2010/10%20%E2%80%93%20Probabilidade.ipynb) [<img src="images/github_logo.svg" style="float: right; margin-right: 12px; vertical-align: middle; width: 36px; height: 36px;">](https://github.com/urielmoreirasilva/urielmoreirasilva.github.io/blob/main/aulas/T%C3%B3pico%2010/10%20%E2%80%93%20Probabilidade.ipynb)

Vamos aprender o básico da Teoria de Probabilidade.

### Resultados Esperados

1. Introduzir os conceitos de espaço amostral, eventos, massa e densidade de probabilidade.
1. Aprender algumas propriedades básicas de probabilidade.
1. Introduzir os conceitos de probabilidade condicional e independência.

### Referências
- [CIT, Capítulo 9](https://inferentialthinking.com/)

Material adaptado do [DSC10 (UCSD)](https://dsc10.com/) por [Flavio Figueiredo (DCC-UFMG)](https://flaviovdf.io/fcd/) e [Uriel Silva (DEST-UFMG)](https://urielmoreirasilva.github.io)

## Probabilidade

- Algumas coisas na vida são _naturalmente_ aleatórias.
- Por exemplo, quando lançamos uma moeda ou um dado 🎲, não sabemos o resultado de antemão, então podemos dizer que esse resultado é _incerto_, ou _aleatório_.
- Porém, ainda que um resultado em particular seja incerto, podemos estudar a _regularidade_ com as quais certos resultados acontecem através da **Teoria de Probabilidade**.

- Novamente tomando como exemplo o lançamento de uma moeda "honesta", a **probabilidade** de observamos "cara" é igual a probabilidade de observarmos "coroa", e ambas são iguais a $\frac{1}{2}$.
- Outro exemplo é o lançamento de um lado de 6 faces: a probabilidade com que cada face ocorre é de $\frac{1}{6}$.

- Apesar da Probabilidade ser uma área da Estatística/Matemática muito bem definida em termos formais, é natural que busquemos diferentes _interpretações_ para o que uma probabilidade realmente _representa_.
- A interpretação "clássica" ou **frequentista** nos diz que, se pudéssemos repetir um **experimento aleatório** infinitas vezes, a **frequência** com a qual um resultado ocorre é sua probabilidade de ocorrência.
- Por outro lado, a interpretação "subjetiva" ou **Bayesiana** nos diz que a probabilidade de ocorrência de um resultado é **diferente para cada indivíduo**, e depende do quão **provável** (ou **improvável**) esse resultado é relativo a todos os outros possíveis resultados do experimento em questão.

- Nesse curso, adotaremos a interpretação frequentista, e utilizaremos **frequências relativas para estimar probabilidades**!
    - Veremos isso com mais detalhes nos Tópicos 11 e 12.

### Terminologia básica

**Experimento aleatório**: Um processo ou ação cujo resultado é aleatório.

- Exemplos:
    - lançamento de um dado;
    - lançamento de uma moeda duas vezes;
    - ocorrência de chuva no dia de hoje;
    - vitória do Galo na Libertadores 2024.

**Espaço amostral**: O conjunto de todos os resultados possíveis de um experimento aleatório.

- Notação: utilizamos $\Omega$ para denotar o espaço amostral.

- Exemplos:
    - $\Omega = \{1, 2, 3, 4, 5, 6\}$;
    - $\Omega = \{(H, H), (H, T), (T, H), (T, T)\}$;
    - $\Omega = \{\text{chove}, \text{não chove}\}$;
    - $\Omega = \{\text{vitória}, \text{derrota}\}$.

**Evento**: um conjunto específico de resultados de interesse do experimento aleatório. 

- Notação: utilizamos $A$ para denotar um evento. Escrevemos $A \subseteq \Omega$, pois formalmente $A$ é um _subconjunto_ de $\Omega$.

- Exemplos:
    - $A = \text{``número par''} = \{2, 4, 6\}$;
    - $A = \text{``pelo menos 1 cara''} = \{(H, H), (H, T), (T, H)\}$;
    - $A = \text{``chove e vou me molhar''} = \{ \}$;
    - $A = \text{``felicidade da nação atleticana''} = \{ \text{vitória} \}$.

**Probabilidade**: um número entre 0 e 1 (equivalentemente, entre 0% e 100%) que descreve a probabilidade de um evento.

- Notação: utilizamos $P(A)$ para denotar a probabilidade de um evento $A$. Temos sempre $P(A) \in [0, 1]$.

- Exemplos:
    - $P(A) = 1/2 = 0.50 = 50\%$;
    - $P(A) = 3/4 = 0.75 = 75\%$;
    - $P(A) = 0 = 0\%$;
    - $P(A) = \,?$

- Nota: o evento $A = \{ \}$ é denominado **evento impossível**, pois $P(\{ \}) = 0$.
- Analogamente, o evento $A = \Omega$ é denominado **evento certo**, pois $P(\Omega) = 1$.

### Resultados igualmente prováveis

- Se todos os resultados do espaço amostral $\Omega$ forem _equiprováveis_ (isto é, igualmente prováveis), então a probabilidade de qualquer evento $A \subseteq \Omega$ é dada por

\begin{equation*}
    P(A) = \frac{\# \text{de elementos em } A}{\# \text{de elementos em } \Omega} = \frac{\#(A)}{\#(\Omega)}
\end{equation*}

#### Exemplo

- Suponha que lancemos uma moeda "justa" 3 vezes. Qual é a probabilidade de vermos exatamente 2 caras?

O espaço amostral nesse exemplo é dado por $\Omega = \{(H, H, H), (H, H, T), (H, T, H), (H, T, T), (T, H, H), (T, H, T), (T, T, H), (T, T, T)\}$. 

Nosso evento de interesse é $A = \{(H, H, T), (H, T, H), (T, H, H)\}$.

Dessa forma, como $\#(A) = 3$ e $\#(\Omega) = 2^3 = 8$, então $P(A) = 3/8$.

### Exercício ✅

Suponha que você tenha três cartas: uma vermelha, uma azul e outra verde. 

Qual é a probabilidade de você escolher uma das cartas aleatoriamente e ela ser verde, e então – **sem devolvê-la** – você escolher outra carta aleatoriamente e ela ser vermelha?

A. $\frac{1}{9}$

B. $\frac{1}{6}$

C. $\frac{1}{3}$

D. $\frac{2}{3}$

E Nenhuma das opções acima.

### Eventos mutuamente exclusivos

- Suponha que $A$ e $B$ sejam dois eventos **mutuamente exclusivos**.
- Isso significa que se $A$ acontecer, $B$ não acontece, e vice-versa.
- Na linguagem de Teoria de Conjuntos, dizemos que $A$ e $B$ são _disjuntos_, isto é, _não existe interseção entre $A$ e $B$_.
- Formalmente, escrevemos $A \cap B = \{ \}$.

- Quando $A$ e $B$ são mutuamente exclusivos, é razoável que a probabilidade de que o evento $\text{``} A \text{ ou } B \text{''}$ ocorra seja igual a **soma das probabilidades** de ocorrência de $A$ e $B$.
- Intuitivamente, $\text{``} A \text{ ou } B \text{''} = A \cup B$.
- Essa regra é denominada de **regra da adição**.

Mais precisamente, a regra da adição diz que, para $A \cap B = \{ \}$,
\begin{equation*}
    P(A \text{ ou } B) = P(A) + P(B)
\end{equation*}

#### Exemplo

- Suponha que estejamos analisando o lançamento de um dado de 6 faces. Qual é a probabilidade de obtermos um 5 **ou** um 6?

O espaço amostral nesse exemplo é dado por $\Omega = \{1, 2, 3, 4, 5, 6\}$. 

Nossos eventos de interesse são $A = \{ 5 \}$ e $B = \{ 6 \}$.

Dessa forma, como $A \cap B = \{ \}$, $A$ e $B$ são mutuamente exclusivos, e $P(A \text{ ou } B) = P(A) + P(B)$.

Como todos os resultados são igualmente prováveis e $\#(\Omega) = 6$, então $P(A) = \#(A) / \#(\Omega) = 1/6$ e $P(B) = \#(B) / \#(\Omega) = 1/6$.

Finalmente, aplicando a regra da adição, chegamos a $P(A \text{ ou } B) = P(A) + P(B) = 1/6 + 1/6 = 2/6 = 1/3$.

### Eventos complementares

- Suponha agora que estejamos interessados na probabilidade de que um evento $A$ **não aconteça**.
- Em Teoria dos Conjuntos, denominamos tais eventos de **complementares**.
- O complementar de $A$ (em $\Omega$) é definido como $A^c$.
- Formalmente, denotamos $\text{``} A \text{ não ocorrer} \text{''} \equiv A^c$.

- Podemos provar, utilizando a regra da adição, que
\begin{equation*}
    P(\text{``} A \text{ não ocorrer} \text{''}) := P(A^c) = 1 - P(A)
\end{equation*}

- O resultado acima é intuitivo, uma vez que os eventos $A$ e $\text{``} A \text{ não ocorrer} \text{''}$ são mutuamente exclusivos, e como um ou o outro _sempre_ ocorrem, a soma de suas probabilidades é igual a 1.

#### Exemplo

- Suponha que $A = \{\text{chover hoje}\}$, e que $P(A) = 20\%$. Então $A^c = \{\text{não chover hoje}\}$, e $P(\text{``} A \text{ não ocorrer} \text{''}) = P(A^c) = 1 - P(A) = 80\%$.

### Eventos simultâneos

- Suponha agora que estejamos interessados na probabilidade de que **ambos** $A$ e $B$ ocorram.
- O evento de interesse aqui pode ser então denotado como $\text{``} A \text{ e } B \text{''}$.
- Intuitivamente, $\text{``} A \text{ e } B \text{''} = A \cap B$.
- É comum denotarmos $P(\text{``} A \text{ e } B \text{''}) = P(A, B)$.

#### Exemplo

- Suponha que você lance um dado de 6 faces. Qual é a probabilidade de o lançamento ser igual a 3 ou menos, e ainda por cima um número par?

O espaço amostral nesse exemplo é dado por $\Omega = \{1, 2, 3, 4, 5, 6\}$. 

Nossos eventos de interesse são $A = \{ 1, 2, 3 \}$ e $B = \{ 2, 4, 6 \}$.

Dessa forma, temos $\text{``} A \text{ e } B \text{''} = A \cap B = \{ 2 \}$.

Como todos os resultados são igualmente prováveis e $\#(\Omega) = 6$, então $P(A \cap B) = \#(A \cap B) / \#(\Omega) = 1/6$.

### Probabilidade Condicional

- Suponha agora que estejamos interessados na probabilidade de que $B$ ocorra, sabendo que $A$ já ocorreu.
- Nesse contexto, definimos a **probabilidade condicional** de $B$ dado $A$ por:

\begin{equation*}
P(\text{``} B \text{ dado } A \text{''}) \equiv P(B | A) := \frac{P(A, B)}{P(A)}
\end{equation*}

- Na probabilidade condicional de $B$ dado $A$, "restringimos" o espaço amostral $\Omega$ a ser igual aos elementos contidos em $A$.
- Em outras palavras, o conhecimento da ocorrência de $A$ **aumenta** a probabilidade de ocorrência de $P(A, B)$, uma vez que aqui temos **mais informação** e logo **menos incerteza**.

- Para ilustrar esse ponto formalmente, note que se todos os elementos de $\Omega$ forem equiprováveis, temos que
\begin{equation*}
    P(B|A) = \frac{P(A, B)}{P(A)} = \frac{\frac{\#(A \cap B)}{\#(\Omega)}}{\frac{\#(A)}{\#(\Omega)}} = \frac{\#(A \cap B)}{\#(\Omega)} \cdot \frac{\#(\Omega)}{\#(A)} = \frac{\#(A \cap B)}{\#(A)}
\end{equation*}
o que corrobora nossa intuição de que $A$ se torna o "novo espaço amostral" quando condicionamos em sua ocorrência.

### Exercício ✅

Suponha que você lance um dado de 6 lados e sabe apenas que o resultado é igual a 3 ou menos. Qual é a probabilidade de que o resultado seja um número par?

A. $\frac{1}{2}$

B. $\frac{1}{3}$

C. $\frac{1}{4}$

D. Nenhuma das opções acima.

### A regra da multiplicação

- A **regra da multiplicação** nos fornece uma maneira de calcular a probabilidade de ocorrência de ambos $A$ e $B$, sabendo qual é a probabilidade **marginal** de $A$ e qual é a probabilidade condicional de $B$ dado $A$.
- Mais especificamente, 

\begin{equation*}
    P(A, B) = P(A) \cdot P(B | A)
\end{equation*}

#### Exemplo (de novo!)

- Suponha que você lance um dado de 6 faces. Qual é a probabilidade de o lançamento ser igual a 3 ou menos, e ainda por cima um número par?

O espaço amostral nesse exemplo é dado por $\Omega = \{1, 2, 3, 4, 5, 6\}$. 

Nossos eventos de interesse são $A = \{ 1, 2, 3 \}$ e $B = \{ 2, 4, 6 \}$.

Sabemos que $P(A) = 1/2$ e que $P(B|A) = 1/3$.

Logo, utilizando a regra da multiplicação, $P(A, B) = 1/2 \cdot 1/3 = 1/6$, assim como obtivemos anteriormente.

### Eventos independentes

- A noção de **eventos independentes** surge naturalmente no contexto de Probabilidade Condicional quando fazemos a seguinte pergunta:

> "e se a ocorrência de $A$ não afetar a ocorrência de $B$? 🤔"

- Formalmente, dois eventos $A$ e $B$ são independentes se
\begin{equation*}
    P(B | A) = P(B)
\end{equation*}

- Agora, pela regra da multiplicação, note que isso implica que
\begin{equation*}
    P(A, B) = P(A) \cdot P(B)
\end{equation*}

- Em geral, ambas as definições são válidas para eventos independentes, mas a consequência de ambas é a mesma: se $A$ e $B$ são independentes, $P(B|A) = P(B)$ e $P(A|B) = P(A)$, de maneira que **o conhecimento da ocorrência de um evento não impacta a probabilidade do outro**.

#### Exemplo

- Suponha que lancemos uma moeda justa repetidas vezes, de maneira independente uma da outra. Qual é a probabilidade de observarmos 50 caras seguidas?

O espaço amostral de _cada lançamento_ nesse exemplo é dado por $\Omega_i = \{H, T\}$, $i = 1, \ldots, 50$.

Nosso evento de interesse é $(A_1, A_2, \ldots, A_{50})$, onde cada $A_i = \{ H \}$. 

Cada $A_i$ têm probabilidade igual a $P(A_i) = 1/2$.

Como os $A_i$ são independentes, então $P(A_1, A_2, \ldots, A_{50}) = (\frac{1}{2})^{50}$.

### Exercício ✅

Suponha que cada vez que você liga para sua avó 👵, a probabilidade de ela atender o telefone é de $\frac{1}{3}$, independentemente se ela atendeu o telefone ou não na última ligação. Se você ligar três vezes para sua avó hoje, qual a chance de você conseguir falar com ela exatamente três vezes?

_Dica_: utilize a independência e a complementariedade dos eventos.

A. $\frac{1}{3}$

B. $\frac{1}{9}$

C. $\frac{1}{27}$

D. $1$

E. Nenhuma das opções acima.

### Booleanos

- A Teoria de Probabilidade é _intrinsicamente_ ligada à Teoria dos Conjuntos.
- Como vimos anteriormente, as operações entre variáveis booleanas também são naturalmente formuladas como operações entre conjuntos.
- Na prática, é muito comum definirmos os eventos sobre os quais estamos interessados através de operações entre booleanas nos nossos `arrays`, `DataFrames`, `Series`, `Lists`, etc; veremos isso mais adiante nos próximos tópicos.

## Resumo

- O conjunto de todos os possíveis resultados de um experimento aleatório é denominado de **espaço amostral**.
- Um **evento** é uma coleção de elementos de interesse do espaço amostral. 
- A **probabilidade** de ocorrência de um evento pode ser interpretada como a **frequência** com a qual esse evento ocorreria caso pudéssemos repetir o experimento aleatório infinitas vezes.
- Existem várias regras para calcular probabilidades. Nesse curso analisaremos muitos casos especiais em que os elementos do espaço amostral são igualmente prováveis.
- Duas regras úteis para o cálculo das probabilidades de certos eventos são:
    1. A **regra da adição**, que afirma que para quaisquer dois eventos **mutuamente exclusivos**, $P(A \text{ ou } B) = P(A) + P(B)$;
    1. A **regra da multiplicação**, que afirma que para quaisquer dois eventos, $P(A, B) = P(B | A) \cdot P(A) \:$.
