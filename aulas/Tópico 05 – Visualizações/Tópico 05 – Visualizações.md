---
layout: default
title: "Tópico 05 – Visualização de Dados"
parent: "Aulas"
nav_order: 5
---
# Tópico 05 – Visualização de Dados 📈 [<img src="images/colag_logo.svg" style="float: right; vertical-align: middle; width: 42px; height: 42px;">](https://colab.research.google.com/github/urielmoreirasilva/urielmoreirasilva.github.io/blob/main/aulas/T%C3%B3pico%2005/05%20%E2%80%93%20Visualizacoes.ipynb) [<img src="images/github_logo.svg" style="float: right; margin-right: 12px; vertical-align: middle; width: 36px; height: 36px;">](https://github.com/urielmoreirasilva/urielmoreirasilva.github.io/blob/main/aulas/T%C3%B3pico%2005/05%20%E2%80%93%20Visualizacoes.ipynb)

Um pouco sobre como representar dados de maneira visual!

### Resultados Esperados
1. Aprender algumas ferramentas simples para exploração de dados.
1. Aprender os conceitos básicos de visualização de dados.
1. Aprender a manipular os DataFrames de `pandas` para produzir gráficos elementares.  

### Referências
- [CIT, Capítulo 7](https://inferentialthinking.com/)

Material adaptado do [DSC10 (UCSD)](https://dsc10.com/) por [Flavio Figueiredo (DCC-UFMG)](https://flaviovdf.io/fcd/) e [Uriel Silva (DEST-UFMG)](https://urielmoreirasilva.github.io)


```python
# Importando BabyPandas e Numpy
import babypandas as bpd
import numpy as np

# Importando Matplotlib
import matplotlib.pyplot as plt
plt.style.use('ggplot')

# Importando alguns outros módulos para nos ajudar nas visualizações
from IPython.display import HTML, display, IFrame
```

## Visualização de dados

### Por que visualizar?

- Os computadores são melhores que os humanos para processar números, mas os humanos (em geral) são melhores para identificar padrões visuais.
- As visualizações nos permitem compreender rapidamente um grande volume de dados, facilitando a identificação de tendências e a comunicação de resultados.
- Existem _vários_ tipos de visualizações – neste tópico, veremos gráficos de dispersão, gráficos de linhas, gráficos de barras e histogramas.
- A escolha "certa" do método de visualização depende sempre do tipo de dado em questão!

## Prelúdio: um pouco de terminologia

### Indivíduos e variáveis

<center><img src='https://raw.githubusercontent.com/flaviovdf/fcd/master/assets/07-DataViz/images/ind-var.png' largura=90%/></center>

- <span style="color:#6d9eeb"><b>Indivíduo (linha):</b></span> Pessoa/lugar/coisa para a qual os dados são registrados. Também chamado de **observação**, ou _data point_.

- <span style="color:#ff9900"><b>Variável (coluna):</b></span> Característica observada para cada indivíduo. Também chamado de **recurso**, ou _feature_.

### Tipos de variáveis

Existem dois tipos principais de variáveis:

- **Numéricas**: Variáveis tais que seus valores permitam operações de aritmética básica.
- **Categóricas**: Variáveis cujos valores se enquadram em _categorias_, que podem ou não ter alguma _ordem_ entre elas.

### Exemplos de variáveis ​​numéricas

- Conjunto de dados: Salários dos jogadores da NBA. 🏀
    - Indivíduo: um jogador da NBA.
    - Variável: seu salário.

- Conjunto de dados: O rendimento no _box office_ de vários filmes. 🎬💰
    - Indivíduo: um filme.
    - Variável: o rendimento do filme no _box office_.

- Conjunto de dados: Doses de reforço de vacinas administradas por dia. 💉
    - Indivíduo: data de cada dia onde foram administradas as vacinas.
    - Variável: número de doses de reforço administradas em cada data.

### Exemplos de variáveis ​​​​categóricas

- Conjunto de dados: Gêneros de filmes. 🎬
    - Indivíduo: um filme.
    - Variável: seu gênero.

- Conjunto de dados: Códigos de Endereço Postais (CEPs). 🏠
    - Indivíduo: um habitante de uma cidade, ou região.
    - Variável: seu CEP.

Nota: apesar de serem reportados como números, os CEPs na verdade são categóricos (operações aritméticas básicas não têm sentido quando aplicadas aos CEPs).

- Conjunto de dados: Nível de experiência anterior em programação para alunos de Ciência de Dados 🧑‍🎓.
    - Indivíduo: um aluno.
    - Variável: seu nível de experiência anterior em programação, por ex.: "nenhum", "baixo", "médio" ou "alto".

Nota: essa é uma variável categórica _ordenada_!

### Exercício ✅

Qual destas **não** é uma variável numérica?

A. Gasto de combustível em quilômetros por litro.

B. Número de semestres de um curso na UFMG.

C. Período do curso na UFMG (primeiro, quinto, sétimo, etc).

D. Número de uma conta bancária.

E. Mais de uma das acima não são variáveis ​​numéricas.

### Tipos de visualizações

O _tipo de visualização_ que criamos depende dos _tipos de variáveis_ ​​que estamos visualizando.

- **Gráfico de dispersão**: numérica vs. numérica.
- **Gráfico de linhas**: numérica "sequencial" (por exemplo no tempo) vs. numérica.
- **Gráfico de barras**: categórica vs. numérica.
- **Histograma**: numérica.

Veremos todos os esses tipos de gráficos nesse e no próximo tópico.

## Gráficos de dispersão

### Exemplo: os 50 atores de maior bilheteria

|Coluna |Conteúdo|
|----------|------------|
`'Actor'`|Nome do ator
`'Total Gross'`| Receita total bruta no _box office_, em milhões de dólares, de todos os filmes do ator
`'Number of Movies'`| O número total de filmes em que o ator esteve
`'Average per Movie'`| O total de receita bruta dividido pelo número total de filmes
`'#1 Movie'`| O filme de maior bilheteria em que o ator já esteve
`'Gross'`| Receita bruta de bilheteria interna, em milhões de dólares, do filme de maior bilheteria do ator


```python
actors = bpd.read_csv('data/actors.csv').set_index('Actor')
actors
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Gross</th>
      <th>Number of Movies</th>
      <th>Average per Movie</th>
      <th>#1 Movie</th>
      <th>Gross</th>
    </tr>
    <tr>
      <th>Actor</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Harrison Ford</th>
      <td>4871.7</td>
      <td>41</td>
      <td>118.8</td>
      <td>Star Wars: The Force Awakens</td>
      <td>936.7</td>
    </tr>
    <tr>
      <th>Samuel L. Jackson</th>
      <td>4772.8</td>
      <td>69</td>
      <td>69.2</td>
      <td>The Avengers</td>
      <td>623.4</td>
    </tr>
    <tr>
      <th>Morgan Freeman</th>
      <td>4468.3</td>
      <td>61</td>
      <td>73.3</td>
      <td>The Dark Knight</td>
      <td>534.9</td>
    </tr>
    <tr>
      <th>Tom Hanks</th>
      <td>4340.8</td>
      <td>44</td>
      <td>98.7</td>
      <td>Toy Story 3</td>
      <td>415.0</td>
    </tr>
    <tr>
      <th>Robert Downey, Jr.</th>
      <td>3947.3</td>
      <td>53</td>
      <td>74.5</td>
      <td>The Avengers</td>
      <td>623.4</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Jeremy Renner</th>
      <td>2500.3</td>
      <td>21</td>
      <td>119.1</td>
      <td>The Avengers</td>
      <td>623.4</td>
    </tr>
    <tr>
      <th>Philip Seymour Hoffman</th>
      <td>2463.7</td>
      <td>40</td>
      <td>61.6</td>
      <td>Catching Fire</td>
      <td>424.7</td>
    </tr>
    <tr>
      <th>Sandra Bullock</th>
      <td>2462.6</td>
      <td>35</td>
      <td>70.4</td>
      <td>Minions</td>
      <td>336.0</td>
    </tr>
    <tr>
      <th>Chris Evans</th>
      <td>2457.8</td>
      <td>23</td>
      <td>106.9</td>
      <td>The Avengers</td>
      <td>623.4</td>
    </tr>
    <tr>
      <th>Anne Hathaway</th>
      <td>2416.5</td>
      <td>25</td>
      <td>96.7</td>
      <td>The Dark Knight Rises</td>
      <td>448.1</td>
    </tr>
  </tbody>
</table>
<p>50 rows × 5 columns</p>
</div>



### Visualizando a relação entre duas variáveis

#### Qual é a relação entre `'Number of Movies'` e `'Total Gross'`?

Uma das maneiras de visualizar essa relação é através de um **diagrama de dispersão**, também conhecido como **gráfico de dispersão**:


```python
actors.plot(kind = 'scatter', x = 'Number of Movies', y = 'Total Gross');
```


    
![png](T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_files/T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_26_0.png)
    


- Os diagramas de dispersão (_scatter plots_) consistem de um arranjo dos valores de cada uma das duas colunas selecionadas de um `DataFrame` em pontos nas ordenadas $x$ e $y$ de um diagrama Cartesiano.
- Cada um dos pontos do diagrama de dispersão representam uma linha no nosso DataFrame. 
- Os diagramas de dispersão são muito úteis para visualizar a relação entre duas variáveis _​​numéricas_!

- Para criar um gráfico de dispersão a partir de um DataFrame `df` genérico com duas colunas numéricas `'x_column_for_horizontal'` e `'y_column_for_vertical'`, invocamos
```
df.plot(
    kind = 'scatter', 
    x = x_column_for_horizontal, 
    y = y_column_for_vertical
)
```

Nota: em geral coloamos um ponto e vírgula após uma chamada para `.plot`, para ocultar a saída de texto que acompanha a execução desse método.


```python
# O texto que aparece após a execução da célula abaixo não aparece quando colocamos ";" após chamarmos o método `.plot`
actors.plot(kind = 'scatter', x = 'Number of Movies', y = 'Total Gross')
```




    <Axes: xlabel='Number of Movies', ylabel='Total Gross'>




    
![png](T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_files/T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_29_1.png)
    


Analisando o diagrama de dispersão acima, vemos uma associação positiva, mas bem dispersa, entre o número de filmes de um ator e o total de suas receitas no box office.

#### Qual é a relação entre `'Number of Movies'` e `'Average per Movie'`?


```python
actors.plot(kind = 'scatter', x = 'Number of Movies', y = 'Average per Movie');
```


    
![png](T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_files/T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_32_0.png)
    


No gráfico acima, vamos associação _negativa_ entre as duas variáveis, e um _valor discrepante_ (_outlier_).

#### Qual ator esteve em 60 ou mais filmes?


```python
actors[actors.get('Number of Movies') >= 60]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Gross</th>
      <th>Number of Movies</th>
      <th>Average per Movie</th>
      <th>#1 Movie</th>
      <th>Gross</th>
    </tr>
    <tr>
      <th>Actor</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Samuel L. Jackson</th>
      <td>4772.8</td>
      <td>69</td>
      <td>69.2</td>
      <td>The Avengers</td>
      <td>623.4</td>
    </tr>
    <tr>
      <th>Morgan Freeman</th>
      <td>4468.3</td>
      <td>61</td>
      <td>73.3</td>
      <td>The Dark Knight</td>
      <td>534.9</td>
    </tr>
    <tr>
      <th>Bruce Willis</th>
      <td>3189.4</td>
      <td>60</td>
      <td>53.2</td>
      <td>Sixth Sense</td>
      <td>293.5</td>
    </tr>
    <tr>
      <th>Robert DeNiro</th>
      <td>3081.3</td>
      <td>79</td>
      <td>39.0</td>
      <td>Meet the Fockers</td>
      <td>279.3</td>
    </tr>
    <tr>
      <th>Liam Neeson</th>
      <td>2942.7</td>
      <td>63</td>
      <td>46.7</td>
      <td>The Phantom Menace</td>
      <td>474.5</td>
    </tr>
  </tbody>
</table>
</div>



#### E quem é o outlier no último diagrama?

Podemos identificar o outlier no diagrama anterior buscando pelo único ator que fez menos que 10 filmes.


```python
actors[actors.get('Number of Movies') < 10]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Gross</th>
      <th>Number of Movies</th>
      <th>Average per Movie</th>
      <th>#1 Movie</th>
      <th>Gross</th>
    </tr>
    <tr>
      <th>Actor</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Anthony Daniels</th>
      <td>3162.9</td>
      <td>7</td>
      <td>451.8</td>
      <td>Star Wars: The Force Awakens</td>
      <td>936.7</td>
    </tr>
  </tbody>
</table>
</div>



A média de receita no box office desse ator é bem alta!

#### Anthony Daniels

<center><img src='images/c3po.png' width=200></center>

## Gráficos de linha 📉

### Exemplo: agregando filmes por ano

|Coluna| Conteúdo|
|------|-----------|
`'Year'`| Ano
`'Total Gross in Billions'`| Total bruto de bilheteria doméstica, em bilhões de dólares, de todos os filmes lançados no ano
`'Number of Movies'`| Número de filmes lançados no ano
`'#1 Movie'`| Filme de maior bilheteria no ano


```python
movies_by_year = bpd.read_csv('data/movies_by_year.csv').set_index('Year')
movies_by_year
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Gross in Billions</th>
      <th>Number of Movies</th>
      <th>#1 Movie</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2022</th>
      <td>5.64</td>
      <td>380</td>
      <td>Top Gun: Maverick</td>
    </tr>
    <tr>
      <th>2021</th>
      <td>4.48</td>
      <td>439</td>
      <td>Spider-Man: No Way Home</td>
    </tr>
    <tr>
      <th>2020</th>
      <td>2.11</td>
      <td>456</td>
      <td>Bad Boys for Life</td>
    </tr>
    <tr>
      <th>2019</th>
      <td>11.36</td>
      <td>910</td>
      <td>Avengers: Endgame</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>11.89</td>
      <td>993</td>
      <td>Black Panther</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1981</th>
      <td>0.90</td>
      <td>56</td>
      <td>Superman II</td>
    </tr>
    <tr>
      <th>1980</th>
      <td>1.64</td>
      <td>68</td>
      <td>Star Wars: Episode V - The Empire Strikes Back</td>
    </tr>
    <tr>
      <th>1979</th>
      <td>1.23</td>
      <td>40</td>
      <td>Superman</td>
    </tr>
    <tr>
      <th>1978</th>
      <td>0.83</td>
      <td>13</td>
      <td>Grease</td>
    </tr>
    <tr>
      <th>1977</th>
      <td>0.44</td>
      <td>9</td>
      <td>Star Wars: Episode IV - A New Hope</td>
    </tr>
  </tbody>
</table>
<p>46 rows × 3 columns</p>
</div>



- **Pergunta**: como o número de filmes lançados por ano mudou ao longo do tempo? 🤔


```python
movies_by_year.plot(kind = 'line', y = 'Number of Movies');
```


    
![png](T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_files/T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_45_0.png)
    


### Gráficos de linha

- Os gráficos de linhas mostram tendências em variáveis ​​numéricas ao longo do tempo.

- Para criar um gráfico de linhas a partir de um DataFrame `df` genérico com duas colunas numéricas `'x_column_for_horizontal'` e `'y_column_for_vertical'`, invocamos

````python
df.plot(
    kind = 'line', 
    x = x_column_for_horizontal, 
    y = y_column_for_vertical
)
````

- **Dica**: quando quisermos que o eixo $x$ seja o índice do DataFrame, basta omitirmos o argumento `x =`!

Naturalmente, isso não funciona para gráficos de dispersão, mas funciona para a maioria dos outros tipos de gráficos.


```python
movies_by_year.plot(kind = 'line', y = 'Number of Movies');
```


    
![png](T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_files/T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_49_0.png)
    


#### Filtrando pelo índice

- Muitas vezes estamos interessados em _encurtar_ o horizonte de um gráfico de linhas.
- Isso pode nos ajudar a melhorar a visualização geral ou nos permitir discernir melhor algum detalhe específico, por exemplo.
- Para realizar esse encurtamento, basta invocar o plot após filtrar o DataFrame da maneira desejada por seu índice.

No exemplo acima, podemos criar um gráfico de linhas considerando apenas os anos de 2000 em diante:


```python
movies_by_year[movies_by_year.index >= 2000].plot(kind='line', y='Number of Movies');
```


    
![png](T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_files/T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_52_0.png)
    


Note agora que as quedas em torno de 2008 e 2020 estão muito mais aparentes!

#### Como as quedas em 2008 e 2020 afetaram o total bruto de bilheteria doméstica?


```python
movies_by_year[movies_by_year.index >= 2000].plot(kind = 'line', y = 'Total Gross in Billions');
```


    
![png](T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_files/T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_55_0.png)
    


#### Curiosidade: qual foi o filme de maior bilheteria de 2016? 🐟


```python
movies_by_year[movies_by_year.index == 2016]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Gross in Billions</th>
      <th>Number of Movies</th>
      <th>#1 Movie</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2016</th>
      <td>11.38</td>
      <td>855</td>
      <td>Finding Dory</td>
    </tr>
  </tbody>
</table>
</div>



## Gráficos de barras 📊

### Exemplo: [200 músicas mais tocadas no Spotify dos EUA](https://spotifycharts.com/regional) (21/01/23)


```python
charts = (bpd.read_csv('data/regional-us-daily-2023-01-21.csv')
          .set_index('rank')
          .get(['track_name', 'artist_names', 'streams', 'uri'])
         )
charts
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_name</th>
      <th>artist_names</th>
      <th>streams</th>
      <th>uri</th>
    </tr>
    <tr>
      <th>rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Flowers</td>
      <td>Miley Cyrus</td>
      <td>3356361</td>
      <td>spotify:track:0yLdNVWF3Srea0uzk55zFn</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kill Bill</td>
      <td>SZA</td>
      <td>2479445</td>
      <td>spotify:track:1Qrg8KqiBpW07V7PNxwwwL</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Creepin' (with The Weeknd &amp; 21 Savage)</td>
      <td>Metro Boomin, The Weeknd, 21 Savage</td>
      <td>1337320</td>
      <td>spotify:track:2dHHgzDwk4BJdRwy9uXhTO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Superhero (Heroes &amp; Villains) [with Future &amp; C...</td>
      <td>Metro Boomin, Future, Chris Brown</td>
      <td>1235285</td>
      <td>spotify:track:0vjeOZ3Ft5jvAi9SBFJm1j</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Rich Flex</td>
      <td>Drake, 21 Savage</td>
      <td>1109704</td>
      <td>spotify:track:1bDbXMyjaUIooNwFE9wn0N</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>196</th>
      <td>Burn, Burn, Burn</td>
      <td>Zach Bryan</td>
      <td>267772</td>
      <td>spotify:track:5jfhLCSIFUO4ndzNRh4w4G</td>
    </tr>
    <tr>
      <th>197</th>
      <td>LET GO</td>
      <td>Central Cee</td>
      <td>267401</td>
      <td>spotify:track:3zkyus0njMCL6phZmNNEeN</td>
    </tr>
    <tr>
      <th>198</th>
      <td>Major Distribution</td>
      <td>Drake, 21 Savage</td>
      <td>266986</td>
      <td>spotify:track:46s57QULU02Voy0Kup6UEb</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Sun to Me</td>
      <td>Zach Bryan</td>
      <td>266968</td>
      <td>spotify:track:1SjsVdSXpwm1kTdYEHoPIT</td>
    </tr>
    <tr>
      <th>200</th>
      <td>The Real Slim Shady</td>
      <td>Eminem</td>
      <td>266698</td>
      <td>spotify:track:3yfqSUWxFvZELEM4PmlwIR</td>
    </tr>
  </tbody>
</table>
<p>200 rows × 4 columns</p>
</div>



### Motivação

Quantos streams as 10 músicas mais populares têm?


```python
charts
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_name</th>
      <th>artist_names</th>
      <th>streams</th>
      <th>uri</th>
    </tr>
    <tr>
      <th>rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Flowers</td>
      <td>Miley Cyrus</td>
      <td>3356361</td>
      <td>spotify:track:0yLdNVWF3Srea0uzk55zFn</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kill Bill</td>
      <td>SZA</td>
      <td>2479445</td>
      <td>spotify:track:1Qrg8KqiBpW07V7PNxwwwL</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Creepin' (with The Weeknd &amp; 21 Savage)</td>
      <td>Metro Boomin, The Weeknd, 21 Savage</td>
      <td>1337320</td>
      <td>spotify:track:2dHHgzDwk4BJdRwy9uXhTO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Superhero (Heroes &amp; Villains) [with Future &amp; C...</td>
      <td>Metro Boomin, Future, Chris Brown</td>
      <td>1235285</td>
      <td>spotify:track:0vjeOZ3Ft5jvAi9SBFJm1j</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Rich Flex</td>
      <td>Drake, 21 Savage</td>
      <td>1109704</td>
      <td>spotify:track:1bDbXMyjaUIooNwFE9wn0N</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>196</th>
      <td>Burn, Burn, Burn</td>
      <td>Zach Bryan</td>
      <td>267772</td>
      <td>spotify:track:5jfhLCSIFUO4ndzNRh4w4G</td>
    </tr>
    <tr>
      <th>197</th>
      <td>LET GO</td>
      <td>Central Cee</td>
      <td>267401</td>
      <td>spotify:track:3zkyus0njMCL6phZmNNEeN</td>
    </tr>
    <tr>
      <th>198</th>
      <td>Major Distribution</td>
      <td>Drake, 21 Savage</td>
      <td>266986</td>
      <td>spotify:track:46s57QULU02Voy0Kup6UEb</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Sun to Me</td>
      <td>Zach Bryan</td>
      <td>266968</td>
      <td>spotify:track:1SjsVdSXpwm1kTdYEHoPIT</td>
    </tr>
    <tr>
      <th>200</th>
      <td>The Real Slim Shady</td>
      <td>Eminem</td>
      <td>266698</td>
      <td>spotify:track:3yfqSUWxFvZELEM4PmlwIR</td>
    </tr>
  </tbody>
</table>
<p>200 rows × 4 columns</p>
</div>




```python
charts.take(np.arange(10))
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_name</th>
      <th>artist_names</th>
      <th>streams</th>
      <th>uri</th>
    </tr>
    <tr>
      <th>rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Flowers</td>
      <td>Miley Cyrus</td>
      <td>3356361</td>
      <td>spotify:track:0yLdNVWF3Srea0uzk55zFn</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kill Bill</td>
      <td>SZA</td>
      <td>2479445</td>
      <td>spotify:track:1Qrg8KqiBpW07V7PNxwwwL</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Creepin' (with The Weeknd &amp; 21 Savage)</td>
      <td>Metro Boomin, The Weeknd, 21 Savage</td>
      <td>1337320</td>
      <td>spotify:track:2dHHgzDwk4BJdRwy9uXhTO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Superhero (Heroes &amp; Villains) [with Future &amp; C...</td>
      <td>Metro Boomin, Future, Chris Brown</td>
      <td>1235285</td>
      <td>spotify:track:0vjeOZ3Ft5jvAi9SBFJm1j</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Rich Flex</td>
      <td>Drake, 21 Savage</td>
      <td>1109704</td>
      <td>spotify:track:1bDbXMyjaUIooNwFE9wn0N</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Shakira: Bzrp Music Sessions, Vol. 53</td>
      <td>Bizarrap, Shakira</td>
      <td>1051226</td>
      <td>spotify:track:4nrPB8O7Y7wsOCJdgXkthe</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Just Wanna Rock</td>
      <td>Lil Uzi Vert</td>
      <td>998684</td>
      <td>spotify:track:4FyesJzVpA39hbYvcseO2d</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Anti-Hero</td>
      <td>Taylor Swift</td>
      <td>936166</td>
      <td>spotify:track:0V3wPSX9ygBnCm8psDIegu</td>
    </tr>
    <tr>
      <th>9</th>
      <td>golden hour</td>
      <td>JVKE</td>
      <td>870031</td>
      <td>spotify:track:5odlY52u43F5BjByhxg7wg</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Unholy (feat. Kim Petras)</td>
      <td>Sam Smith, Kim Petras</td>
      <td>859271</td>
      <td>spotify:track:3nqQXoyQOWXiESFLlDF1hG</td>
    </tr>
  </tbody>
</table>
</div>




```python
charts.take(np.arange(10)).plot(kind = 'barh', x = 'track_name', y = 'streams');
```


    
![png](T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_files/T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_64_0.png)
    


### Gráficos de barra

- Os gráficos de barras nos permitem visualizar a relação entre uma variável categórica e uma variável numérica.

- Para criar um gráfico de barras a partir de um DataFrame `df` genérico com uma coluna categórica `'categorical_column_name'` e uma coluna numérica `'numerical_column_name'`, invocamos

````python
df.plot(
    kind = 'barh', 
    x = categorical_column_name, 
    y = numerical_column_name
)
````

- O **"h"** em `'barh'` significa **"horizontal"**.
- Tipicamente, é mais fácil ler os rótulos quando o gráfico de barras é organizado de maneira horizontal.
- No gráfico anterior, definimos `y = 'Streams'`, ainda que os streams sejam medidos pelo comprimento do eixo $x$.
    - Isso ocorre porque em um gráfico de barras, _canonicamente_, a variável categórica está no eixo $x$ e a numérica no eixo $y$ – a opção `'barh'` apenas muda a "orientação" do gráfico de maneira a produzir uma visualização melhor (mais sobre isso abaixo). 


```python
# As barras no gráfico abaixo aparecem na ordem "oposta" à que aparecem no DataFrame.
(charts
 .take(np.arange(10))
 .sort_values(by = 'streams')
 .plot(kind = 'barh', x = 'track_name', y = 'streams')
);
```


    
![png](T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_files/T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_68_0.png)
    


- Embora em geral na maior parte dos casos consigamos escolher parâmetros que nos ajudem a visualizar melhor nosso dados, a _espessura_ e o _espaçamento_ das barras em um gráfico de barras são _arbitrários_.
- Da mesma forma, a _ordem dos rótulos_ categóricos também é arbitrária.

#### Quantas músicas os 15 melhores artistas têm entre as 200 mais tocadas?

Para responder essa pergunta, primeiro vamos criar um DataFrame com uma única coluna que descreve o número de músicas entre as 200 melhores por artista.

Faremos isso utilizando o `.groupby` com `.size()`, agrupando por `'artist_names'`:


```python
charts
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_name</th>
      <th>artist_names</th>
      <th>streams</th>
      <th>uri</th>
    </tr>
    <tr>
      <th>rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Flowers</td>
      <td>Miley Cyrus</td>
      <td>3356361</td>
      <td>spotify:track:0yLdNVWF3Srea0uzk55zFn</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kill Bill</td>
      <td>SZA</td>
      <td>2479445</td>
      <td>spotify:track:1Qrg8KqiBpW07V7PNxwwwL</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Creepin' (with The Weeknd &amp; 21 Savage)</td>
      <td>Metro Boomin, The Weeknd, 21 Savage</td>
      <td>1337320</td>
      <td>spotify:track:2dHHgzDwk4BJdRwy9uXhTO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Superhero (Heroes &amp; Villains) [with Future &amp; C...</td>
      <td>Metro Boomin, Future, Chris Brown</td>
      <td>1235285</td>
      <td>spotify:track:0vjeOZ3Ft5jvAi9SBFJm1j</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Rich Flex</td>
      <td>Drake, 21 Savage</td>
      <td>1109704</td>
      <td>spotify:track:1bDbXMyjaUIooNwFE9wn0N</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>196</th>
      <td>Burn, Burn, Burn</td>
      <td>Zach Bryan</td>
      <td>267772</td>
      <td>spotify:track:5jfhLCSIFUO4ndzNRh4w4G</td>
    </tr>
    <tr>
      <th>197</th>
      <td>LET GO</td>
      <td>Central Cee</td>
      <td>267401</td>
      <td>spotify:track:3zkyus0njMCL6phZmNNEeN</td>
    </tr>
    <tr>
      <th>198</th>
      <td>Major Distribution</td>
      <td>Drake, 21 Savage</td>
      <td>266986</td>
      <td>spotify:track:46s57QULU02Voy0Kup6UEb</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Sun to Me</td>
      <td>Zach Bryan</td>
      <td>266968</td>
      <td>spotify:track:1SjsVdSXpwm1kTdYEHoPIT</td>
    </tr>
    <tr>
      <th>200</th>
      <td>The Real Slim Shady</td>
      <td>Eminem</td>
      <td>266698</td>
      <td>spotify:track:3yfqSUWxFvZELEM4PmlwIR</td>
    </tr>
  </tbody>
</table>
<p>200 rows × 4 columns</p>
</div>




```python
songs_per_artist = charts.groupby('artist_names').size()
songs_per_artist
```




    artist_names
    21 Savage, Metro Boomin    1
    80purppp                   1
    A Boogie Wit da Hoodie     1
    Arctic Monkeys             2
    Arcángel, Bad Bunny        1
                              ..
    XXXTENTACION               1
    Yeat                       1
    Zach Bryan                 4
    d4vd                       2
    Ñengo Flow, Bad Bunny      1
    Length: 145, dtype: int64



Agora, utilizando `.sort_values` e `.take`, manteremos apenas os 15 melhores artistas:


```python
top_15_artists = (songs_per_artist
                  .sort_values(ascending = False)
                  .take(np.arange(15)))
top_15_artists
```




    artist_names
    SZA                 11
    Taylor Swift         8
    Morgan Wallen        6
    Drake, 21 Savage     5
    Zach Bryan           4
                        ..
    Joji                 2
    Eminem               2
    Kanye West           2
    Childish Gambino     2
    NewJeans             2
    Length: 15, dtype: int64



Antes de invocar `.plot(kind = 'barh', y = 'count')`, ordenaremos `top_15_artists` em ordem **crescente**.

Devemos fazer isso porque o Python _inverte_ a ordem das linhas ao criar barras em gráficos de barras horizontais.


```python
top_15_artists.sort_values().plot(kind = 'barh', y = 'count');
```


    
![png](T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_files/T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_79_0.png)
    


Note que no comando acima, omitimos a opção `x = 'artist_names'` sem nenhum problema porque como `top_15_artists` é uma `Series` e que já está indexada, o método `.plot` subentende que `x` é o seu índice. 


```python
# Descomente e execute.
# top_15_artists.sort_values().plot(kind = 'barh', x = 'artist_names', y = 'count');
```

### Gráficos de barras verticais

- Para criar um gráfico de barras verticais, utilizamos `kind = 'bar'` ao invés de `kind = 'barh'`.

No nosso exemplo:


```python
top_15_artists.plot(kind = 'bar', y = 'count');
```


    
![png](T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_files/T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_84_0.png)
    


- Aqui fica clara a razão do Python tomar a variável categórica como a variável correspondente ao eixo $x$, e a variável numérica como a variável correspondente ao eixo $y$.
- Ainda sobre esse ponto, reforçamos aqui a ideia de que `kind = 'barh'` apenas muda a orientação do tipo "canônico", que é `kind = 'bar'`.

#### Quantas vezes as músicas do The Weeknd foram tocadas?


```python
(charts
 [charts.get('artist_names') == 'The Weeknd']
 .sort_values('streams')
 .plot(kind='barh', x='track_name', y='streams')
);
```


    
![png](T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_files/T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_87_0.png)
    


Parece que não estamos incluindo todas as músicas do The Weeknd aqui...

E como resolvemos esse problema? 🤔

Resposta: Usando `.str.contains`!


```python
weeknd = charts[charts.get('artist_names').str.contains('The Weeknd')]
weeknd
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_name</th>
      <th>artist_names</th>
      <th>streams</th>
      <th>uri</th>
    </tr>
    <tr>
      <th>rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Creepin' (with The Weeknd &amp; 21 Savage)</td>
      <td>Metro Boomin, The Weeknd, 21 Savage</td>
      <td>1337320</td>
      <td>spotify:track:2dHHgzDwk4BJdRwy9uXhTO</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Die For You</td>
      <td>The Weeknd</td>
      <td>794924</td>
      <td>spotify:track:2LBqCSwhJGcFQeTHMVGwy3</td>
    </tr>
    <tr>
      <th>76</th>
      <td>Stargirl Interlude</td>
      <td>The Weeknd, Lana Del Rey</td>
      <td>372624</td>
      <td>spotify:track:5gDWsRxpJ2lZAffh5p7K0w</td>
    </tr>
    <tr>
      <th>78</th>
      <td>Starboy</td>
      <td>The Weeknd, Daft Punk</td>
      <td>361999</td>
      <td>spotify:track:7MXVkk9YMctZqd1Srtv4MB</td>
    </tr>
    <tr>
      <th>102</th>
      <td>The Hills</td>
      <td>The Weeknd</td>
      <td>334354</td>
      <td>spotify:track:7fBv7CLKzipRk6EC6TWHOB</td>
    </tr>
    <tr>
      <th>110</th>
      <td>I Was Never There</td>
      <td>The Weeknd, Gesaffelstein</td>
      <td>328724</td>
      <td>spotify:track:1cKHdTo9u0ZymJdPGSh6nq</td>
    </tr>
    <tr>
      <th>128</th>
      <td>Blinding Lights</td>
      <td>The Weeknd</td>
      <td>311176</td>
      <td>spotify:track:0VjIjW4GlUZAMYd2vXMi3b</td>
    </tr>
    <tr>
      <th>168</th>
      <td>Call Out My Name</td>
      <td>The Weeknd</td>
      <td>281141</td>
      <td>spotify:track:09mEdoA6zrmBPgTEN5qXmN</td>
    </tr>
  </tbody>
</table>
</div>




```python
weeknd.sort_values('streams').plot(kind='barh', x='track_name', y='streams');
```


    
![png](T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_files/T%C3%B3pico%2005%20%E2%80%93%20Visualiza%C3%A7%C3%B5es_92_0.png)
    


- As comparações do tipo `charts.get('artist_names') == 'The Weeknd'` filtram apenas pelas músicas cujo artista é **exatamente** `'The Weekend'`.
- Nos casos acima em que esse artista fez algum tipo de colaboração, isso não foi detectado!
- Utilizando o método `.str.contains` em `charts.get('artist_names').str.contains('The Weeknd')`, podemos captar tanto as músicas autoradas _apenas_ por `'The Weekend'`, mas também as que ele fez algum tipo de participação, isto é, autoradas _não somente_ por ele.

#### Uma demonstração interessante 🎵


```python
# Execute essa célula, mas por enquanto não se preocupe com o que ela faz.
def show_spotify(uri):
    code = uri[uri.rfind(':')+1:]
    src = f"https://open.spotify.com/embed/track/{code}"
    width = 400
    height = 75
    display(IFrame(src, width, height))
```

- Vamos encontrar o URI (_Unique Resource Identifier_) de uma música que nos interessa!


```python
charts
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_name</th>
      <th>artist_names</th>
      <th>streams</th>
      <th>uri</th>
    </tr>
    <tr>
      <th>rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Flowers</td>
      <td>Miley Cyrus</td>
      <td>3356361</td>
      <td>spotify:track:0yLdNVWF3Srea0uzk55zFn</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kill Bill</td>
      <td>SZA</td>
      <td>2479445</td>
      <td>spotify:track:1Qrg8KqiBpW07V7PNxwwwL</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Creepin' (with The Weeknd &amp; 21 Savage)</td>
      <td>Metro Boomin, The Weeknd, 21 Savage</td>
      <td>1337320</td>
      <td>spotify:track:2dHHgzDwk4BJdRwy9uXhTO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Superhero (Heroes &amp; Villains) [with Future &amp; C...</td>
      <td>Metro Boomin, Future, Chris Brown</td>
      <td>1235285</td>
      <td>spotify:track:0vjeOZ3Ft5jvAi9SBFJm1j</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Rich Flex</td>
      <td>Drake, 21 Savage</td>
      <td>1109704</td>
      <td>spotify:track:1bDbXMyjaUIooNwFE9wn0N</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>196</th>
      <td>Burn, Burn, Burn</td>
      <td>Zach Bryan</td>
      <td>267772</td>
      <td>spotify:track:5jfhLCSIFUO4ndzNRh4w4G</td>
    </tr>
    <tr>
      <th>197</th>
      <td>LET GO</td>
      <td>Central Cee</td>
      <td>267401</td>
      <td>spotify:track:3zkyus0njMCL6phZmNNEeN</td>
    </tr>
    <tr>
      <th>198</th>
      <td>Major Distribution</td>
      <td>Drake, 21 Savage</td>
      <td>266986</td>
      <td>spotify:track:46s57QULU02Voy0Kup6UEb</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Sun to Me</td>
      <td>Zach Bryan</td>
      <td>266968</td>
      <td>spotify:track:1SjsVdSXpwm1kTdYEHoPIT</td>
    </tr>
    <tr>
      <th>200</th>
      <td>The Real Slim Shady</td>
      <td>Eminem</td>
      <td>266698</td>
      <td>spotify:track:3yfqSUWxFvZELEM4PmlwIR</td>
    </tr>
  </tbody>
</table>
<p>200 rows × 4 columns</p>
</div>




```python
favorite_song = 'Blinding Lights'
```


```python
song_uri = (charts
            [charts.get('track_name') == favorite_song]
            .get('uri')
            .iloc[0])
song_uri
```




    'spotify:track:0VjIjW4GlUZAMYd2vXMi3b'



Agora, veja o que acontece! 🎶


```python
show_spotify(song_uri)
```



<iframe
    width="400"
    height="75"
    src="https://open.spotify.com/embed/track/0VjIjW4GlUZAMYd2vXMi3b"
    frameborder="0"
    allowfullscreen

></iframe>



## Visualizações "ruins"

- Conforme mencionado anteriormente, as visualizações nos permitem identificar facilmente tendências e comunicar nossos resultados de maneira mais informativa a outras pessoas.
- Porém, algumas visualizações podem tornar os padrões nos dados _mais difíceis_ de ver!
- Os elementos adicionais (e na maioria das vezes desnecessários) que dificultam visualizações são popularmente conhecidos como ["chart junk"](https://eagereyes.org/criticism/chart-junk-considered-useful-after-all).

Além do chart junk, algumas manipulações clássicas dos gráficos incluem distorções dos eixos/unidades, inclusão de elementos de comparação relativa com tamanhos incorretos, etc. 

Seguem abaixo alguns exemplos de visualizações "ruins":

<left>
    <img src = "images/usefuljunk-monster.jpg"; width = 50%>
</left>    

<left>
    <img src = "images/average_height.png"; width = 50%>
</left>

<left>
    <img src = "images/bananas.png"; width = 50%>
</left>

<left>
    <img src = "images/weather.png"; width = 50%>
</left>

## Resumo

- As visualizações facilitam a extração de padrões de conjuntos de dados, e a comunicar esses padrões de maneira clara e intuitiva.
- Existem dois tipos principais de variáveis: **categóricas** e **numéricas**.
- Os tipos de variáveis ​​que estamos visualizando usualmente informam nossa escolha de qual tipo de visualização usar.
- Nesse tópico, introduzimos os **gráficos de dispersão**, **gráficos de linhas** e os **gráficos de barras**.
