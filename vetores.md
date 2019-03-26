Vetores
================
*Marcel Ferreira (@marceelrf)*
25/03/2019

Definição
---------

Em R, vetores são estruturas compostas por um **sequência** de dados, onde cada elemento do vetor é conhecido por **componente**. Com um detalhe importante: **Vetores só aceitam componentes do mesmo tipo de dado**. Para definirmos um vetor no R utilizamos o comando *c()*. O *c* vem da palavra concatenar.

Ex:

``` r
v1 <- c(1,4,5,6) # define um vetor numérico com 4 componentes.
v1
```

    ## [1] 1 4 5 6

``` r
v2 <- c("marcel","rodrigues","ferreira") # define um vetor de caracteres com 3 componentes.
v2
```

    ## [1] "marcel"    "rodrigues" "ferreira"

``` r
v3 <- c(TRUE, TRUE,FALSE,F,T) # # define um vetor lógico com 5 componentes.
v3
```

    ## [1]  TRUE  TRUE FALSE FALSE  TRUE

Acessando os componters de um vetor
-----------------------------------

Ao trabalhar com vetores é muito comum precisarmos obter informações sobre um determinado componente ou um grupo de um componentes de um determinado vetor. **Lembre-se que em muitos casos vetores podem ter centenas a milhares de componentes!**. Para acessar o valor de um componente desejado utilizamos *\[\]* após o nome do vetor. Po exemplo, caso desejemos o 2 componente de v2:

``` r
v2[2]
```

    ## [1] "rodrigues"

Agora se for do desejo obtermos um subconjunto de um determinado vetor podemos fazer de dois modos distintos. O geral é utilizar o comando *c()* dentro do colchete:

``` r
v2[c(1,3)] # acessa o primeiro e o terceiro componente de v2.
```

    ## [1] "marcel"   "ferreira"

``` r
v1[(c(2,3))] # acessa o segundo e o terceiro componente de v1.
```

    ## [1] 4 5

Agora em caso de componentes seguidos, como o caso do segundo exemplo, podemos utilizar *:* dentro de *\[\]*:

``` r
v1[2:3] # acessa o segundo e o terceiro componente de v1.
```

    ## [1] 4 5

``` r
v3[1:4] # acessa os quatro primeiros componentes de v3
```

    ## [1]  TRUE  TRUE FALSE FALSE

Concatenando vetores
--------------------

Você pode utilizar o comando *c()* para concatenar diferentes vetores (ou subconjuntos deles). Agora preste atenção, **caso os vetores sejam de tipos de dados distintos o R vai converter os dados para torna-los de um tipo somente!**

A ordem de dominância é a sequinte:

**Character &gt; Complex &gt; Numeric &gt; Integer &gt; Logical**

``` r
v4 <- c(33,2,1,67) # novo vetor numérico
v4
```

    ## [1] 33  2  1 67

``` r
v5 <- c(v1,v4) # retorna um vetor numérico
v5
```

    ## [1]  1  4  5  6 33  2  1 67

``` r
v6 <- c(v1,v2) # retorna um vetor "coagido" em caractere
class(v6)
```

    ## [1] "character"

Contas com vetores
------------------

Ao executarmos calculos com vetores numéricos o procedimento é realizado componente a componente. Por exemplo, se adicionarmos 1 a v1, todos os componentes serão adicionados em 1.

``` r
v1 + 1
```

    ## [1] 2 5 6 7

O mesmo vale para multiplicação/divisão.

``` r
v1 * 4
```

    ## [1]  4 16 20 24

``` r
v1/2
```

    ## [1] 0.5 2.0 2.5 3.0

Ao somarmos dois vetores as contas são feitas componente a componente.

``` r
v1 + v4 #vetores de comprimento igual
```

    ## [1] 34  6  6 73

Agora é importante prestar atenção ao comprimento dos vetores, pois uma vez que estes não tenham o mesmo número de elementos o R irá "reiniciar" a contagem de elementos do menor até "preencher" o maior.

``` r
v1 + v5 # v1 contém 4 componentes e v5 8 componentes
```

    ## [1]  2  8 10 12 34  6  6 73

Perceba que o R realizou a sequinte operação:

``` r
v1 + v5[1:4] # v1 + os 4 primeiros componentes de v5
```

    ## [1]  2  8 10 12

``` r
v1 + v5[5:8] # v1 + os 4 últimos componentes de v5
```

    ## [1] 34  6  6 73

``` r
c(v1 + v5[1:4],v1 + v5[5:8]) # concatena as contas acima em um vetor de 8 componentes
```

    ## [1]  2  8 10 12 34  6  6 73

Perceba que o mesmo vale para as diferentes operações, como a multiplicação no exemplo a seguir

``` r
v1 * v5[1:4] # v1 * os 4 primeiros componentes de v5
```

    ## [1]  1 16 25 36

``` r
v1 * v5[5:8] # v1 * os 4 últimos componentes de v5
```

    ## [1]  33   8   5 402

``` r
c(v1 * v5[1:4],v1 * v5[5:8]) # concatena as contas acima em um vetor de 8 componentes
```

    ## [1]   1  16  25  36  33   8   5 402

``` r
v1 * v5
```

    ## [1]   1  16  25  36  33   8   5 402

Funções úteis ao se trabalhar com vetores
-----------------------------------------

No dia-a-dia com o R ao nos deparamos com vetores muitas vezes precisamos de informações rápidas sobre o mesmo. Por exemplo, no exemplo acima vimos que o número de componentes,ou o **comprimento**, diferentes em dois vetores pode geral complicações. Para verificarmos o comprimento de um vetor usamos a função *length()*.

``` r
length(v1) # retorna o comprimento de v1
```

    ## [1] 4

``` r
length(v4)
```

    ## [1] 4

``` r
length(v5)
```

    ## [1] 8

``` r
length(v1) == length(v4) # Teste lógico do comprimento de vetores
```

    ## [1] TRUE

``` r
length(v4) == length(v5)
```

    ## [1] FALSE

Você pode querer informações como qual o maior e o menor valor em um vetor. Para isto as usamos as funções *max()* e *min()*.

``` r
max(v1)
```

    ## [1] 6

``` r
min(v1)
```

    ## [1] 1

Imagine que você deseje parâmetros estatísticos como média, mediana e desvio padrão. As funções *mean()*, *median()* e *sd()* realizam os esses calculos.

``` r
mean(v5) # média de v5
```

    ## [1] 14.875

``` r
median(v5) # mediana de v5
```

    ## [1] 4.5

``` r
sd(v5) # desvio padrão de v5
```

    ## [1] 23.57624

Para caso estatísticos a função *summary()* resume todas estas informações

``` r
summary(v5) # "resumo"sobre v5 
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    1.00    1.75    4.50   14.88   12.75   67.00

Você deve ter reparado que as funções em R possuem normalmente um nome bem direto e em inglês para o comando desejado. Nesta seção analisamos apenas funções para vetores numéricos, mais para frente (quando já tivermos dominado matrizes e data.frames) vou discutir funções úteis para vetores de caracteres. Mas por hora é isso!

Um forte abraço!
