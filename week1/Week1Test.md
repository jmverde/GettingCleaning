Week 1 test
========================================================

Question 1: 
--------------------------------------------------------

The American Community Survey distributes downloadable data about United States communities. Download the 2006 microdata survey about housing for the state of Idaho using download.file() from here: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv 

and load the data into R. The code book, describing the variable names is here: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FPUMSDataDict06.pdf 

How many properties are worth $1,000,000 or more?


First check existence of data directory, create if not, then check existence of file, download if not, and load into a variable 

Didnt put a timestamp because this is a one shot code


```r
if (!file.exists("dataTest")) {
    dir.create("dataTest")
}

dataOrigin <- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv"

destfile <- "./dataTest/dataQ1.csv"

if (!file.exists(destfile)) {
    getwd()
    download.file(dataOrigin, destfile, method = "curl")
}

dataQ1 <- read.csv(destfile)
head(dataQ1)
```

```
##   RT SERIALNO DIVISION PUMA REGION ST  ADJUST WGTP NP TYPE ACR AGS BDS BLD
## 1  H      186        8  700      4 16 1015675   89  4    1   1  NA   4   2
## 2  H      306        8  700      4 16 1015675  310  1    1  NA  NA   1   7
## 3  H      395        8  100      4 16 1015675  106  2    1   1  NA   3   2
## 4  H      506        8  700      4 16 1015675  240  4    1   1  NA   4   2
## 5  H      835        8  800      4 16 1015675  118  4    1   2   1   5   2
## 6  H      989        8  700      4 16 1015675  115  4    1   1  NA   3   2
##   BUS CONP ELEP FS FULP GASP HFL INSP KIT MHP MRGI MRGP MRGT MRGX PLM RMS
## 1   2   NA  180  0    2    3   3  600   1  NA    1 1300    1    1   1   9
## 2  NA   NA   60  0    2    3   3   NA   1  NA   NA   NA   NA   NA   1   2
## 3   2   NA   70  0    2   30   1  200   1  NA   NA   NA   NA    3   1   7
## 4   2   NA   40  0    2   80   1  200   1  NA    1  860    1    1   1   6
## 5   2   NA  250  0    2    3   3  700   1  NA    1 1900    1    1   1   7
## 6   2   NA  130  0    2    3   3  250   1  NA    1  700    1    1   1   6
##   RNTM RNTP SMP TEL TEN VACS VAL VEH WATP YBL FES  FINCP FPARC GRNTP GRPIP
## 1   NA   NA  NA   1   1   NA  17   3  840   5   2 105600     2    NA    NA
## 2    2  600  NA   1   3   NA  NA   1    1   3  NA     NA    NA   660    23
## 3   NA   NA  NA   1   2   NA  18   2   50   5   7   9400     2    NA    NA
## 4   NA   NA 400   1   1   NA  19   3  500   2   1  66000     1    NA    NA
## 5   NA   NA 650   1   1   NA  20   5    2   3   1  93000     2    NA    NA
## 6   NA   NA 400   1   1   NA  15   2 1200   5   2  61000     1    NA    NA
##   HHL HHT  HINCP HUGCL HUPAC HUPAOC HUPARC LNGI MV NOC NPF NPP NR NRC
## 1   1   1 105600     0     2      2      2    1  4   2   4   0  0   2
## 2   1   4  34000     0     4      4      4    1  3   0  NA   0  0   0
## 3   1   3   9400     0     2      2      2    1  2   1   2   0  0   1
## 4   1   1  66000     0     1      1      1    1  3   2   4   0  0   2
## 5   1   1  93000     0     2      2      2    1  1   1   4   0  0   1
## 6   1   1  61000     0     1      1      1    1  4   2   4   0  0   2
##   OCPIP PARTNER PSF R18 R60 R65 RESMODE SMOCP SMX SRNT SVAL TAXP WIF
## 1    18       0   0   1   0   0       1  1550   3    0    1   24   3
## 2    NA       0   0   0   0   0       2    NA  NA    1    0   NA  NA
## 3    23       0   0   1   0   0       1   179  NA    0    1   16   1
## 4    26       0   0   1   0   0       2  1422   1    0    1   31   2
## 5    36       0   0   1   0   0       1  2800   1    0    1   25   3
## 6    26       0   0   1   0   0       2  1330   2    0    1    7   1
##   WKEXREL WORKSTAT FACRP FAGSP FBDSP FBLDP FBUSP FCONP FELEP FFSP FFULP
## 1       2        3     0     0     0     0     0     0     0    0     0
## 2      NA       NA     0     0     0     0     0     0     0    0     0
## 3      13       13     0     0     0     0     0     0     0    0     0
## 4       2        1     0     0     0     0     0     0     0    0     0
## 5       1        1     0     0     0     0     0     0     0    0     0
## 6       7        3     0     0     0     0     0     0     0    0     0
##   FGASP FHFLP FINSP FKITP FMHP FMRGIP FMRGP FMRGTP FMRGXP FMVYP FPLMP
## 1     0     0     0     0    0      0     0      0      0     0     0
## 2     0     0     0     0    0      0     0      0      0     0     0
## 3     0     0     0     0    0      0     0      0      0     0     0
## 4     0     0     0     0    0      0     0      0      0     0     0
## 5     0     0     0     0    0      0     0      0      0     0     0
## 6     0     0     1     0    0      0     0      0      0     0     0
##   FRMSP FRNTMP FRNTP FSMP FSMXHP FSMXSP FTAXP FTELP FTENP FVACSP FVALP
## 1     0      0     0    0      0      0     0     0     0      0     0
## 2     0      0     0    0      0      0     0     0     0      0     0
## 3     0      0     0    0      0      0     0     0     0      0     0
## 4     0      0     0    0      0      0     0     0     0      0     0
## 5     0      0     0    0      0      0     0     0     0      0     0
## 6     0      0     0    0      0      0     1     0     0      0     0
##   FVEHP FWATP FYBLP wgtp1 wgtp2 wgtp3 wgtp4 wgtp5 wgtp6 wgtp7 wgtp8 wgtp9
## 1     0     0     0    87    28   156    95    26    25    95    93    93
## 2     0     0     1   539   363   293   422   566   289    87   242   453
## 3     0     0     0   187    35   184   178    83    95    31    32   177
## 4     0     0     0   232   406   234   270   249   242   406   249   287
## 5     0     0     0   107   194   129    41   156   174    47   113   101
## 6     0     1     0   191   197   127   115   115   107   119    34    32
##   wgtp10 wgtp11 wgtp12 wgtp13 wgtp14 wgtp15 wgtp16 wgtp17 wgtp18 wgtp19
## 1     91     87    166     90     25    153     89    148     82     25
## 2    453    334    358    414    102    281     99    108    278    131
## 3    118    110    114    184    107     95    115     33    118    120
## 4     67     72    413    399     77    245    424     67     63    226
## 5     33    115     52    113     95    135    206    100    185    135
## 6     30    123    199    117     33    109    117     31    115    201
##   wgtp20 wgtp21 wgtp22 wgtp23 wgtp24 wgtp25 wgtp26 wgtp27 wgtp28 wgtp29
## 1    180     90     24    140     92     25     27     86     84     87
## 2    407    447    264    352    238    390    336    122    374    482
## 3     37    184     35    176    176    110    103     29     30    197
## 4    254    238     69    238    255    239    248     69    234    247
## 5    279    116     33    105    244     38     30    230    123    123
## 6    190    184    198    113    109    117    111    110     33     37
##   wgtp30 wgtp31 wgtp32 wgtp33 wgtp34 wgtp35 wgtp36 wgtp37 wgtp38 wgtp39
## 1     93     90    149     91     28    143     81    144     95     27
## 2    468    335    251    613    104    284    116     91    326    102
## 3    127     92    118    177     99     99    109     34    100    105
## 4    437    423     74     61    401    267     72    388    335    229
## 5    243    120    238     98     90    107     44    122     32    127
## 6     36    110    183    114     35    134    119     32    121    188
##   wgtp40 wgtp41 wgtp42 wgtp43 wgtp44 wgtp45 wgtp46 wgtp47 wgtp48 wgtp49
## 1     22     90    171     27     83    153    148     92     91     91
## 2    361    107    253    321    289     96    343    564    274    118
## 3     33    173     36    168    175     99    103     30     35    155
## 4    236    239     65    259    247    230    225     82    220    233
## 5    195    116     36    135    237     33     33    249    102     84
## 6     33     34     32    109    115    115    112    119    192    186
##   wgtp50 wgtp51 wgtp52 wgtp53 wgtp54 wgtp55 wgtp56 wgtp57 wgtp58 wgtp59
## 1     93     90     26     94    142     24     91     29     84    148
## 2    118    321    261    130    463    294    479    391    307    476
## 3    102     95    107    185    120    114    113     36    115    103
## 4    419    390     69     74    391    276     70    422    409    223
## 5    224    119    250    119    125    126     32    112     33    131
## 6    213    106     34    124    179    106    107    190    112     34
##   wgtp60 wgtp61 wgtp62 wgtp63 wgtp64 wgtp65 wgtp66 wgtp67 wgtp68 wgtp69
## 1     30     93    143     24     88    147    145     91     83     83
## 2    283    116    353    323    374    106    236    380    313     90
## 3     29    183     35    179    169     95    110     28     34    233
## 4    245    269    488    221    250    247    240    415    234    219
## 5     45    101    165    125     41    191    195     49    119     92
## 6     35     32     34    119    123    122    121    123    196    196
##   wgtp70 wgtp71 wgtp72 wgtp73 wgtp74 wgtp75 wgtp76 wgtp77 wgtp78 wgtp79
## 1     86     81     27     93    151     28     79     25    101    157
## 2     94    292    401     81    494    346    496    615    286    454
## 3     97    123    119    168    107     95    101     30    124    106
## 4     66     68    359    385     71    234    421     76     77    242
## 5     44    127     36    119    121    116    209     97    176    144
## 6    207    120     34    109    199    116    110    211    120     31
##   wgtp80
## 1    129
## 2    260
## 3     31
## 4    231
## 5     38
## 6    189
```


La columna que tiene el valor que nos interesa segun el codebook se llama VAL, nos quedamos solo con esa 


```r
dataQ1 <- subset(dataQ1, select = "VAL")
head(dataQ1)
```

```
##   VAL
## 1  17
## 2  NA
## 3  18
## 4  19
## 5  20
## 6  15
```


Los valores estan codificados en clave,  las posesiones con mayor valor que 1M$ tienen el codigo 24


```r
sum(dataQ1$VAL == 24, na.rm = TRUE)
```

```
## [1] 53
```


Y la respuesta es 53  Lo que esta bastante bien por que es una de las posibilidades


Question 2: 
--------------------------------------------------------
Use the data you loaded from Question 1. Consider the variable FES in the code book. Which of the "tidy data" principles does this variable violate?
Numeric values in tidy data can not represent categories.
Tidy data has one variable per column.
Tidy data has variable values that are internally consistent.
Each tidy data table contains information about only one type of observation

Veamos que dice el codebook de la variable FES 

"FES 1 
 Family type and employment status "

Con lo que tenemos dos variables por columna y la respuesta es la que en esta version del examen sale la segunda 


Question 3: 
--------------------------------------------------------

Download the Excel spreadsheet on Natural Gas Aquisition Program here: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FDATA.gov_NGAP.xlsx 

Read rows 18-23 and columns 7-15 into R and assign the result to a variable called:
 dat 
What is the value of:
 sum(dat$Zip*dat$Ext,na.rm=T) 
(original data source: http://catalog.data.gov/dataset/natural-gas-acquisition-program) 

Empezamos buscando la existencia del archivo y directorio  y si no lo hay lo creamos y descargamos



```r
if (!file.exists("dataTest")) {
    dir.create("dataTest")
}

dataOrigin <- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FDATA.gov_NGAP.xlsx"

destfile <- "./dataTest/dataQ3.xlsx"

if (!file.exists(destfile)) {
    getwd()
    download.file(dataOrigin, destfile, method = "curl")
}

```



Ahora que ya tenemos el archivo podemos cargarlo a la variable dat como piden (es necesario haber instalado con install.packages el paquete "xlsx")



```r
library(xlsx)
```

```
## Warning: package 'xlsx' was built under R version 3.1.1
```

```
## Loading required package: rJava
## Loading required package: xlsxjars
```

```
## Warning: package 'xlsxjars' was built under R version 3.1.1
```

```r
dat <- read.xlsx(destfile, sheetIndex = 1, header = TRUE, rowIndex = 18:23, 
    colIndex = 7:15)
head(dat)
```

```
##     Zip CuCurrent PaCurrent PoCurrent      Contact Ext          Fax email
## 1 74136         0         1         0 918-491-6998   0 918-491-6659    NA
## 2 30329         1         0         0 404-321-5711  NA         <NA>    NA
## 3 74136         1         0         0 918-523-2516   0 918-523-2522    NA
## 4 80203         0         1         0 303-864-1919   0         <NA>    NA
## 5 80120         1         0         0 345-098-8890 456         <NA>    NA
##   Status
## 1      1
## 2      1
## 3      1
## 4      1
## 5      1
```


y ya metemos la cuentecita del examen, que no sirve para nada mas que para el examen todo sea dicho 


```r
sum(dat$Zip * dat$Ext, na.rm = T)
```

```
## [1] 36534720
```




Question 4
-------------------------------------------------
Read the XML data on Baltimore restaurants from here: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml 

How many restaurants have zipcode 21231?


Empezamos buscando la existencia del archivo y directorio  y si no lo hay lo creamos y descargamos



```r
if (!file.exists("dataTest")) {
    dir.create("dataTest")
}

dataOrigin <- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml"

destfile <- "./dataTest/dataQ4.xml"

if (!file.exists(destfile)) {
    getwd()
    download.file(dataOrigin, destfile, method = "curl")
}
```



Vamos a cargar el archivo

```r
library(XML)
document <- xmlTreeParse(destfile, useInternalNodes = T)

rootNode <- xmlRoot(document)
```


Hay una forma bastante facil de hacerlos sabiendo que el tag que buscamos se llama zipcode,  extraemos todos los valores de zipcode a un archivo


```r
zips <- xpathSApply(rootNode, "//zipcode", xmlValue)
```


Y sumamos los que coinciden con el 21231 


```r
sum(zips == "21231")
```

```
## [1] 127
```



Question 5
-------------------------------

Aunque es evidente aqui pondre el codigo para comprobarlo y tener guardados los tiempos 

Va a haber que usar system.time
