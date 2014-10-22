Week 3 Quiz
========================================================

Question 1

The American Community Survey distributes downloadable data about United States communities. Download the 2006 microdata survey about housing for the state of Idaho using download.file() from here: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv 

and load the data into R. The code book, describing the variable names is here: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FPUMSDataDict06.pdf 

Create a logical vector that identifies the households on greater than 10 acres who sold more than $10,000 worth of agriculture products. Assign that logical vector to the variable agricultureLogical. Apply the which() function like this to identify the rows of the data frame where the logical vector is TRUE. which(agricultureLogical) What are the first 3 values that result?
236, 238, 262
59, 460, 474
125, 238,262
153 ,236, 388




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

datos <- read.csv(destfile)

head(datos)
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




De acuerdo con la documentacion  la primera condicion implica que la variable (ACR) tiene que tener un valor de 3 y la variable AGS un valor de 6 



```r
agricultureLogical <- ((datos$ACR == 3) & (datos$AGS == 6))
head(agricultureLogical)
```

```
## [1] FALSE    NA FALSE FALSE FALSE FALSE
```

```r
which(agricultureLogical)
```

```
##  [1]  125  238  262  470  555  568  608  643  787  808  824  849  952  955
## [15] 1033 1265 1275 1315 1388 1607 1629 1651 1856 1919 2101 2194 2403 2443
## [29] 2539 2580 2655 2680 2740 2838 2965 3131 3133 3163 3291 3370 3402 3585
## [43] 3652 3852 3862 3912 4023 4045 4107 4113 4117 4185 4198 4310 4343 4354
## [57] 4448 4453 4461 4718 4817 4835 4910 5140 5199 5236 5326 5417 5531 5574
## [71] 5894 6033 6044 6089 6275 6376 6420
```



Question 2
--------------------------------------------------------

Using the jpeg package read in the following picture of your instructor into R 

https://d396qusza40orc.cloudfront.net/getdata%2Fjeff.jpg 

Use the parameter native=TRUE. What are the 30th and 80th quantiles of the resulting data? (some Linux systems may produce an answer 638 different for the 30th quantile)
-10904118 -10575416
10904118 -594524
-15259150 -10575416
-15259150 -594524 

empezamos por cargar el package y descargar el archi


```r
if (!file.exists("dataTest")) {
    dir.create("dataTest")
}

dataOrigin <- "https://d396qusza40orc.cloudfront.net/getdata%2Fjeff.jpg"

destfile <- "./dataTest/dataQ2.jpg"

if (!file.exists(destfile)) {
    getwd()
    download.file(dataOrigin, destfile, method = "curl")
}

library(jpeg)
image <- readJPEG(destfile, native = TRUE)
```


ahora que tenemos los datos es tan facil como 


```r
quantile(image, probs = c(0.3, 0.8))
```

```
##       30%       80% 
## -15259150 -10575416
```



Question 3
--------------


Load the Gross Domestic Product data for the 190 ranked countries in this data set: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv 

Load the educational data from this data set: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv 

Match the data based on the country shortcode. How many of the IDs match? Sort the data frame in descending order by GDP rank (so United States is last). What is the 13th country in the resulting data frame? 

Original data sources: 
http://data.worldbank.org/data-catalog/GDP-ranking-table 
http://data.worldbank.org/data-catalog/ed-stats
190, Spain
234, Spain
189, St. Kitts and Nevis
189, Spain
190, St. Kitts and Nevis
234, St. Kitts and Nevis


En primer lugar descargamos los archivos y los cargamos en DF



```r
if (!file.exists("dataTest")) {
    dir.create("dataTest")
}

dataOriginGDP <- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv "

destfileGDP <- "./dataTest/GDP.csv"

if (!file.exists(destfileGDP)) {
    getwd()
    download.file(dataOriginGDP, destfileGDP, method = "curl")
}


dataOriginEDU <- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv  "

destfileEDU <- "./dataTest/EDU.csv"

if (!file.exists(destfileEDU)) {
    getwd()
    download.file(dataOriginEDU, destfileEDU, method = "curl")
}

dataGDP <- read.csv(destfileGDP, na.strings = c("", "NA"), skip = 4, nrows = 190)
dataEDU <- read.csv(destfileEDU, na.strings = c("", "NA"))
head(dataGDP)
```

```
##     X X.1 X.2            X.3          X.4  X.5 X.6 X.7 X.8 X.9
## 1 USA   1  NA  United States  16,244,600  <NA>  NA  NA  NA  NA
## 2 CHN   2  NA          China   8,227,103  <NA>  NA  NA  NA  NA
## 3 JPN   3  NA          Japan   5,959,718  <NA>  NA  NA  NA  NA
## 4 DEU   4  NA        Germany   3,428,131  <NA>  NA  NA  NA  NA
## 5 FRA   5  NA         France   2,612,878  <NA>  NA  NA  NA  NA
## 6 GBR   6  NA United Kingdom   2,471,784  <NA>  NA  NA  NA  NA
```

```r
head(dataEDU)
```

```
##   CountryCode                    Long.Name         Income.Group
## 1         ABW                        Aruba High income: nonOECD
## 2         ADO      Principality of Andorra High income: nonOECD
## 3         AFG Islamic State of Afghanistan           Low income
## 4         AGO  People's Republic of Angola  Lower middle income
## 5         ALB          Republic of Albania  Upper middle income
## 6         ARE         United Arab Emirates High income: nonOECD
##                       Region Lending.category Other.groups  Currency.Unit
## 1  Latin America & Caribbean             <NA>         <NA>  Aruban florin
## 2      Europe & Central Asia             <NA>         <NA>           Euro
## 3                 South Asia              IDA         HIPC Afghan afghani
## 4         Sub-Saharan Africa              IDA         <NA> Angolan kwanza
## 5      Europe & Central Asia             IBRD         <NA>   Albanian lek
## 6 Middle East & North Africa             <NA>         <NA>  U.A.E. dirham
##   Latest.population.census  Latest.household.survey
## 1                     2000                     <NA>
## 2           Register based                     <NA>
## 3                     1979               MICS, 2003
## 4                     1970 MICS, 2001, MIS, 2006/07
## 5                     2001               MICS, 2005
## 6                     2005                     <NA>
##                                                                 Special.Notes
## 1                                                                        <NA>
## 2                                                                        <NA>
## 3 Fiscal year end: March 20; reporting period for national accounts data: FY.
## 4                                                                        <NA>
## 5                                                                        <NA>
## 6                                                                        <NA>
##   National.accounts.base.year National.accounts.reference.year
## 1                        1995                               NA
## 2                        <NA>                               NA
## 3                   2002/2003                               NA
## 4                        1997                               NA
## 5                        <NA>                             1996
## 6                        1995                               NA
##   System.of.National.Accounts SNA.price.valuation
## 1                          NA                <NA>
## 2                          NA                <NA>
## 3                          NA                 VAB
## 4                          NA                 VAP
## 5                        1993                 VAB
## 6                          NA                 VAB
##   Alternative.conversion.factor PPP.survey.year
## 1                          <NA>              NA
## 2                          <NA>              NA
## 3                          <NA>              NA
## 4                       1991-96            2005
## 5                          <NA>            2005
## 6                          <NA>              NA
##   Balance.of.Payments.Manual.in.use External.debt.Reporting.status
## 1                              <NA>                           <NA>
## 2                              <NA>                           <NA>
## 3                              <NA>                         Actual
## 4                              BPM5                         Actual
## 5                              BPM5                         Actual
## 6                              BPM4                           <NA>
##   System.of.trade Government.Accounting.concept
## 1         Special                          <NA>
## 2         General                          <NA>
## 3         General                  Consolidated
## 4         Special                          <NA>
## 5         General                  Consolidated
## 6         General                  Consolidated
##   IMF.data.dissemination.standard
## 1                            <NA>
## 2                            <NA>
## 3                            GDDS
## 4                            GDDS
## 5                            GDDS
## 6                            GDDS
##   Source.of.most.recent.Income.and.expenditure.data
## 1                                              <NA>
## 2                                              <NA>
## 3                                              <NA>
## 4                                         IHS, 2000
## 5                                        LSMS, 2005
## 6                                              <NA>
##   Vital.registration.complete Latest.agricultural.census
## 1                        <NA>                       <NA>
## 2                         Yes                       <NA>
## 3                        <NA>                       <NA>
## 4                        <NA>                    1964-65
## 5                         Yes                       1998
## 6                        <NA>                       1998
##   Latest.industrial.data Latest.trade.data Latest.water.withdrawal.data
## 1                     NA              2008                           NA
## 2                     NA              2006                           NA
## 3                     NA              2008                         2000
## 4                     NA              1991                         2000
## 5                   2005              2008                         2000
## 6                     NA              2008                         2005
##   X2.alpha.code WB.2.code           Table.Name           Short.Name
## 1            AW        AW                Aruba                Aruba
## 2            AD        AD              Andorra              Andorra
## 3            AF        AF          Afghanistan          Afghanistan
## 4            AO        AO               Angola               Angola
## 5            AL        AL              Albania              Albania
## 6            AE        AE United Arab Emirates United Arab Emirates
```

```r
# vamos a retocar un poquito los nombres de dataGDP que asi son feos
names(dataGDP)[1] <- "ShortCode"
names(dataGDP)[2] <- "GDPRank"
```


Por inspeccion vemos que el codigo de archivo es en dataEdu, "CountryCode", mientras que en GDP es la primera columna que es "ShortCode"  asi que va a tocar hacerlo con merge Ojo, que solo valian los ranked


```r
dataMERG <- merge(dataEDU, dataGDP, by.x = "CountryCode", by.y = "ShortCode")
dim(dataMERG)
```

```
## [1] 189  40
```


el numero que coinciden es 189

Para la segunda parte hay que colocarlos por la columna GDPRank, pero antes hay que convertirla en numerica que si no la liamos 


```r
dataMERG$GDPRank <- as.numeric(dataMERG$GDPRank)

library(plyr)
dataMERGORD <- arrange(dataMERG, desc(GDPRank))
dataMERGORD[13, 2]
```

```
## [1] St. Kitts and Nevis
## 234 Levels: American Samoa Antigua and Barbuda ... World
```


y por supuesto sale ST kits  

DataMERG nos va a seguir haciendo falta para las proximas 

Question 4
----------------
What is the average GDP ranking for the "High income: OECD" and "High income: nonOECD" group? 

hay que hacerlo por income group 


```r
sapply(split(dataMERG$GDPRank, dataMERG$Income.Group), mean)
```

```
##    High income: OECD High income: nonOECD           Low income 
##                32.97                91.91               133.73 
##  Lower middle income  Upper middle income 
##               107.70                92.13
```



Question 5
---------------

Cut the GDP ranking into 5 separate quantile groups. Make a table versus Income.Group. How many countries are Lower middle income but among the 38 nations with highest GDP?

Metemos los grupos en una nueva variable y hacemos la tabla

```r
dataMERG$GDPQ <- cut(dataMERG$GDPRank, 5)
table(dataMERG$GDPQ, dataMERG$Income.Group)
```

```
##               
##                High income: OECD High income: nonOECD Low income
##   (0.811,38.8]                18                    4          0
##   (38.8,76.6]                 10                    5          1
##   (76.6,114]                   1                    8          9
##   (114,152]                    1                    4         16
##   (152,190]                    0                    2         11
##               
##                Lower middle income Upper middle income
##   (0.811,38.8]                   5                  11
##   (38.8,76.6]                   13                   9
##   (76.6,114]                    12                   8
##   (114,152]                      8                   8
##   (152,190]                     16                   9
```


La respuesta se saca por inspeccion del resultado
