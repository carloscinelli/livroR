---
title: 'Introdução a Objetos e à Área de Trabalho'
author: "Carlos Cinelli e Edson Bastos"
date: "15 de Setembro de 2014"
---
Essa frase não vai fazer muito sentido agora, mas é bom você já começar a tê-la em mente: no R, praticamente tudo o que existe na sua área de trabalho é um “objeto”. E praticamente tudo o que acontece na sua área de trabalho é resultado de uma função. 

Nesta seção veremos um pouco sobre o objeto mais básico do R, o vetor, e como gerenciar sua érea de trabalho. Aprenderemos, basicamente, algumas formas de criar e remover um objeto (no caso um vetor), como verificar suas propriedades e alterar seus elementos. Ao final veremos como salvar e carregar sua área de trabalho e/ou objetos específicos.


## Criando objetos: assignment operators
Durante o uso do R, você irá criar e guardar objetos com um nome, por exemplo:


```r
x1 <- 10 # atribui o valor 10 à variável x1
x1
```

```
## [1] 10
```

O operador `<-` é conhecido como "assignment operator" e, no caso acima, atribuiu o valor `10` a um objeto de nome `x1` (no caso, um vetor). Na maior parte das vezes, o operador `=` é equivalente a `<-`. Vejamos:


```r
x2 = 20 # atribui o valor 20 à variável x2
x2 
```

```
## [1] 20
```

Neste livro recomendaremos o uso do `<-` pois ele funciona *sempre* como atribuição. O operador `=` é usado para definir argumentos dentro de um função e, assim, seu comportamento pode ser diferente de uma atribuição em certos casos (veremos isso mais a frente). Contudo, na maior parte das vezes o uso de `=` e `<-` é indiferente, então desde que você seja consistente, escolha a forma que mais lhe agradar.

Estudaremos funções mais a fundo em outra seção, mas, é importante desde já ter a idéia de que o assignment operator `<-` nada mais é do que uma *função*. Para se chamar uma função utiliza-se seu nome seguido dos argumentos entre parênteses, isto é, `funcao(argumento1, argumento2, ...)`.

Dessa forma, poderíamos ter chamado o operado `<-` com a sintaxe de uma função (usando os backticks para auxiliar). Isto é, o comando:


```r
`<-`("x1", 10) 
```
É equivalente a 

```r
x1 <- 10
```
Não se preocupe se você não estiver entendendo tudo agora, mais para frente esses detalhes passarão a fazer mais sentido. 

Além do `=`, outra função que é de certo modo equivalente a `<-` é a função `assign()`, que toma a forma `assign("nomeObjeto", valorObjeto)`. 


```r
# cria a variável x3 com o valor 4
assign("x3", 4) 
x3
```

```
## [1] 4
```

```r
# veja que é equivalente a x3 <- 4
x3 <- 4
x3
```

```
## [1] 4
```

Uma vez que você atribuiu uma variável a um nome, você pode utilizá-la em operações e funções utilizando seu nome.


```r
x1 + x2 + x3 # soma x1,x2,x3
```

```
## [1] 34
```

```r
x1/x2 # divide x1 por x2
```

```
## [1] 0.5
```

```r
x1 * x2 # multiplica x1 por x2
```

```
## [1] 200
```

E você pode guardar os resultados dessas operações em outras variáveis:


```r
y <- x1*x2 + x3 #cria y com o resultado de x1*x2 + x3
y
```

```
## [1] 204
```

## Nomes de variáveis
O R é *case sensitive* - isto é, letras maiúsculas e minúsculas são diferenciadas - portanto `x1` (com x minúsculo) e `X1` (com x maiúsculo) são objetos diferentes.


```r
X1 # O R não vai encontrar, pois não criamos X1 com X maiúsculo.
```

```
## Error in eval(expr, envir, enclos): objeto 'X1' não encontrado
```

```r
x1 # Encontra normalmente
```

```
## [1] 10
```

Os nomes dos objetos no R podem conter combinações arbitrárias de números, textos, bem como ponto ( . ) e *underscore* ( _ ). Entretanto, os nomes **não podem começar com números ou underscore**. 

```r
a1_B2.c15 <- "variável com nome estranho"
a1_B2.c15
```

```
## [1] "variável com nome estranho"
```

```r
_x <- 1 # erro, pois começa com underscore
1var <- 1 # erro, pois começa com número
```
Existem alguns caracteres reservados que também não podem ser utilizados no início dos nomes (como operadores matemáricos +, -,), mas o R é bastante flexível, e todas essas regras podem ser "burladas" se você utilizar backticks ( ` ).


```r
`_x` <- 1 # agora funciona
`+variavel` <- 100 # funciona
`1var` <- 1 #  funciona
```

## Concatenando valores
Até agora construimos vetores com apenas um elemento. Uma das formas de construir um vetor com mais elementos é concatenando uma quantidade arbitrária de objetos com a função `c()`.


```r
x3 <- c(x1, 2, 3, x2) # concatena x1, 2, 3 e x2.
x3 
```

```
## [1] 10  2  3 20
```

```r
x4 <- c("a", "b","c") # concatena "a", "b" e "c"
x4
```

```
## [1] "a" "b" "c"
```

## Classes de vetores
No `R`, a estrutura mais simples de dados é um vetor. Os vetores no R podem ser, entre outros, de classes: *numeric* (números de ponto flutuante), *integer* (número inteiro), *complex* (número complexo), *character* (texto), *logical* (lógicos, booleanos).  Há também datas e fatores, que discutiremos mais a frente.  Os objetos `x1` e `x2`, por exemplo, são vetores numéricos de tamanho 1

Criemos alguns vetores para cada uma dessas classes:


```r
numero <- c(546.90, 10, 789)

# note o L
inteiro <- c(1L, 98L) 

# note o i
complexo <- c(20i, 2+9i) 

# notem as aspas
texto <- c("Um texto de exemplo", "outro texto", "mais texto")

# sempre maiúsculo
logico <- c(TRUE, FALSE, TRUE)
```
Note que inteiros são criados seguidos de um `L` maiúsculo. Números complexos são seguidos de um `i` minúsculo. Textos podem ser criados com aspas duplas (`"texto"`) ou simples (`'texto'`). Vetores lógicos são criados pelas palavras `TRUE` ou `FALSE`, sempre em maiúsculo (e podem ser abreviados para `T` ou `F`, mas não recomendamos).

A função class() é útil para identificar a classe de um determinado objeto. Verifiquemos as classes dos objetos que acabamos de criar:


```r
class(numero)
```

```
## [1] "numeric"
```

```r
class(inteiro)
```

```
## [1] "integer"
```

```r
class(complexo)
```

```
## [1] "complex"
```

```r
class(texto)
```

```
## [1] "character"
```

```r
class(logico)
```

```
## [1] "logical"
```

Você pode testar se um vetor é de determinada classe com as funções `is.xxx` (sendo "xxx" a classe). Por exemplo:


```r
is.numeric(numero)
```

```
## [1] TRUE
```

```r
is.character(numero)
```

```
## [1] FALSE
```

```r
is.character(texto)
```

```
## [1] TRUE
```

```r
is.logical(texto)
```

```
## [1] FALSE
```

E você também pode forçar a conversão de um vetor de uma classe para outra com as funções `as.xxx` (sendo "xxx" a classe). Entretanto, nem sempre essa conversão faz sentido, e pode resultar em erros ou NA's (veremos NA's mais a frente). Por exemplo:



```r
as.character(numero) # Vira texto
```

```
## [1] "546.9" "10"    "789"
```

```r
as.numeric(logico) # TRUE -> 1, FALSE -> 0
```

```
## [1] 1 0 1
```

```r
as.numeric(texto) # Não faz sentido
```

```
## Warning: NAs introduzidos por coerção
```

```
## [1] NA NA NA
```

```r
as.numeric("1012312") # Faz sentido
```

```
## [1] 1012312
```

## Estrutura e tamanho de um objeto
Para ver a e**str**utura de um objeto, use a função `str()`. Esta é uma função simples, mas talvez uma das mais úteis do R. 

Vejamos um exemplo simples, a estrutura do objeto `x3`


```r
str(x3)
```

```
##  num [1:4] 10 2 3 20
```

Note que o resultado de `str()` fornece várias informações: idade trata-se de um vetor numérico (`num`), com 4 elementos (`[1:4]`) e os primeiros elementos do vetor são (`10 2 3 20`).

Se você estiver utilizando o RStudio, um resumo dessa mesma informação já estará aparcendo no seu canto superior direito.

![rstudio_str](https://dl.dropboxusercontent.com/u/44201187/wp/rstudio_str.png)

Teste o resultado de str() em alguns dos outros objetos que criamos e repare nos resultados:


```r
str(x1)
```

```
##  num 10
```

```r
str(x4)
```

```
##  chr [1:3] "a" "b" "c"
```

```r
str(numero)
```

```
##  num [1:3] 547 10 789
```

```r
str(inteiro)
```

```
##  int [1:2] 1 98
```

```r
str(complexo)
```

```
##  cplx [1:2] 0+20i 2+9i
```

```r
str(texto)
```

```
##  chr [1:3] "Um texto de exemplo" "outro texto" "mais texto"
```

```r
str(logico)
```

```
##  logi [1:3] TRUE FALSE TRUE
```

Para obter o tamanho de um objeto, utilize a função `length()`. Note que comandos no R podem ser colocados na mesma linha se separados por ponto-e-vírgula (;).



```r
length(x1)
```

```
## [1] 1
```

```r
length(x3)
```

```
## [1] 4
```

```r
length(x4)
```

```
## [1] 3
```

```r
length(numero); length(inteiro)
```

```
## [1] 3
```

```
## [1] 2
```


## Elementos de um vetor

Você pode acessar elementos de um vetor por meio de colchetes `[ ]` e sua posição.


```r
numero[1] # apenas primeiro elemento do vetor número
```

```
## [1] 546.9
```

```r
numero[c(1,2)] # elementos 1 e 2
```

```
## [1] 546.9  10.0
```

```r
numero[c(1,3)] # elementos 1 e 3
```

```
## [1] 546.9 789.0
```

```r
numero[c(3,1,2)] # troca de posição  
```

```
## [1] 789.0 546.9  10.0
```

Índices negativos podem ser utilizados para selecionar todos os demais elementos de um vetor, exceto aquele que está no índice. Por exemplo:


```r
# seleciona todos os elementos menos o primeiro
numero[-1] 
```

```
## [1]  10 789
```

```r
numero[-c(1,2)] # todos menos 1 e 2
```

```
## [1] 789
```

```r
numero[-c(1,3)] # todos menos 1 e 3
```

```
## [1] 10
```

```r
numero[-3] # todos menos 3
```

```
## [1] 546.9  10.0
```

## Nomes dos elementos
Objetos podem ter seus elementos nomeados.  A função `names()` nos dá os nomes desses elementos:


```r
names(numero)
```

```
## NULL
```

Note que o resultado foi `NULL` pois os elementos do vetor `numero` ainda não foram nomeados. Façamos isso, portanto, utilizando a função `names()<-` 


```r
numero 
```

```
## [1] 546.9  10.0 789.0
```

```r
names(numero) <- c("numero1", "numero2", "numero3")
numero
```

```
## numero1 numero2 numero3 
##   546.9    10.0   789.0
```

Agora, além de acessar o elemento do vetor pela posição, pode-se utilizar seu nome.


```r
# seleciona o elemento de nome "numero1"
numero["numero1"] 
```

```
## numero1 
##   546.9
```

```r
# seleciona o elemento de nome "numero2"
numero["numero2"]
```

```
## numero2 
##      10
```

```r
# seleciona o elemento de nome "numero3"
numero["numero3"]
```

```
## numero3 
##     789
```

```r
# seleciona os elementos de nome "numero1" e "numero3"
numero[c("numero1", "numero3")] 
```

```
## numero1 numero3 
##   546.9   789.0
```

## Alterando elementos
Com o assignment operator e o colchetes, consegue-se alterar apeans alguns elementos específicos de um vetor.

Você pode fazer isso utilizando índices numéricos:

```r
numero
```

```
## numero1 numero2 numero3 
##   546.9    10.0   789.0
```

```r
numero[1] <- 100 # altera elemento 1 para 100
numero
```

```
## numero1 numero2 numero3 
##     100      10     789
```

```r
numero[2:3] <- c(12.3, -10) # altera elementos 2 e 3
numero
```

```
## numero1 numero2 numero3 
##   100.0    12.3   -10.0
```
O que ocorre se você colocar um índice maior do que o tamanho do vetor? O R estende o vetor até o tamanho do índice, e preenche os valores restantes com NA (veremos mais sobre NA a frente):


```r
numero[10] <- 50 # o vetor número não tem 10 elementos...
numero # ao elemento 10 foi atribuido o valor 50 e o restante foi preenchido com NA
```

```
## numero1 numero2 numero3                                                 
##   100.0    12.3   -10.0      NA      NA      NA      NA      NA      NA 
##         
##    50.0
```

Como deletar um elemento de um vetor? Basta usar o índice negativo e sobrescrever o resultado:


```r
logico # 3 elementos
```

```
## [1]  TRUE FALSE  TRUE
```

```r
logico <- logico[-2] # deletamos o segundo elemento
logico
```

```
## [1] TRUE TRUE
```

Você também pode modificar o vetor utilizando os nomes dos elementos:

```r
numero["numero3"] <- 431
numero
```

```
## numero1 numero2 numero3                                                 
##   100.0    12.3   431.0      NA      NA      NA      NA      NA      NA 
##         
##    50.0
```

```r
numero[c("numero1", "numero2")] <- c(-100, 100)
numero
```

```
## numero1 numero2 numero3                                                 
##    -100     100     431      NA      NA      NA      NA      NA      NA 
##         
##      50
```

## Ordenando um vetor
A função `order()` retorna um vetor com as posições para que um objeto fique em ordem crescente. 

```r
order(numero) # indices
```

```
##  [1]  1 10  2  3  4  5  6  7  8  9
```

```r
numero[order(numero)] # ordena numero
```

```
## numero1         numero2 numero3                                         
##    -100      50     100     431      NA      NA      NA      NA      NA 
##         
##      NA
```

A função `sort()` retorna o vetor ordenado.


```r
sort(numero)
```

```
## numero1         numero2 numero3 
##    -100      50     100     431
```
As duas funções tem o parâmetro `decreasing` que, quando `TRUE`, retornam o vetor de em ordem decrescente.


## Encontrando e removendo objetos
Para listar todos os objetos que estão na sua área de trabalho, você pode usar a função `ls()` ou `objects()`.


```r
ls()
```

```
##  [1] "_x"        "+variavel" "1var"      "a1_B2.c15" "complexo" 
##  [6] "inteiro"   "logico"    "numero"    "texto"     "x1"       
## [11] "x2"        "x3"        "x4"        "y"
```

```r
objects()
```

```
##  [1] "_x"        "+variavel" "1var"      "a1_B2.c15" "complexo" 
##  [6] "inteiro"   "logico"    "numero"    "texto"     "x1"       
## [11] "x2"        "x3"        "x4"        "y"
```

Note que apareceram todos os objetos que criamos.

A função `rm(objeto)` remove um objeto da área de trabalho.


```r
rm(x3) # remove o objeto x3 da área de trabalho
x3 # não encontrará o objeto
```

```
## Error in eval(expr, envir, enclos): objeto 'x3' não encontrado
```

```r
ls() # note que x3 não aparecerá na lista de objetos
```

```
##  [1] "_x"        "+variavel" "1var"      "a1_B2.c15" "complexo" 
##  [6] "inteiro"   "logico"    "numero"    "texto"     "x1"       
## [11] "x2"        "x4"        "y"
```

Voltando à função `ls()`, note que o que ela retorna também é um objeto: é um vetor de tipo "texto", ou, como vimos, na terminologia do `R`, do tipo "character". Este resultado pode ser atribuído a um objeto e armazenado na área de trabalho. 


```r
lista_obj <- ls() # guarda o resultado de ls() na variável lista_obj
lista_obj 
```

```
##  [1] "_x"        "+variavel" "1var"      "a1_B2.c15" "complexo" 
##  [6] "inteiro"   "logico"    "numero"    "texto"     "x1"       
## [11] "x2"        "x4"        "y"
```

```r
ls() 
```

```
##  [1] "_x"        "+variavel" "1var"      "a1_B2.c15" "complexo" 
##  [6] "inteiro"   "lista_obj" "logico"    "numero"    "texto"    
## [11] "x1"        "x2"        "x4"        "y"
```

Isto pode ser interessante pois a função `rm()` aceita um parâmetro de texto (`list`) para remover objetos. Por exemplo:


```r
rm(list=lista_obj) # remove todos os objetos que estão na lista_obj
ls() # note que sobrou apenas lista_obj
```

```
## [1] "lista_obj"
```
Desta forma, um atalho para remover todos os objetos da sua área de trabalho é `rm(list = ls())`.

A função `ls()` também aceita um parâmetro (`pattern`) que define um padrão na busca dos objetos no ambiente de trabalho. O `pattern` é bem flexível e inclusive aceita expressões regulares (veremos expressões regulares mais a frente). Por exemplo, o comando `ls(pattern="y")` irá buscar todas as variáveis que contenham "y" no seu nome.

Buscando apenas as variáveis que contenham "y" no nome:


```r
x1 <- 1:10 #  x1 números de 1 a 10
x2 <- c(2, 4,9); y1 <- 50; y2 <- 10 # ; comandos na mesma linha
ls() # lista tudo
```

```
## [1] "lista_obj" "x1"        "x2"        "y1"        "y2"
```

```r
ls(pattern="y") # lista somente y1 e y2
```

```
## [1] "y1" "y2"
```

Combinando este recurso do `ls()` com o `rm()` você pode remover apenas certos objetos. 


```r
rm(list=ls(pattern="y")) #remove todos os objetos que contenham "y".
ls()
```

```
## [1] "lista_obj" "x1"        "x2"
```

## Salvando e carregando objetos
Para salvar uma cópia da sua área de trabalho você pode utilizar a função `save.image()`:


```r
# salva a área de trabalho no arquivo "aula_1.RData"
save.image(file="aula_1.RData") 
```

Agora você pode recuperar todos os objetos com `load()`.


```r
# vamos remover todos os objetos da área de trabalho
rm(list=ls())
ls() # não encontra nada
```

```
## character(0)
```

```r
load(file="aula_1.RData")
ls() # note que os objetos foram carregados
```

```
##  [1] "dados_2010_11_10" "dados_2013_11_10" "encoding"        
##  [4] "input"            "novembro"         "out"             
##  [7] "outubro"          "publish"          "shortcode"       
## [10] "title"
```

Com a função `save()` é possível salvar apenas um ou um conjunto de objetos.


```r
# simula 100 obs de uma normal(10, 2)
sim_normal <- rnorm(100, mean=10, sd=2)

# salva no arquivo sim_normal.RData e remove da área de trabalho
save(sim_normal, file="sim_normal.RData") 
rm(sim_normal) 
ls() # sim_normal não aparece
```

```
##  [1] "dados_2010_11_10" "dados_2013_11_10" "encoding"        
##  [4] "input"            "novembro"         "out"             
##  [7] "outubro"          "publish"          "shortcode"       
## [10] "title"
```

```r
# carrega sim_normal.RData
load(file="sim_normal.RData")
ls() # sim_normal aparece
```

```
##  [1] "dados_2010_11_10" "dados_2013_11_10" "encoding"        
##  [4] "input"            "novembro"         "out"             
##  [7] "outubro"          "publish"          "shortcode"       
## [10] "sim_normal"       "title"
```

Estas operações podem ser realizadas com o botão de salvar no canto direito do RStudio.

Outro conjunto de funções para salvar e ler objetos do R são `saveRDS()` e `readRDS()`. Uma das principais diferenças com relação a `save()` e `load()` é que, enquanto estas salvam e carregam os objetos com o seu nome original, as funções RDS permitem a você carregar o objeto com um nome diferente.



```r
saveRDS(sim_normal, file="sim_normal.rds")
rm(sim_normal)
### carrega sim_normal.rds em um objeto com nome diferente ###
simulacao <- readRDS("sim_normal.rds")
ls()
```

```
##  [1] "dados_2010_11_10" "dados_2013_11_10" "encoding"        
##  [4] "input"            "novembro"         "out"             
##  [7] "outubro"          "publish"          "shortcode"       
## [10] "simulacao"        "title"
```

## Exercícios
Agora é sua vez.

- Remova todos os objetos do ambiente de trabalho.
- Crie objetos com nomes `dados_2010_10_10`, `dados_2010_11_10`, `dados_2013_10_10`, `dados_2013_11_10`. Faça com que os objetos sejam do tipo numérico, character, lógico e inteiro. Verifique a classe e a estrutura dos objetos criados.
- Use `ls()` para listar apenas os dados de Novembro. E depois para listar apenas os dados de Outubro. Use `rm()` para remover apenas os dados de outubro (dica: você vai precisar do resultado de `ls()`).
- Salve sua area de trabalho com o nome `exercicio_objetos.RData`. Salve apenas `dados_2010_11_10` com o nome `dados_2010_11_10.RData`.

## Soluções


```r
rm(list=ls()) # remove todos os objetos

dados_2010_10_10 <- 10.5
dados_2010_11_10 <- "texto"
dados_2013_10_10 <- TRUE 
dados_2013_11_10 <- 24L

class(dados_2010_10_10)
class(dados_2010_11_10)
class(dados_2013_10_10)
class(dados_2013_11_10)

str(dados_2010_10_10)
str(dados_2010_11_10)
str(dados_2013_10_10)
str(dados_2013_11_10)

novembro <- ls(pattern="_11_")
outubro <- ls(pattern="_10_")

rm(list=outubro)

save.image(file="exercicios_objetos.RData")
save(dados_2010_11_10, file="dados_2010_11_10.RData")
```
