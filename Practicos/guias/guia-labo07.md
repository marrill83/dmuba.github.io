# Guía LABORATORIO VII: Análisis de Secuencias

Hoy vamos a trabajar con la librería __arulesSecuences__ de R para explorar los algoritmos __SPADE__ y __GSP__ que fueron abordados en la clase.

## Cargamos/Instalamos la librería arulesSecuences

```r
librerias_instaladas<-rownames(installed.packages())
if("arulesSecuences" %in% librerias_instaladas == FALSE) {
  install.packages("arulesSecuences", dependencies = TRUE)
}

library(arulesSecuences)
```

## Carga del dataset
Cargamos un dataset de ejemplo -que está en el repo, con el nombre de secuencias.txt- con algunas secuencias conformadas por caracteres alfanuméricos.
```r
setwd("path/to/file/")
transactions <- read_baskets("secuencias.txt", info = c("sequenceID","eventID","SIZE"))
```
Como puede observarse, en análisis de secuencias también vamos a trabajar con transacciones. Para más información sobre el tipo de datos __transaction__ de R puede mirar el siguiente [enlace](https://www.rdocumentation.org/packages/arules/versions/1.6-1/topics/transactions-class).

## Algoritmo SPADE

Generamos las secuencias con la función __cspade__, estableciendo un soporte mínimo como parámetro.

```R
secuences <- cspade(data.transactions, parameter = list(support = 0.4), control = list(verbose = TRUE))
```

Podemos ver un resumen con información de las secuencias generadas:

```R
summary(secuences)
```

Además, es posible observar las secuencias generadas a partir de la instrucción __inspect__:

```R
inspect(secuences)
```

# Consignas propuestas:
1. ¿Cuantas secuencias se generan si definimos un support=0.03? ¿y con un support=0.2? Fundamente la respuesta y compare con el algoritmo de la clase anterior.
2. Comente cuales son los items que aparecen en las secuencias con mayor soporte. ¿A qué principio obedece esto?
4. ¿Que información nos proveen los métodos __inspect__ y __summary__ sobre las secuencias? Explique que elementos de __cspade__ se observan a través de ellos.