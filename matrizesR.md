Matrizes
================
*Marcel Ferreira (@marceelrf)*
27/03/2019

Definindo matrizes
------------------

Matrizes são objetos complexos que reúnem uma coleção de dados organizados de modo bidimensional. Em R matrizes só aceitam uma classe de dados (igual aos vetores), então fique atento. A matriz m1 por exemplo é composta dos números de 1 a 9 organizados em 3 linhas e 3 colunas.

``` r
m1 <- matrix(c(1,2,3,4,5,6,7,8,9), # Componentes da Matriz
             nrow = 3, # número de linhas
             ncol = 3, # número de colunas
             byrow = TRUE # preencher por linhas
)

m1 # imprimi a matriz m1
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    2    3
    ## [2,]    4    5    6
    ## [3,]    7    8    9

Para defirnir uma matriz em R utilizamos a função *matrix()*. Esta conta com três argumentos principais **Componetes** (escritos na forma de um vetor), **nrow** (número de linhas) e **ncol** (número de colunas). **byrow** é um argumento opicional, porém impacta na construção da matriz de modo importante.

``` r
m2 <- matrix(c(1,2,3,4,5,6,7,8,9), # Componentes da Matriz
             nrow = 3, 
             ncol = 3, 
             byrow = FALSE # preencher por linhas - FALSO!
)

m2 # imprimi a matriz m1
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    4    7
    ## [2,]    2    5    8
    ## [3,]    3    6    9

Ao alterarmos para ***FALSE***, o R começa a montar a matriz pelas colunas e não pelas linhas (Parmetro padrão). E com isso a matriz é completamente alterada.

Acessando os componentes de uma matriz
--------------------------------------

Igual aos vetores, é possível acessar cada componente de uma matriz. Para isso utilizamos a notação *\[i,j\]*, onde *i* é o número da linha e *j* o número da coluna.

``` r
m1[1,2] # Acessa o componente da linha 1 e coluna 2
```

    ## [1] 2

``` r
m1[3,1] # Acessa o componente da linha 3 e coluna 1
```

    ## [1] 7

É possível também acessar uma determinada linha ou coluna. Para isto basta escolher o *i* ou *j*.

``` r
m1[1,] # Acessa a primeira linha inteira
```

    ## [1] 1 2 3

``` r
m1[,3] # Acessa a terceira coluna inteira
```

    ## [1] 3 6 9

Os operadores *:* e *c()* também pode ser utilizado para acessar subconjuntos dentro da matriz.

``` r
m1[1:2,3] # Acessa a primeira e segunda linha da terceira coluna
```

    ## [1] 3 6

``` r
m1[2,2:3] # Acessa a segunda linha da segunda e terceira coluna
```

    ## [1] 5 6

``` r
m1[c(1,3),c(1,3)] # Acessa os componentes [1,1],[1,3],[3,1] e [3,3]
```

    ##      [,1] [,2]
    ## [1,]    1    3
    ## [2,]    7    9

Operações algébricas com matrizes
---------------------------------

Caso multipliquemos uma matriz por um número todos seus componentes serão multiplicados por este. O mesmo ocorre para as demais operações matemáticas.

``` r
m1 + 3
```

    ##      [,1] [,2] [,3]
    ## [1,]    4    5    6
    ## [2,]    7    8    9
    ## [3,]   10   11   12

``` r
m2 * 3
```

    ##      [,1] [,2] [,3]
    ## [1,]    3   12   21
    ## [2,]    6   15   24
    ## [3,]    9   18   27

``` r
m1 /5
```

    ##      [,1] [,2] [,3]
    ## [1,]  0.2  0.4  0.6
    ## [2,]  0.8  1.0  1.2
    ## [3,]  1.4  1.6  1.8

``` r
log(m2)
```

    ##           [,1]     [,2]     [,3]
    ## [1,] 0.0000000 1.386294 1.945910
    ## [2,] 0.6931472 1.609438 2.079442
    ## [3,] 1.0986123 1.791759 2.197225

A para somarmos duas matrizes é só utilizamos *+*. A operação é realizado componente a componente, então é importante verificarmos se as ***matrizes possuem a mesma dimensão***. O mesmo ocorre com a subtração

``` r
m1 + m2
```

    ##      [,1] [,2] [,3]
    ## [1,]    2    6   10
    ## [2,]    6   10   14
    ## [3,]   10   14   18

``` r
m1 - m2
```

    ##      [,1] [,2] [,3]
    ## [1,]    0   -2   -4
    ## [2,]    2    0   -2
    ## [3,]    4    2    0

Agora caso você deseje multiplicar duas matrizes você deve utilizar \_%\*%\_ ao invés de \_\*\_.

``` r
m1 %*% m2 # realiza a multiplicação de matrizes
```

    ##      [,1] [,2] [,3]
    ## [1,]   14   32   50
    ## [2,]   32   77  122
    ## [3,]   50  122  194

``` r
m1 * m2 # realiza a multiplicação componente a componente
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    8   21
    ## [2,]    8   25   48
    ## [3,]   21   48   81

Em R é possível realizar divisão de componente a componente entre duas matrizes.

``` r
m1/m2
```

    ##          [,1]     [,2]      [,3]
    ## [1,] 1.000000 0.500000 0.4285714
    ## [2,] 2.000000 1.000000 0.7500000
    ## [3,] 2.333333 1.333333 1.0000000

Combinando matrizes
-------------------

Caso você deseje combinar duas matrizes podemos utilizar as funções *rbind()* e *cbind()*.

``` r
rbind(m1,m2) # Combina as matrizes m1 e m2 pelas linhas
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    2    3
    ## [2,]    4    5    6
    ## [3,]    7    8    9
    ## [4,]    1    4    7
    ## [5,]    2    5    8
    ## [6,]    3    6    9

``` r
cbind(m1,m2) # Combina as matrizes m1 e m2 pelas colunas
```

    ##      [,1] [,2] [,3] [,4] [,5] [,6]
    ## [1,]    1    2    3    1    4    7
    ## [2,]    4    5    6    2    5    8
    ## [3,]    7    8    9    3    6    9

Funções úteis ao se trabalhar com matrizes
------------------------------------------

-   *dim()*

Retorna as dimensões de uma matriz

``` r
dim(m1)
```

    ## [1] 3 3

-   *nrow()* e *ncol()*

Retornam o número de linhas ou colunas.

``` r
ncol(m2) # número de colunas
```

    ## [1] 3

``` r
nrow(m1) # número de linhas
```

    ## [1] 3

-   *length()*

Retorna o número de componentes da matriz (similar ao seu uso com vetores)

``` r
length(m1)
```

    ## [1] 9

``` r
length(m2)
```

    ## [1] 9

-   *t()*

Realiza a transposição da matriz

``` r
t(m1)
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    4    7
    ## [2,]    2    5    8
    ## [3,]    3    6    9

-   Funções estatísticas: *mean()*, *median()*, *sd()*, *max()* e *min()*

Realizam o calculo considerando todos os componentes da matriz

``` r
mean(m1) # média
```

    ## [1] 5

``` r
median(m1) #mediana
```

    ## [1] 5

``` r
sd(m2) # desvio padrão
```

    ## [1] 2.738613

``` r
max(m2) # máximo
```

    ## [1] 9

``` r
min(m1) #mínimo
```

    ## [1] 1

A função *summary()* pode ser utilizada com matrizes também, porém cuidado. Ela realiza sua operação coluna a coluna.

``` r
summary(m1)
```

    ##        V1            V2            V3     
    ##  Min.   :1.0   Min.   :2.0   Min.   :3.0  
    ##  1st Qu.:2.5   1st Qu.:3.5   1st Qu.:4.5  
    ##  Median :4.0   Median :5.0   Median :6.0  
    ##  Mean   :4.0   Mean   :5.0   Mean   :6.0  
    ##  3rd Qu.:5.5   3rd Qu.:6.5   3rd Qu.:7.5  
    ##  Max.   :7.0   Max.   :8.0   Max.   :9.0

Existem diversas outras funções muito úteis para se trabalhar com matrizes. Mais adiante iremos observa-las com atenção. Por hora é isso.

**Um forte abraço!** [Twitter](www.twitter.com/marceelrf) [Instagram](www.instagram.com/marceelrf) [LinkedIn](https://www.linkedin.com/in/marcel-rodrigues-ferreira-435b7b13b/)
