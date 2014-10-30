Quiz w 4
========================================================



Question 1
------------ 

The American Community Survey distributes downloadable data about United States communities. Download the 2006 microdata survey about housing for the state of Idaho using download.file() from here: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv 

and load the data into R. The code book, describing the variable names is here: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FPUMSDataDict06.pdf 

Apply strsplit() to split all the names of the data frame on the characters "wgtp". What is the value of the 123 element of the resulting list?



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

cosa <- strsplit(names(datos), "wgtp")

cosa[123]
```

```
## [[1]]
## [1] ""   "15"
```





Question 2
--------------------
Load the Gross Domestic Product data for the 190 ranked countries in this data set: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv 

Remove the commas from the GDP numbers in millions of dollars and average them. What is the average? 

Original data sources: http://data.worldbank.org/data-catalog/GDP-ranking-table








```r
if (!file.exists("dataTest")) {
    dir.create("dataTest")
}

dataOrigin <- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv"

destfile <- "./dataTest/dataQ2.csv"

if (!file.exists(destfile)) {
    getwd()
    download.file(dataOrigin, destfile, method = "curl")
}

# esto ya lo apa??e de la semana pasada
datos <- read.csv(destfile, na.strings = c("", "NA"), skip = 4, nrows = 190)
```


la columna que nos interesa es la X.4 asi que nos quedamos solo con ella 


```r
datos <- datos$X.4

datos <- gsub("\\,", "", datos)
datos <- as.numeric(datos)
mean(datos)
```

```
## [1] 377652
```



Question 3
----------------
In the data set from Question 2 what is a regular expression that would allow you to count the number of countries whose name begins with "United"? Assume that the variable with the country names in it is named countryNames. How many countries begin with United?

y ahora nos jodemos por que he pisado los datos 


```r
datos <- read.csv(destfile, na.strings = c("", "NA"), skip = 4, nrows = 190)
countryNames <- datos$X.3
grep("^United", countryNames, value = T)
```

```
## [1] "United States"        "United Kingdom"       "United Arab Emirates"
```


Question 4
-------------
Load the Gross Domestic Product data for the 190 ranked countries in this data set: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv 

Load the educational data from this data set: 

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv 

Match the data based on the country shortcode. Of the countries for which the end of the fiscal year is available, how many end in June?  


Cojo todo lo que tenia hecho de la semana pasada


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


dataMERG <- merge(dataEDU, dataGDP, by.x = "CountryCode", by.y = "ShortCode")
```



Los a??os fiscales estan en special notes 


```r
disponibles <- grep("Fiscal year end:", dataMERG$Special.Notes, value = T)
res <- grep("June", disponibles)
length(res)
```

```
## [1] 13
```



Question 5
---------------

You can use the quantmod (http://www.quantmod.com/) package to get historical stock prices for publicly traded companies on the NASDAQ and NYSE. Use the following code to download data on Amazon's stock price and get the times the data was sampled.


```r
library(quantmod)
```

```
## Warning: package 'quantmod' was built under R version 3.1.1
```

```
## Loading required package: xts
## Loading required package: zoo
## 
## Attaching package: 'zoo'
## 
## The following objects are masked from 'package:base':
## 
##     as.Date, as.Date.numeric
## 
## Loading required package: TTR
## Version 0.4-0 included new data defaults. See ?getSymbols.
```

```r
amzn = getSymbols("AMZN", auto.assign = FALSE)
```

```
##     As of 0.4-0, 'getSymbols' uses env=parent.frame() and
##  auto.assign=TRUE by default.
## 
##  This  behavior  will be  phased out in 0.5-0  when the call  will
##  default to use auto.assign=FALSE. getOption("getSymbols.env") and 
##  getOptions("getSymbols.auto.assign") are now checked for alternate defaults
## 
##  This message is shown once per session and may be disabled by setting 
##  options("getSymbols.warning4.0"=FALSE). See ?getSymbol for more details
```

```r
sampleTimes = index(amzn)
```


How many values were collected in 2012? How many values were collected on Mondays in 2012?


```r
library(lubridate)

agnos <- year(sampleTimes) == "2012"
sum(agnos)
```

```
## [1] 250
```

```r
samplemio <- sampleTimes[agnos]

dsemana <- wday(samplemio) == 2
sum(dsemana)
```

```
## [1] 47
```




Voy a probar con lubridate

