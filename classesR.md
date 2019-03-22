Trabalhando com diferentes classes no R
================
*Marcel Ferreira (@marceelrf)*
22/03/2019

Classes
-------

O R permite que dados sejam de diferentes classes. Cada classe possui propriedades que merecem atenção ao trabalhada. As classes básicas no R são:

-   *numeric*
-   *integer*
-   *complex*
-   *logical*
-   *character*

***numeric***

Permitem qualquer número real e qualquer operação matermática

``` r
4 + 4 #soma
```

    ## [1] 8

``` r
log(4) #log base 10 de 4
```

    ## [1] 1.386294

***integer***

Permitem qualquer número inteiro e qualquer operação matermática. Para forçar o número a ser um *integer* e não *numeric* basta acrescentar "L" ao número.

``` r
4L + 4L #soma
```

    ## [1] 8

``` r
log(4L) #log base 10 de 4
```

    ## [1] 1.386294

``` r
log(4) == log(4L) # teste se o resultado do log de 4 é igual ao de 4L
```

    ## [1] TRUE

``` r
4.5L # perceba que ao colocar o ponto decimal o R vai dar um aviso e tratar como numeric
```

    ## [1] 4.5

***complex***

Formato de número complexo. Pouco utilizado. Permite operações além do conjunto real. Seu formato é:

``` r
2 + 4i # onde i é a parte imaginária
```

    ## [1] 2+4i

``` r
# perceba que i sozinho não é reconhecido pelo R
(2 + 4i) + 3 # soma de um Real ao um complexo
```

    ## [1] 5+4i

``` r
(3 + 5i) + (2 + 1i) # soma de complexos
```

    ## [1] 5+6i

``` r
sqrt(-1) # raíz de números negativos produz NaN (não números)
```

    ## Warning in sqrt(-1): NaNs produzidos

    ## [1] NaN

``` r
sqrt(-1 + 0i) # ao adicionarmos 0i o R reconhece com complexo e realiza a operação
```

    ## [1] 0+1i

***logical***

Formato lógico é composto por *TRUE* ou *T* para verdadeiro e *FALSE* ou *F* para falso. Extremamente utilizado quando trabalhamos com o R nos permitindo fazer comparações através de testes lógicos. Mais adiante veremos como estes teste controlam nosso código.

``` r
3 == 4 
```

    ## [1] FALSE

``` r
T == TRUE
```

    ## [1] TRUE

``` r
F == FALSE
```

    ## [1] TRUE

***character***

É o tipo de dado que nos permite criar Strings ou, de modo geral, textos. Não nos permitem operações matemáticas. São utilizados para nomear colunas e linhas. Para definir um *character* basta colocarmos entre aspas.

``` r
c1 <- "marcel"
c1
```

    ## [1] "marcel"

``` r
# c1 + "ferreira",  Não vai funcionar
```

Estes são as classes de dados básicas do R. Elas são utilizadas para a construção de objetos mais complexos como *vetores*, *matrizes*, *data.frames* e *lista*, mas isso são tópicos a serem explorados mais adiante.

Mãos a obra
-----------

Vamos agora ver como manipular estas classes num exemplo real. Temos que descobrir qual a classe estamos trabalhando e como podemos altera-lá. Para isto vamos usar o objeto *mtcars*, que já vem com o RStudio.

``` r
dim(mtcars) # checa as dimensões do objeto
```

    ## [1] 32 11

``` r
head(mtcars) # visualiza as 6 primeiras linhas do objeto
```

    ##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
    ## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
    ## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
    ## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
    ## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
    ## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
    ## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1

``` r
class(mtcars) # verifica a classe do objeto
```

    ## [1] "data.frame"

Com a função *class()* vimos que o objeto *mtcars* é um data.frame. No R, data.frame são objetos bidimensionais (como um matriz) capaz de armazenar diferentes classes. Mtcars contem 32 anotações (linhas), cada uma representando um carro diferente, para 11 variáveis diferentes (colunas). Num primeiro olhar para os dados presentes em mtcars podemos pensar que todos são numéricos. E de fato eles estão representados como numéricos. Para verificarmos isso podemos usar duas funções *class()* ou *is.numeric()*. Para utilizar essas funções vamos ter que usar o operador "$".

``` r
class(mtcars$mpg) # note que ao digitar o "$" o RStudio já fornece uma lista dos cabeçalhos em mtcars
```

    ## [1] "numeric"

``` r
is.numeric(mtcars$mpg)
```

    ## [1] TRUE

Perceba que embora ambas as funções testem o tipo da variavel, elas o fazem de modos distintos. Class() nos diz qual é a classe o objeto é (neste exemplo, uma coluna de mtcars). Já a função is.numeric() retorna uma resposta lógica TRUE ou FALSE. Aliás, esta função pode ser implementada para qualquer classe! Para isso só digitar "is.*tipodaClasse*". Agora, se você entende de carros (eu admito que não é meu caso) deve ter reparado que a coluna *cyl* contém o número de cilindros que o carro tem. E embora possamos utilizar *cyl* como uma variavel numérica, esta não é a melhor representação. Por que? Repare que não podemos colocar qualquer valor para representar o número de cilindros de um carro. Não existe um carro com 4,6 cilindros. Então para representar este tipo de váriavel utilizamos a classe *factor*. *factor* é uma classe de dados categóricos. Como *mtcars$cyl* contém 3 catergorias representando o número de cilindros nos diferentes carros, devemos transformar de *numeric* para *factor*.

Transformando classes
---------------------

Para transformar um classe usamos a função "as.*nomedaClasse*" (análogo ao "is."). Neste caso *as.factor()*.

``` r
mtcars$cyl <- as.factor(mtcars$cyl)
class(mtcars$cyl) # teste se a transformação deu certo
```

    ## [1] "factor"

``` r
is.factor(mtcars$cyl) # teste lógico se a transformação deu certo
```

    ## [1] TRUE

Perceba que agora ao inspecionarmos o objeto convertido a *factor* vai aparecer *Levels:* indicando os diferentes níveis que a variavel contém.

``` r
mtcars$cyl
```

    ##  [1] 6 6 4 6 8 6 8 4 4 6 6 8 8 8 8 8 8 4 4 4 4 8 8 8 8 4 4 4 8 6 8 4
    ## Levels: 4 6 8

A mesma operação pode ser executada para as colunas *vs*, *am*, *carb* e *gear*.
