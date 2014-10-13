Test2Q5
========================================================

Read this data set into R and report the sum of the numbers in the fourth of the nine columns. 

https://d396qusza40orc.cloudfront.net/getdata%2Fwksst8110.for 

Original source of the data: http://www.cpc.ncep.noaa.gov/data/indices/wksst8110.for 

(Hint this is a fixed width file format)

Empiezo bajando el archivo para variar


```r
if (!file.exists("dataTest")) {
    dir.create("dataTest")
}

dataOrigin <- "https://d396qusza40orc.cloudfront.net/getdata%2Fwksst8110.for "

destfile <- "./dataTest/dataQ5.for"

if (!file.exists(destfile)) {
    getwd()
    download.file(dataOrigin, destfile, method = "curl")
}

```


Despues miro a ojo en las primeras lineas los anchos de las 9 columnas, eso hay que hacerlo a mano  

va a tocar hacerlo con read.fwf 
las cuatro primeras filas no aportan nada, asi que la cosa sera poner un skip = 4 

los anchos a ojo podrian ser algo asi como 14,5,4,9,4,9,4,9,4   


```r
data <- read.fwf(file = destfile, widths = c(14, 5, 4, 9, 4, 9, 4, 9, 4), skip = 4)

head(data)
```

```
##               V1   V2   V3   V4   V5   V6   V7   V8  V9
## 1  03JAN1990     23.4 -0.4 25.1 -0.3 26.6  0.0 28.6 0.3
## 2  10JAN1990     23.4 -0.8 25.2 -0.3 26.6  0.1 28.6 0.3
## 3  17JAN1990     24.2 -0.3 25.3 -0.3 26.5 -0.1 28.6 0.3
## 4  24JAN1990     24.4 -0.5 25.5 -0.4 26.5 -0.1 28.4 0.2
## 5  31JAN1990     25.1 -0.2 25.8 -0.2 26.7  0.1 28.4 0.2
## 6  07FEB1990     25.8  0.2 26.1 -0.1 26.8  0.1 28.4 0.3
```


El resultado tiene bastante buena pinta asi que calculamos lo que pide 


```r
sum(data[, 4])
```

```
## [1] 32427
```



