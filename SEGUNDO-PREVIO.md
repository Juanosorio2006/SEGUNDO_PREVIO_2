Segundo Previo De DISEÑO DE EXPERIMENTOS
================

## *Juan Felipe Osorio Ramirez 1950139*

Este es el segundo previo de diseño de experimentos, teniendo como base
de datos para la prueba la base stackloss que nos muestra los datos
operativos de una planta de oxidación de amoniaco a ácido nítrico.

## Stackloss

``` r
View(stackloss)
force(stackloss)
```

    ##    Air.Flow Water.Temp Acid.Conc. stack.loss
    ## 1        80         27         89         42
    ## 2        80         27         88         37
    ## 3        75         25         90         37
    ## 4        62         24         87         28
    ## 5        62         22         87         18
    ## 6        62         23         87         18
    ## 7        62         24         93         19
    ## 8        62         24         93         20
    ## 9        58         23         87         15
    ## 10       58         18         80         14
    ## 11       58         18         89         14
    ## 12       58         17         88         13
    ## 13       58         18         82         11
    ## 14       58         19         93         12
    ## 15       50         18         89          8
    ## 16       50         18         86          7
    ## 17       50         19         72          8
    ## 18       50         19         79          8
    ## 19       50         20         80          9
    ## 20       56         20         82         15
    ## 21       70         20         91         15

data(stackloss) stackloss

# porcentaje de acido = (Acid.Conc./10)+50

names(stackloss) ncol(stackloss) nrow(stackloss)

``` r
summary(stackloss)
```

    ##     Air.Flow       Water.Temp     Acid.Conc.      stack.loss   
    ##  Min.   :50.00   Min.   :17.0   Min.   :72.00   Min.   : 7.00  
    ##  1st Qu.:56.00   1st Qu.:18.0   1st Qu.:82.00   1st Qu.:11.00  
    ##  Median :58.00   Median :20.0   Median :87.00   Median :15.00  
    ##  Mean   :60.43   Mean   :21.1   Mean   :86.29   Mean   :17.52  
    ##  3rd Qu.:62.00   3rd Qu.:24.0   3rd Qu.:89.00   3rd Qu.:19.00  
    ##  Max.   :80.00   Max.   :27.0   Max.   :93.00   Max.   :42.00

``` r
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.3     v purrr   0.3.4
    ## v tibble  3.1.0     v dplyr   1.0.6
    ## v tidyr   1.1.3     v stringr 1.4.0
    ## v readr   1.4.0     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
mutate (stackloss,porcentaje_de_acido = ((Acid.Conc./10)+50))
```

    ##    Air.Flow Water.Temp Acid.Conc. stack.loss porcentaje_de_acido
    ## 1        80         27         89         42                58.9
    ## 2        80         27         88         37                58.8
    ## 3        75         25         90         37                59.0
    ## 4        62         24         87         28                58.7
    ## 5        62         22         87         18                58.7
    ## 6        62         23         87         18                58.7
    ## 7        62         24         93         19                59.3
    ## 8        62         24         93         20                59.3
    ## 9        58         23         87         15                58.7
    ## 10       58         18         80         14                58.0
    ## 11       58         18         89         14                58.9
    ## 12       58         17         88         13                58.8
    ## 13       58         18         82         11                58.2
    ## 14       58         19         93         12                59.3
    ## 15       50         18         89          8                58.9
    ## 16       50         18         86          7                58.6
    ## 17       50         19         72          8                57.2
    ## 18       50         19         79          8                57.9
    ## 19       50         20         80          9                58.0
    ## 20       56         20         82         15                58.2
    ## 21       70         20         91         15                59.1

## Relación entre la temperatura del agua y la tasa de funcionamiento de la planta por observación

``` r
mutate (stackloss,Relacion.T.F = Air.Flow/Water.Temp)
```

    ##    Air.Flow Water.Temp Acid.Conc. stack.loss Relacion.T.F
    ## 1        80         27         89         42     2.962963
    ## 2        80         27         88         37     2.962963
    ## 3        75         25         90         37     3.000000
    ## 4        62         24         87         28     2.583333
    ## 5        62         22         87         18     2.818182
    ## 6        62         23         87         18     2.695652
    ## 7        62         24         93         19     2.583333
    ## 8        62         24         93         20     2.583333
    ## 9        58         23         87         15     2.521739
    ## 10       58         18         80         14     3.222222
    ## 11       58         18         89         14     3.222222
    ## 12       58         17         88         13     3.411765
    ## 13       58         18         82         11     3.222222
    ## 14       58         19         93         12     3.052632
    ## 15       50         18         89          8     2.777778
    ## 16       50         18         86          7     2.777778
    ## 17       50         19         72          8     2.631579
    ## 18       50         19         79          8     2.631579
    ## 19       50         20         80          9     2.500000
    ## 20       56         20         82         15     2.800000
    ## 21       70         20         91         15     3.500000

## Promedio de la relacion

colSums(Relacion.T.F)

``` r
60.46128/21
```

    ## [1] 2.879109

``` r
# De aqui podemos deducir que la relacion promedio entre la temperatura y el funcionamiento de la planta es de 2.87 a 1, es decir por cada grado de temperatura que aumente el agua, el funcionamiento ira creciendo exponencialmente de 2.87 en 2.87
```

## Filtracion de datos por Temperaturas: 19° y 23°

``` r
filter(stackloss,Water.Temp == 19)
```

    ##   Air.Flow Water.Temp Acid.Conc. stack.loss
    ## 1       58         19         93         12
    ## 2       50         19         72          8
    ## 3       50         19         79          8

``` r
filter(stackloss,Water.Temp == 23)
```

    ##   Air.Flow Water.Temp Acid.Conc. stack.loss
    ## 1       62         23         87         18
    ## 2       58         23         87         15

## Desviacion Estandar

``` r
temp23 <- filter(stackloss,Water.Temp == 23)

A <- c(58,50,50,62,58)
W <- c(19,19,19,23,23)
Ac <- c(93,72,79,87,87)
S <- c(12,8,8,18,15)

sd(c(A,Ac,W,S))
```

    ## [1] 29.70557

``` r
# La desviacion estandar entre los datos de la tabla es de 29.70557 
```
