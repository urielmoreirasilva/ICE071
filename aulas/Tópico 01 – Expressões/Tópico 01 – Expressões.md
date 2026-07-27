---
layout: default
title: "Tópico 01 – Expressões"
parent: "Aulas"
nav_order: 1
---
# Tópico 01 – Expressões [<img src="images/colag_logo.svg" style="float: right; vertical-align: middle; width: 42px; height: 42px;">](https://colab.research.google.com/github/urielmoreirasilva/urielmoreirasilva.github.io/blob/main/aulas/T%C3%B3pico%2001/01%20%E2%80%93%20Expressoes.ipynb) [<img src="images/github_logo.svg" style="float: right; margin-right: 12px; vertical-align: middle; width: 36px; height: 36px;">](https://github.com/urielmoreirasilva/urielmoreirasilva.github.io/blob/main/aulas/T%C3%B3pico%2001/01%20%E2%80%93%20Expressoes.ipynb)

Primeiros passos em Python.

### Resultados Esperados
1. Aprender sobre o que é um notebook e um arquivo `.py`.
1. Aprender a fazer matemática simples em Python.
1. Entender as ferramentas básicas de Ciência de Dados.

### Referências
- [BPD, Capítulos 1 a 6](https://notes.dsc10.com/)
- [CIT, Capítulos 3 e 4](https://inferentialthinking.com/)

Material adaptado do [DSC10 (UCSD)](https://dsc10.com/) por [Flavio Figueiredo (DCC-UFMG)](https://flaviovdf.io/fcd/) e [Uriel Silva (DEST-UFMG)](https://urielmoreirasilva.github.io)

## Código, Python e Jupyter 💻

### O que é "código"?

- As instruções para computadores são escritas em **linguagens de programação** e são chamadas de **código**.
- "Programas de computador" são como **receitas**: escrevemos programas que dizem ao computador exatamente o que fazer, e ele faz exatamente isso – nada mais e nada menos.

### Por que Python?

<center>
<img src='images/languages.png' width=400>
</center>

- Popular.
- Variedade de usos.
- Desenvolvimento web.
- Ciência de dados e aprendizado de máquina.
- Fácil de começar!

### ...mas existem outras linguagens também!

- O [R](https://www.r-project.org/) é a outra principal linguagem de programação utilizada para Ciência de Dados.
- A maior parte dos times de desenvolvimento em Ciência de Dados trabalha com uma mistura de [_ambos_](https://www.datacamp.com/blog/python-vs-r-for-data-science-whats-the-difference) Python e R!
- Tradicionalmente, o R vêm sendo desenvolvido pela comunidade estatística _exclusivamente_ para análise de dados, então possui uma [comunidade bem ativa](https://stackoverflow.com/questions/tagged/r) e algumas ferramentas bem avançadas!

<center>
    <img src = "images/Python_and_R.png" width = 50%>
</center> 

### Notebooks Jupyter 📓

- Frequentemente, escrevemos código em um editor de texto e depois executamos esse código em uma interface de linha de comando.

<center>
<img src='images/terminal.png' width=800>
</center>

- Porém, por ser uma _linguagem interpretada_, o Python nos permite trabalhar com execução de código em _tempo real_ na maior parte das IDEs (ambiente de desenvolvimento integrado, ou _integrated development environment_).
- O [Jupyter](https://jupyter.org/), em particular, é uma IDE bem popular para o ensino e para a prática de Ciência de Dados. 
    - O nome "Jupyter" é uma referência às 3 linguagens de programação suportadas pelo Jupyter: _Julia_, _Python_ e _R_.
    - Através dos seus **Notebooks**, o Jupyter nos permite escrever e executar código em um único documento, renderizar texto e _Markdown_, e muito mais! 

## Expressões

### Utilizando o Python como uma calculadora

- Uma **expressão** é uma combinação de _valores_, _operadores_ e _funções_ cujo **resultado** é um **valor**.
- Nesse sentido, podemos utilizar o Python como uma calculadora – ele pega expressões e avalia seu resultado.
- Inserimos nossas expressões em **células de código**.
- Para executar uma célula de código:
    - **Pressione `shift` + `enter` (ou `shift` + `return`) no teclado (de preferência)**, ou
    - Pressione o botão "▶ Executar" na barra de ferramentas.


```python
17
```




    17




```python
-1 + 3.14
```




    2.14




```python
2 ** 3
```




    8




```python
(17 - 14) / 2
```




    1.5



Nota: o padrão do Jupyter é exibir apenas o _último_ valor de uma célula de código. 


```python
3 * 4
5
```




    5



### Cheatsheet: operações aritméticas básicas no Python

| Operação | Operador | Exemplo | Valor |
| --- | --- | --- | --- |
| Adição | `+` | `2 + 3` | `5` |
| Subtração | `-` | `2 - 3` | `-1` |
| Multiplicação | `*` | `2 * 3` | `6` |
| Divisão | `/` | `7/3` | `2.66667` |
| Restante | `%` | `7% 3` | `1` |
| Exponenciação | `**` | `2 ** 0,5` | `1.41421` |

### Ordem de operações no Python

- O Python utiliza a ordem típica de operações aritméticas: PEMDAS (_Parentheses, Exponents, Multiplication, Division, Addition and Subtraction_).
- O PEMDAS também é conhecido como BEDMAS (🛏️?): _Brackets, Exponents, Division, Multiplication, Addition and Subtraction_.


```python
3 * 2 ** 2
```




    12




```python
(3 * 2) ** 2
```




    36



### Exercício ✅

Na célula abaixo, substitua as reticências por uma expressão equivalente a

$$(19 + 6 \cdot 3) - 15 \cdot \left(\sqrt{100} \cdot \frac{1}{30}\right) \cdot \frac{3}{5} + \frac{4 ^2}{2^3} + \left( 6 - \frac{2}{3} \right) \cdot 12 $$

Tente usar parênteses somente quando necessário.


```python
...
```




    Ellipsis



## Variáveis

### Motivação

Abaixo, calculamos o número de segundos em um ano.


```python
60 * 60 * 24 * 365
```




    31536000



Se quisermos utilizar o valor acima mais tarde no nosso bloco de notas para determinar, digamos, o número de segundos em 12 anos, teremos de copiar e colar a expressão. 

**Isso é inconveniente, e muitas vezes leva à introdução de erros no código.**


```python
60 * 60 * 24 * 365 * 12
```




    378432000



Seria ótimo então se pudéssemos **armazenar** o valor inicial e consultá-lo mais tarde!

### Variáveis ​​e instruções de atribuição

- Uma **variável** é um objeto que armazena um valor para que possa ser consultado posteriormente em nosso código.
- Para definir uma variável, utilizamos uma **instrução de atribuição**:

$$ \overbrace{\text{minha \: variável}}^{\text{nome}} = \overbrace{\texttt{2 + 3}}^{\text{qualquer expressão}} $$

- Uma instrução de atribuição altera o significado do **nome** à esquerda do símbolo `=`.

- A expressão do lado direito do símbolo `=` é avaliada antes de ser atribuída ao nome do lado esquerdo.
- No exemplo acima, `myvariable` está vinculado a `5` (valor) e não a `2 + 3` (expressão).

Observe que, antes de usá-lo em uma instrução de atribuição, uma variável denominada `more_than_1` não tem significado.


```python
# Descomente e execute
# more_than_1
```

Depois de usá-lo em uma instrução de atribuição, podemos pedir para printar o seu valor.


```python
# Note que uma instrução de atribuição não gera nenhuma saída!
more_than_1 = 15 - 5
```


```python
more_than_1
```




    10



Sempre que usarmos `more_than_1` em uma expressão daqui em diante, `more_than_1` é substituído por `10`.


```python
more_than_1 * 2
```




    20



Observe que a expressão acima **não alterou** o valor de `more_than_1`, porque **não reatribuímos** `more_than_1`!


```python
more_than_1
```




    10



### Nomeando variáveis

- Em geral, é uma boa prática dar nomes úteis às suas variáveis ​​para que você saiba a que elas se referem.
- Nomes de variáveis ​​podem conter caracteres maiúsculos e minúsculos, dígitos de 0 a 9 e sublinhados/underlines "_".
- Nomes de variáveis não podem começar com um número.
- Nomes de variáveis não podem conter pontos ".". 
- Nomes de variáveis diferenciam letras maiúsculas de minúsculas!

As instruções de atribuição a seguir são **válidas**, porém usam nomes de variáveis ​​que na prática podem "**não ser muito bons**" 😕.


```python
six = 15
```


```python
i_45love_chocolate_9999 = 60 * 60 * 24 * 365
```

As instruções de atribuição a seguir são **válidas**, e utilizam nomes de variáveis "​​**bons**" ✅.


```python
seconds_per_hour = 60 * 60
hours_per_year = 24 * 365
seconds_per_year = seconds_per_hour * hours_per_year
```

As seguintes "declarações de atribuição" são **inválidas ❌**.


```python
# Descomente e execute
# 6 = 15
```


```python
# Descomente e execute
# 3 = 2 + 1
```

### Declarações de atribuição não são equações matemáticas!

- Ao contrário da matemática, onde $x = 3$ significa a mesma coisa que $3 = x$, as instruções de atribuição **não são simétricas**.
- Uma instrução de atribuição atribui o nome à esquerda de `=` ao valor à direita de `=`, nada mais.


```python
x = 3
x
```




    3




```python
# Descomente e execute
# 4 = x
```

### O valor de uma variável é definido no momento da atribuição


```python
uc = 2
sd = 3 + uc
```

As declarações de atribuição não são **permanentes** – o valor de uma variável pode mudar!


```python
uc = 7
uc
```




    7



Observe que mesmo depois de alterar `uc`, não alteramos `sd`, então essa variável ainda retém o mesmo valor de antes.


```python
sd
```




    5



### Uma analogia útil

<center>
<img src='images/box.png' width=600>
</center>

- Uma metáfora comum é que as variáveis ​​são como "caixas" ou "contêineres" ([fonte](https://www.tomasbeuzen.com/python-programming-for-data-science/chapters/chapter1-basics.html)).
- Outra analogia: uma declaração de atribuição é como colocar um adesivo em um valor.

### Exercício ✅

Suponha que você tenha executado as três linhas de código a seguir:

```py
side_length = 5
area = side_length ** 2
side_length = side_length + 2
```

Quais são os valores de `side_length` e `area` após a execução?

A. `side_length = 5`, `area = 25`

B. `side_length = 5`, `area = 49`

C. `side_length = 7`, `area = 25`

D. `side_length = 7`, `area = 49`

E. Nenhuma das opções acima

## Expressões de chamada (call expressions) 📞

### Funções algébricas

- Em matemática, as funções recebem alguma entrada e retornam alguma saída:

$$f(x, y) = 2x^2 + 3xy - 1$$

- Dessa forma, podemos determinar a saída de uma função mesmo se passarmos argumentos relativamente complicados:

$$f\left(\frac{1+2}{3+4}, (-1)^{15}\right) = -\frac{94}{49}$$

### Expressões de chamada

* **Expressões de chamada** em Python invocam _funções_ – elas dizem a uma função para "executar sua receita".
* As funções em Python funcionam da mesma forma que as funções em matemática!
* As entradas de uma função são denominadas seus **argumentos**.


```python
abs(-12)
```




    12



- Algumas funções podem receber um número variável de argumentos


```python
max(3, -4)
```




    3




```python
max(2, -3, -6, 10, -4)
```




    10




```python
# Nota: esses são apenas 2 argumentos!
max(4 + 5, 5 - 4)
```




    9



Podemos usar ```?``` depois de uma função para ver a documentação de uma função:


```python
max?
```


    [1;31mDocstring:[0m
    max(iterable, *[, default=obj, key=func]) -> value
    max(arg1, arg2, *args, *[, key=func]) -> value
    
    With a single iterable argument, return its biggest item. The
    default keyword-only argument specifies an object to return if
    the provided iterable is empty.
    With two or more arguments, return the largest argument.
    [1;31mType:[0m      builtin_function_or_method


Outra alternativa é utilizar a função `help`:


```python
help(max)
```

    Help on built-in function max in module builtins:
    
    max(...)
        max(iterable, *[, default=obj, key=func]) -> value
        max(arg1, arg2, *args, *[, key=func]) -> value
        
        With a single iterable argument, return its biggest item. The
        default keyword-only argument specifies an object to return if
        the provided iterable is empty.
        With two or more arguments, return the largest argument.
    
    

Outro exemplo: função `round`.


```python
my_number = 1.22
round(my_number)
```




    1




```python
round?
```


    [1;31mSignature:[0m [0mround[0m[1;33m([0m[0mnumber[0m[1;33m,[0m [0mndigits[0m[1;33m=[0m[1;32mNone[0m[1;33m)[0m[1;33m[0m[1;33m[0m[0m
    [1;31mDocstring:[0m
    Round a number to a given precision in decimal digits.
    
    The return value is an integer if ndigits is omitted or None.  Otherwise
    the return value has the same type as the number.  ndigits may be negative.
    [1;31mType:[0m      builtin_function_or_method



```python
help(round)
```

    Help on built-in function round in module builtins:
    
    round(number, ndigits=None)
        Round a number to a given precision in decimal digits.
        
        The return value is an integer if ndigits is omitted or None.  Otherwise
        the return value has the same type as the number.  ndigits may be negative.
    
    


```python
round(1.22222, 3)
```




    1.222



### Avaliação aninhada (nested evaluation)

Podemos **aninhar** muitas chamadas de função para avaliar expressões sofisticadas.


```python
min(abs(max(-1, -2, -3, min(4, -2))), max(5, 100))
```




    1



E como isso é feito? 🤔

- Sem entrar em mais detalhes técnicos, as funções no Python avaliam seus argumentos da _esquerda para a direita_.
- Na prática, o Python nos mostra apenas o resultado final.


```python
a = abs(max(-1, -2, -3, min(4, -2)))
a
```




    1




```python
b = max(5, 100)
b
```




    100




```python
min(a, b)
```




    1



... e assim em diante.

### Importando módulos
- Em geral, o Python não possui tudo que precisamos de maneira "integrada".
- Para obter funcionalidades adicionais, importamos **módulos** (também conhecidos como **bibliotecas** 📚) por meio de **instruções de importação** (`import`).
- Os **módulos** podem ser considerados coleções de funções e valores no Python.
- Invocamos essas funções usando a sintaxe `module.function()`, chamada "notação de ponto" (_dot notation_).

### Exemplo: `import math`

O módulo `math` contém funções algébricas comuns, como `sqrt`, `log`, `pow`, etc.


```python
import math
```


```python
math.sqrt(9)
```




    3.0




```python
math.pow(3, 2)
```




    9.0




```python
# Qual é a base do log no Python?
math.log?
```


    [1;31mDocstring:[0m
    log(x, [base=math.e])
    Return the logarithm of x to the given base.
    
    If the base not specified, returns the natural logarithm (base e) of x.
    [1;31mType:[0m      builtin_function_or_method


Esse modulo também possui constantes integradas!


```python
math.e
```




    2.718281828459045




```python
math.pi
```




    3.141592653589793



- Raramente precisamos disso, mas apenas para ilustrar o conceito, o código abaixo faz com que o Python "perca o acesso" ao módulo `math`.


```python
# Descomente e execute.
# del math
# math.sqrt(9)
# math.pi
```

### Exercício ✅

Suponha que você tenha executado as seguintes instruções:

```py
x = 3
y = -2
```

Qual desses exemplos resulta em um erro?

A. `abs(x, y)`

B. `math.pow(x, abs(y))`

C. `round(x, max (abs (y ** 2)))`

D. `math.pow(x, math.pow(y, x))`

E. Mais de um dos itens acima

## Tipos de dados/variáveis

- Qual é a diferença entre os números abaixo? 🧐


```python
4 / 2
```




    2.0




```python
5 - 3
```




    2



Para nós, `2.0` e `2` são o mesmo número, $2$. Mas para o Python, esses números são bem diferentes!

### Tipos de dados
- Todo valor/variável/dado em Python tem um **tipo**.
- Use a função `type` para verificar o tipo de um valor.
- É importante entender como diferentes tipos funcionam com diferentes operações, pois os resultados podem nem sempre ser aqueles que esperamos!

### Dois tipos de dados numéricos: ```int``` e ```float```
- ```int``` : Um número _inteiro_ de qualquer tamanho.
- ```float```: Um número (possivelmente não-inteiro) com ponto decimal.

### ```int```
- Se você usar essas operações entre `int`s (`+`, `-`, `*`, `**`), o resultado será outro `int`.
- `int`s têm precisão arbitrária em Python, o que significa que seus cálculos serão sempre exatos.


```python
3 + 5
```




    8




```python
type(3 + 5)
```




    int




```python
2 ** 300
```




    2037035976334486086268445688409378161051468393665936250636140449354381299763336706183397376




```python
2 ** 3000
```




    1230231922161117176931558813276752514640713895736833715766118029160058800614672948775360067838593459582429649254051804908512884180898236823585082482065348331234959350355845017413023320111360666922624728239756880416434478315693675013413090757208690376793296658810662941824493488451726505303712916005346747908623702673480919353936813105736620402352744776903840477883651100322409301983488363802930540482487909763484098253940728685132044408863734754271212592471778643949486688511721051561970432780747454823776808464180697103083861812184348565522740195796682622205511845512080552010310050255801589349645928001133745474220715013683413907542779063759833876101354235184245096670042160720629411581502371248008430447184842098610320580417992206662247328722122088513643683907670360209162653670641130936997002170500675501374723998766005827579300723253474890612250135171889174899079911291512399773872178519018229989376



### ```float```
* Um `float` é especificado usando um ponto **decimal**.
* Um `float` pode ser impresso utilizando notação científica.


```python
2.0 + 3.2
```




    5.2




```python
type(2.0 + 3.2)
```




    float




```python
2.0 ** 300
```




    2.037035976334486e+90



### As armadilhas do ```float```
* `float`s têm tamanho limitado (mas o limite é _enorme_: $\simeq 10^{308}$).
* `float`s têm precisão limitada de 15-16 casas decimais.
* Depois da aritmética, as últimas casas decimais podem estar erradas de maneiras inesperadas (precisão limitada!).


```python
1 + 0.2
```




    1.2




```python
1 + 0.1 + 0.1
```




    1.2000000000000002




```python
1.8 ** 1207
```




    1.299911122329652e+308




```python
# Descomente e execute
# 2.0 ** 3000
```

### Coerção de tipo entre ```int``` e ```float```
- Por padrão, Python muda um `int` para um `float` em uma expressão mista envolvendo ambos os tipos.
- Observe que a divisão de dois `int`s retorna automaticamente um valor `float`.
- Um valor pode ser explicitamente **coagido** (ou seja, convertido) usando as funções ```int``` e ```float```.


```python
2.0 + 3
```




    5.0




```python
2 / 1
```




    2.0




```python
# Coagindo o resultado para int
int(2 / 1)
```




    2




```python
# Nota: a coerção de float para int não apenas remove o ponto decimal, mas também *arrendonda o float para baixo!*
int(3.9)
```




    3



### À parte: modelo de memória Jupyter

<center><img src='images/elephant.png' width=20%></center>

Nosso notebook **ainda** se lembra de todas as variáveis ​​que definimos anteriormente.


```python
more_than_1
```




    10



- No entanto, se você fechar e retornar ao seu notebook depois de algum tempo, ele normalmente “esquecerá” todas as variáveis ​​armazenadas.
- Quando isso acontecer, você precisará executar novamente as células do seu notebook!

## Resumo

- Expressões são avaliadas como valores.
- O padrão do Jupyter é sempre exibir apenas o valor da última expressão em uma célula de código.
- O Python suporta todos os operadores matemáticos padrão, e segue a ordem de operações PEMDAS.
- As instruções de atribuição nos permitem vincular valores a variáveis.
- Podemos avaliar funções em Python da mesma forma que avaliamos funções em matemática.
- O Python contém algumas funções nativas, e as instruções de importação nos permitem ter acesso a outras funções através dos mais diversos módulos.
- Todos os valores em Python possuem um tipo:
    - `int`s e `float`s, por exemplo, são números.
    - `int`s são inteiros, enquanto `float`s contêm pontos decimais.
