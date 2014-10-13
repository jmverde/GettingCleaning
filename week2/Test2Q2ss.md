Test2Q2ss
========================================================

Question 2
The sqldf package allows for execution of SQL commands on R data frames. We will use the sqldf package to practice the queries we might send with the dbSendQuery command in RMySQL. Download the American Community Survey data and load it into an R object called
 acs


https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06pid.csv 

Which of the following commands will select only the data for the probability weights pwgtp1 with ages less than 50?
sqldf("select * from acs where AGEP < 50")
sqldf("select pwgtp1 from acs where AGEP < 50")
sqldf("select * from acs")
sqldf("select pwgtp1 from acs")



```r
if (!file.exists("dataTest")) {
    dir.create("dataTest")
}

dataOrigin <- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06pid.csv"

destfile <- "./dataTest/dataQ2.csv"

if (!file.exists(destfile)) {
    getwd()
    download.file(dataOrigin, destfile, method = "curl")
}

acs <- read.csv(destfile)
head(acs)
```

```
##   RT SERIALNO SPORDER PUMA ST  ADJUST PWGTP AGEP CIT COW DDRS DEYE DOUT
## 1  P      186       1  700 16 1015675    89   43   1   7    2    2    2
## 2  P      186       2  700 16 1015675    92   42   1   4    2    2    2
## 3  P      186       3  700 16 1015675   107   16   1   1    2    2    2
## 4  P      186       4  700 16 1015675    91   14   1  NA    2    2   NA
## 5  P      306       1  700 16 1015675   309   29   1   5    2    2    2
## 6  P      395       1  100 16 1015675   108   40   1   8    2    2    2
##   DPHY DREM DWRK ENG FER GCL GCM GCR INTP JWMNP JWRIP JWTR LANX MAR MIG
## 1    2    2    2  NA  NA   2  NA  NA    0    15     1    1    2   1   1
## 2    2    2    2  NA   2   2  NA  NA    0    NA    NA   NA    2   1   1
## 3    2    2    2  NA  NA  NA  NA  NA    0     5     1    1    2   5   1
## 4    2    2   NA  NA  NA  NA  NA  NA   NA    NA    NA   NA    2   5   1
## 5    2    2    2  NA  NA  NA  NA  NA    0    50     8    1    2   5   1
## 6    2    2    2  NA   2   2  NA  NA    0     8     1    1    2   5   2
##   MIL MILY MLPA MLPB MLPC MLPD MLPE MLPF MLPG MLPH MLPI MLPJ MLPK NWAB
## 1   3    2    0    0    1    0    0    0    0    0    0    0    0    3
## 2   5   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA    2
## 3  NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA    3
## 4  NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA
## 5   2    2    1    0    0    0    0    0    0    0    0    0    0    3
## 6   5   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA    2
##   NWAV NWLA NWLK NWRE OIP PAP REL RETP SCH SCHG SCHL  SEMP SEX SSIP SSP
## 1    5    3    3    3   0   0   0    0   1   NA   10 50000   1    0   0
## 2    5    2    2    3   0   0   1    0   1   NA    9     0   2    0   0
## 3    5    3    3    3   0   0   2    0   3    5    7     0   1    0   0
## 4   NA   NA   NA   NA  NA  NA   2   NA   3    4    4    NA   2   NA  NA
## 5    5    3    3    3   0   0   0    0   1   NA   12     0   1    0   0
## 6    5    2    2    2   0   0   0    0   1   NA   13     0   2    0   0
##    WAGP WKHP WKL WKW YOEP UWRK ANC ANC1P ANC2P DECADE DRIVESP DS ESP ESR
## 1 50000   50   1  52   NA    1   2   920   148     NA       1  2  NA   1
## 2   800    4   1  20   NA    2   1   920   999     NA      NA  2  NA   6
## 3  4800   20   1  52   NA    1   2   920   148     NA       1  2   2   1
## 4    NA   NA  NA  NA   NA   NA   1   920   999     NA      NA  2   2  NA
## 5 34000   50   1  52   NA    1   2   902   920     NA       6  2  NA   1
## 6  9000   50   1  52   NA    1   2    82    22     NA       1  2  NA   1
##   HISP INDP JWAP JWDP LANP MIGPUMA MIGSP MSP NAICSP NATIVITY NOP OC OCCP
## 1    1 7690   88   46   NA      NA    NA   1  5617Z        1  NA  0 4200
## 2    1 7870   NA   NA   NA      NA    NA   1  611M1        1  NA  0 2340
## 3    1 8680  200  119   NA      NA    NA   6   722Z        1   1  1 4020
## 4    1   NA   NA   NA   NA      NA    NA  NA               1   1  1   NA
## 5    1 9590   72   23   NA      NA    NA   6   928P        1  NA  0 7140
## 6    1 5370  101   61   NA       1   215   6  45121        1  NA  0 4700
##   PAOC  PERNP  PINCP POBP POVPIP POWPUMA POWSP QTRBIR RAC1P RAC2P RAC3P
## 1   NA 100000 100000   53    501     600    16      3     1     1    69
## 2    2    800    800   41    501      NA    NA      3     1     1    69
## 3   NA   4800   4800   16    501     600    16      2     1     1    69
## 4   NA     NA     NA   41    501      NA    NA      4     1     1    69
## 5   NA  34000  34000   36    333     400    16      1     9    67    43
## 6    2   9000   9000   16     68     100    16      1     1     1    69
##   RACAIAN RACASN RACBLK RACNHPI RACNUM RACSOR RACWHT RC SFN SFR   SOCP VPS
## 1       0      0      0       0      1      0      1  0  NA  NA 371011   9
## 2       0      0      0       0      1      0      1  0  NA  NA 253000  NA
## 3       0      0      0       0      1      0      1  1  NA  NA 352010  NA
## 4       0      0      0       0      1      0      1  1  NA  NA         NA
## 5       1      0      1       0      2      0      0  0  NA  NA 493011   1
## 6       0      0      0       0      1      0      1  0  NA  NA 411011  NA
##   WAOB FAGEP FANCP FCITP FCOWP FDDRSP FDEYEP FDOUTP FDPHYP FDREMP FDWRKP
## 1    1     0     0     0     0      0      0      0      0      0      0
## 2    1     0     0     0     0      0      0      0      0      0      0
## 3    1     0     0     0     0      0      0      0      0      0      0
## 4    1     0     0     0     0      0      0      0      0      0      0
## 5    1     0     0     0     0      0      0      0      0      0      0
## 6    1     0     0     0     0      0      0      0      0      0      0
##   FENGP FESRP FFERP FGCLP FGCMP FGCRP FHISP FINDP FINTP FJWDP FJWMNP
## 1     0     0     0     0     0     0     0     0     0     0      0
## 2     0     0     0     0     0     0     0     0     0     0      0
## 3     0     0     0     0     0     0     0     0     0     0      0
## 4     0     0     0     0     0     0     0     0     0     0      0
## 5     0     0     0     0     0     0     0     0     0     0      0
## 6     0     0     1     0     0     0     0     0     0     0      0
##   FJWRIP FJWTRP FLANP FLANXP FMARP FMIGP FMIGSP FMILPP FMILSP FMILYP FOCCP
## 1      0      0     0      0     0     0      0      0      0      0     0
## 2      0      0     0      0     0     0      0      0      0      0     0
## 3      0      0     0      0     0     0      0      0      0      0     0
## 4      0      0     0      0     0     0      0      0      0      0     0
## 5      0      0     0      0     0     0      0      0      0      0     0
## 6      0      0     0      0     0     0      1      0      0      0     0
##   FOIP FPAP FPOBP FPOWSP FRACP FRELP FRETP FSCHGP FSCHLP FSCHP FSEMP FSEXP
## 1    0    0     0      0     0     0     0      0      0     0     0     0
## 2    0    0     0      0     0     0     0      0      0     0     0     0
## 3    0    0     0      0     0     0     0      0      0     0     0     0
## 4    0    0     0      0     0     0     0      0      0     0     0     0
## 5    0    0     0      0     0     0     0      0      0     0     0     0
## 6    0    0     0      0     0     0     0      0      0     0     0     0
##   FSSIP FSSP FWAGP FWKHP FWKLP FWKWP FYOEP pwgtp1 pwgtp2 pwgtp3 pwgtp4
## 1     0    0     0     0     0     0     0     87     28    153     93
## 2     0    0     1     0     0     1     0     88     30    167     96
## 3     0    0     0     0     0     0     0     94     33    163    110
## 4     0    0     0     0     0     0     0     91     28    161    100
## 5     0    0     0     0     0     0     0    539    365    288    414
## 6     0    0     0     0     0     0     0    192     34    191    177
##   pwgtp5 pwgtp6 pwgtp7 pwgtp8 pwgtp9 pwgtp10 pwgtp11 pwgtp12 pwgtp13
## 1     26     26     95     93     93      92      87     163      91
## 2     27     25     95    100     99      90      91     164      92
## 3     33     29    119    112    109     110     101     184     103
## 4     28     26     98    106    106      98      88     162      90
## 5    573    293     86    245    450     456     334     352     417
## 6     84     96     31     33    180     118     111     115     188
##   pwgtp14 pwgtp15 pwgtp16 pwgtp17 pwgtp18 pwgtp19 pwgtp20 pwgtp21 pwgtp22
## 1      25     153      89     149      83      25     180      89      23
## 2      26     155      95     154      86      24     190      89      25
## 3      32     190     116     178      95      29     219     104      29
## 4      26     164     103     149      90      24     190      93      25
## 5     103     283     100     108     282     129     408     442     261
## 6     109      98     118      33     120     123      37     185      36
##   pwgtp23 pwgtp24 pwgtp25 pwgtp26 pwgtp27 pwgtp28 pwgtp29 pwgtp30 pwgtp31
## 1     139      91      24      26      87      82      86      90      90
## 2     142      96      26      30      88      85      92     100      94
## 3     182     118      32      35     106      98      97     104     105
## 4     145      95      25      27      88      82      90      90      93
## 5     349     237     383     333     124     367     481     458     336
## 6     178     179     110     105      30      29     200     130      92
##   pwgtp32 pwgtp33 pwgtp34 pwgtp35 pwgtp36 pwgtp37 pwgtp38 pwgtp39 pwgtp40
## 1     151      91      28     144      81     146      95      27      22
## 2     154      91      29     154      88     151      96      27      25
## 3     191     107      35     176     101     168     112      34      28
## 4     157      86      26     146      80     144      93      27      23
## 5     255     614     102     284     117      93     327     102     356
## 6     120     178     101     100     109      34      99     108      33
##   pwgtp41 pwgtp42 pwgtp43 pwgtp44 pwgtp45 pwgtp46 pwgtp47 pwgtp48 pwgtp49
## 1      89     173      27      84     153     149      93      89      91
## 2      93     163      29      83     156     153      96      90      91
## 3     100     184      38     109     192     174     125     113      95
## 4      92     160      28      85     156     148      96      99      90
## 5     106     256     326     290      96     346     571     268     117
## 6     176      36     172     175      99     103      31      37     160
##   pwgtp50 pwgtp51 pwgtp52 pwgtp53 pwgtp54 pwgtp55 pwgtp56 pwgtp57 pwgtp58
## 1      92      90      27      91     139      25      91      29      84
## 2      98      93      27      98     150      28      96      30      85
## 3     107     103      35     104     164      33     110      34      97
## 4      97      93      27     100     151      26      93      30      87
## 5     118     320     263     128     453     298     480     393     307
## 6     104      97     111     190     121     115     114      36     114
##   pwgtp59 pwgtp60 pwgtp61 pwgtp62 pwgtp63 pwgtp64 pwgtp65 pwgtp66 pwgtp67
## 1     149      30      94     140      24      90     147     148      93
## 2     152      30      98     144      24      92     161     163      97
## 3     188      40     110     176      34     113     190     186     107
## 4     144      33     101     152      23      95     148     149      92
## 5     480     282     117     347     323     377     106     239     386
## 6     104      29     189      35     180     172      96     112      28
##   pwgtp68 pwgtp69 pwgtp70 pwgtp71 pwgtp72 pwgtp73 pwgtp74 pwgtp75 pwgtp76
## 1      82      84      87      82      27      92     150      28      78
## 2      88      89      93      84      26      90     159      30      87
## 3      99     101     109      90      28      92     177      33     105
## 4      86      84      87      81      28      94     164      29      88
## 5     309      90      96     294     400      80     489     340     491
## 6      35     237      97     123     119     171     108      97     104
##   pwgtp77 pwgtp78 pwgtp79 pwgtp80
## 1      25      99     159     129
## 2      27      98     167     131
## 3      30     104     206     156
## 4      27     104     156     138
## 5     612     282     462     259
## 6      31     127     108      31
```


Carguemos el package y vemos que sacan las distintas propuestas 


```r
library(sqldf)
```

```
## Loading required package: gsubfn
```

```
## Warning: package 'gsubfn' was built under R version 3.1.1
```

```
## Loading required package: proto
## Loading required package: RSQLite
## Loading required package: DBI
```

```
## Warning: package 'DBI' was built under R version 3.1.1
```

```
## Loading required package: RSQLite.extfuns
```

```r

head(sqldf("select * from acs where AGEP < 50"))
```

```
## Loading required package: tcltk
```

```
##   RT SERIALNO SPORDER PUMA ST  ADJUST PWGTP AGEP CIT COW DDRS DEYE DOUT
## 1  P      186       1  700 16 1015675    89   43   1   7    2    2    2
## 2  P      186       2  700 16 1015675    92   42   1   4    2    2    2
## 3  P      186       3  700 16 1015675   107   16   1   1    2    2    2
## 4  P      186       4  700 16 1015675    91   14   1  NA    2    2   NA
## 5  P      306       1  700 16 1015675   309   29   1   5    2    2    2
## 6  P      395       1  100 16 1015675   108   40   1   8    2    2    2
##   DPHY DREM DWRK ENG FER GCL GCM GCR INTP JWMNP JWRIP JWTR LANX MAR MIG
## 1    2    2    2  NA  NA   2  NA  NA    0    15     1    1    2   1   1
## 2    2    2    2  NA   2   2  NA  NA    0    NA    NA   NA    2   1   1
## 3    2    2    2  NA  NA  NA  NA  NA    0     5     1    1    2   5   1
## 4    2    2   NA  NA  NA  NA  NA  NA   NA    NA    NA   NA    2   5   1
## 5    2    2    2  NA  NA  NA  NA  NA    0    50     8    1    2   5   1
## 6    2    2    2  NA   2   2  NA  NA    0     8     1    1    2   5   2
##   MIL MILY MLPA MLPB MLPC MLPD MLPE MLPF MLPG MLPH MLPI MLPJ MLPK NWAB
## 1   3    2    0    0    1    0    0    0    0    0    0    0    0    3
## 2   5   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA    2
## 3  NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA    3
## 4  NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA
## 5   2    2    1    0    0    0    0    0    0    0    0    0    0    3
## 6   5   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA    2
##   NWAV NWLA NWLK NWRE OIP PAP REL RETP SCH SCHG SCHL  SEMP SEX SSIP SSP
## 1    5    3    3    3   0   0   0    0   1   NA   10 50000   1    0   0
## 2    5    2    2    3   0   0   1    0   1   NA    9     0   2    0   0
## 3    5    3    3    3   0   0   2    0   3    5    7     0   1    0   0
## 4   NA   NA   NA   NA  NA  NA   2   NA   3    4    4    NA   2   NA  NA
## 5    5    3    3    3   0   0   0    0   1   NA   12     0   1    0   0
## 6    5    2    2    2   0   0   0    0   1   NA   13     0   2    0   0
##    WAGP WKHP WKL WKW YOEP UWRK ANC ANC1P ANC2P DECADE DRIVESP DS ESP ESR
## 1 50000   50   1  52   NA    1   2   920   148     NA       1  2  NA   1
## 2   800    4   1  20   NA    2   1   920   999     NA      NA  2  NA   6
## 3  4800   20   1  52   NA    1   2   920   148     NA       1  2   2   1
## 4    NA   NA  NA  NA   NA   NA   1   920   999     NA      NA  2   2  NA
## 5 34000   50   1  52   NA    1   2   902   920     NA       6  2  NA   1
## 6  9000   50   1  52   NA    1   2    82    22     NA       1  2  NA   1
##   HISP INDP JWAP JWDP LANP MIGPUMA MIGSP MSP NAICSP NATIVITY NOP OC OCCP
## 1    1 7690   88   46   NA      NA    NA   1  5617Z        1  NA  0 4200
## 2    1 7870   NA   NA   NA      NA    NA   1  611M1        1  NA  0 2340
## 3    1 8680  200  119   NA      NA    NA   6   722Z        1   1  1 4020
## 4    1   NA   NA   NA   NA      NA    NA  NA               1   1  1   NA
## 5    1 9590   72   23   NA      NA    NA   6   928P        1  NA  0 7140
## 6    1 5370  101   61   NA       1   215   6  45121        1  NA  0 4700
##   PAOC  PERNP  PINCP POBP POVPIP POWPUMA POWSP QTRBIR RAC1P RAC2P RAC3P
## 1   NA 100000 100000   53    501     600    16      3     1     1    69
## 2    2    800    800   41    501      NA    NA      3     1     1    69
## 3   NA   4800   4800   16    501     600    16      2     1     1    69
## 4   NA     NA     NA   41    501      NA    NA      4     1     1    69
## 5   NA  34000  34000   36    333     400    16      1     9    67    43
## 6    2   9000   9000   16     68     100    16      1     1     1    69
##   RACAIAN RACASN RACBLK RACNHPI RACNUM RACSOR RACWHT RC SFN SFR   SOCP VPS
## 1       0      0      0       0      1      0      1  0  NA  NA 371011   9
## 2       0      0      0       0      1      0      1  0  NA  NA 253000  NA
## 3       0      0      0       0      1      0      1  1  NA  NA 352010  NA
## 4       0      0      0       0      1      0      1  1  NA  NA         NA
## 5       1      0      1       0      2      0      0  0  NA  NA 493011   1
## 6       0      0      0       0      1      0      1  0  NA  NA 411011  NA
##   WAOB FAGEP FANCP FCITP FCOWP FDDRSP FDEYEP FDOUTP FDPHYP FDREMP FDWRKP
## 1    1     0     0     0     0      0      0      0      0      0      0
## 2    1     0     0     0     0      0      0      0      0      0      0
## 3    1     0     0     0     0      0      0      0      0      0      0
## 4    1     0     0     0     0      0      0      0      0      0      0
## 5    1     0     0     0     0      0      0      0      0      0      0
## 6    1     0     0     0     0      0      0      0      0      0      0
##   FENGP FESRP FFERP FGCLP FGCMP FGCRP FHISP FINDP FINTP FJWDP FJWMNP
## 1     0     0     0     0     0     0     0     0     0     0      0
## 2     0     0     0     0     0     0     0     0     0     0      0
## 3     0     0     0     0     0     0     0     0     0     0      0
## 4     0     0     0     0     0     0     0     0     0     0      0
## 5     0     0     0     0     0     0     0     0     0     0      0
## 6     0     0     1     0     0     0     0     0     0     0      0
##   FJWRIP FJWTRP FLANP FLANXP FMARP FMIGP FMIGSP FMILPP FMILSP FMILYP FOCCP
## 1      0      0     0      0     0     0      0      0      0      0     0
## 2      0      0     0      0     0     0      0      0      0      0     0
## 3      0      0     0      0     0     0      0      0      0      0     0
## 4      0      0     0      0     0     0      0      0      0      0     0
## 5      0      0     0      0     0     0      0      0      0      0     0
## 6      0      0     0      0     0     0      1      0      0      0     0
##   FOIP FPAP FPOBP FPOWSP FRACP FRELP FRETP FSCHGP FSCHLP FSCHP FSEMP FSEXP
## 1    0    0     0      0     0     0     0      0      0     0     0     0
## 2    0    0     0      0     0     0     0      0      0     0     0     0
## 3    0    0     0      0     0     0     0      0      0     0     0     0
## 4    0    0     0      0     0     0     0      0      0     0     0     0
## 5    0    0     0      0     0     0     0      0      0     0     0     0
## 6    0    0     0      0     0     0     0      0      0     0     0     0
##   FSSIP FSSP FWAGP FWKHP FWKLP FWKWP FYOEP pwgtp1 pwgtp2 pwgtp3 pwgtp4
## 1     0    0     0     0     0     0     0     87     28    153     93
## 2     0    0     1     0     0     1     0     88     30    167     96
## 3     0    0     0     0     0     0     0     94     33    163    110
## 4     0    0     0     0     0     0     0     91     28    161    100
## 5     0    0     0     0     0     0     0    539    365    288    414
## 6     0    0     0     0     0     0     0    192     34    191    177
##   pwgtp5 pwgtp6 pwgtp7 pwgtp8 pwgtp9 pwgtp10 pwgtp11 pwgtp12 pwgtp13
## 1     26     26     95     93     93      92      87     163      91
## 2     27     25     95    100     99      90      91     164      92
## 3     33     29    119    112    109     110     101     184     103
## 4     28     26     98    106    106      98      88     162      90
## 5    573    293     86    245    450     456     334     352     417
## 6     84     96     31     33    180     118     111     115     188
##   pwgtp14 pwgtp15 pwgtp16 pwgtp17 pwgtp18 pwgtp19 pwgtp20 pwgtp21 pwgtp22
## 1      25     153      89     149      83      25     180      89      23
## 2      26     155      95     154      86      24     190      89      25
## 3      32     190     116     178      95      29     219     104      29
## 4      26     164     103     149      90      24     190      93      25
## 5     103     283     100     108     282     129     408     442     261
## 6     109      98     118      33     120     123      37     185      36
##   pwgtp23 pwgtp24 pwgtp25 pwgtp26 pwgtp27 pwgtp28 pwgtp29 pwgtp30 pwgtp31
## 1     139      91      24      26      87      82      86      90      90
## 2     142      96      26      30      88      85      92     100      94
## 3     182     118      32      35     106      98      97     104     105
## 4     145      95      25      27      88      82      90      90      93
## 5     349     237     383     333     124     367     481     458     336
## 6     178     179     110     105      30      29     200     130      92
##   pwgtp32 pwgtp33 pwgtp34 pwgtp35 pwgtp36 pwgtp37 pwgtp38 pwgtp39 pwgtp40
## 1     151      91      28     144      81     146      95      27      22
## 2     154      91      29     154      88     151      96      27      25
## 3     191     107      35     176     101     168     112      34      28
## 4     157      86      26     146      80     144      93      27      23
## 5     255     614     102     284     117      93     327     102     356
## 6     120     178     101     100     109      34      99     108      33
##   pwgtp41 pwgtp42 pwgtp43 pwgtp44 pwgtp45 pwgtp46 pwgtp47 pwgtp48 pwgtp49
## 1      89     173      27      84     153     149      93      89      91
## 2      93     163      29      83     156     153      96      90      91
## 3     100     184      38     109     192     174     125     113      95
## 4      92     160      28      85     156     148      96      99      90
## 5     106     256     326     290      96     346     571     268     117
## 6     176      36     172     175      99     103      31      37     160
##   pwgtp50 pwgtp51 pwgtp52 pwgtp53 pwgtp54 pwgtp55 pwgtp56 pwgtp57 pwgtp58
## 1      92      90      27      91     139      25      91      29      84
## 2      98      93      27      98     150      28      96      30      85
## 3     107     103      35     104     164      33     110      34      97
## 4      97      93      27     100     151      26      93      30      87
## 5     118     320     263     128     453     298     480     393     307
## 6     104      97     111     190     121     115     114      36     114
##   pwgtp59 pwgtp60 pwgtp61 pwgtp62 pwgtp63 pwgtp64 pwgtp65 pwgtp66 pwgtp67
## 1     149      30      94     140      24      90     147     148      93
## 2     152      30      98     144      24      92     161     163      97
## 3     188      40     110     176      34     113     190     186     107
## 4     144      33     101     152      23      95     148     149      92
## 5     480     282     117     347     323     377     106     239     386
## 6     104      29     189      35     180     172      96     112      28
##   pwgtp68 pwgtp69 pwgtp70 pwgtp71 pwgtp72 pwgtp73 pwgtp74 pwgtp75 pwgtp76
## 1      82      84      87      82      27      92     150      28      78
## 2      88      89      93      84      26      90     159      30      87
## 3      99     101     109      90      28      92     177      33     105
## 4      86      84      87      81      28      94     164      29      88
## 5     309      90      96     294     400      80     489     340     491
## 6      35     237      97     123     119     171     108      97     104
##   pwgtp77 pwgtp78 pwgtp79 pwgtp80
## 1      25      99     159     129
## 2      27      98     167     131
## 3      30     104     206     156
## 4      27     104     156     138
## 5     612     282     462     259
## 6      31     127     108      31
```

```r
head(sqldf("select pwgtp1 from acs where AGEP < 50"))
```

```
##   pwgtp1
## 1     87
## 2     88
## 3     94
## 4     91
## 5    539
## 6    192
```

```r
head(sqldf("select * from acs"))
```

```
##   RT SERIALNO SPORDER PUMA ST  ADJUST PWGTP AGEP CIT COW DDRS DEYE DOUT
## 1  P      186       1  700 16 1015675    89   43   1   7    2    2    2
## 2  P      186       2  700 16 1015675    92   42   1   4    2    2    2
## 3  P      186       3  700 16 1015675   107   16   1   1    2    2    2
## 4  P      186       4  700 16 1015675    91   14   1  NA    2    2   NA
## 5  P      306       1  700 16 1015675   309   29   1   5    2    2    2
## 6  P      395       1  100 16 1015675   108   40   1   8    2    2    2
##   DPHY DREM DWRK ENG FER GCL GCM GCR INTP JWMNP JWRIP JWTR LANX MAR MIG
## 1    2    2    2  NA  NA   2  NA  NA    0    15     1    1    2   1   1
## 2    2    2    2  NA   2   2  NA  NA    0    NA    NA   NA    2   1   1
## 3    2    2    2  NA  NA  NA  NA  NA    0     5     1    1    2   5   1
## 4    2    2   NA  NA  NA  NA  NA  NA   NA    NA    NA   NA    2   5   1
## 5    2    2    2  NA  NA  NA  NA  NA    0    50     8    1    2   5   1
## 6    2    2    2  NA   2   2  NA  NA    0     8     1    1    2   5   2
##   MIL MILY MLPA MLPB MLPC MLPD MLPE MLPF MLPG MLPH MLPI MLPJ MLPK NWAB
## 1   3    2    0    0    1    0    0    0    0    0    0    0    0    3
## 2   5   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA    2
## 3  NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA    3
## 4  NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA
## 5   2    2    1    0    0    0    0    0    0    0    0    0    0    3
## 6   5   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA    2
##   NWAV NWLA NWLK NWRE OIP PAP REL RETP SCH SCHG SCHL  SEMP SEX SSIP SSP
## 1    5    3    3    3   0   0   0    0   1   NA   10 50000   1    0   0
## 2    5    2    2    3   0   0   1    0   1   NA    9     0   2    0   0
## 3    5    3    3    3   0   0   2    0   3    5    7     0   1    0   0
## 4   NA   NA   NA   NA  NA  NA   2   NA   3    4    4    NA   2   NA  NA
## 5    5    3    3    3   0   0   0    0   1   NA   12     0   1    0   0
## 6    5    2    2    2   0   0   0    0   1   NA   13     0   2    0   0
##    WAGP WKHP WKL WKW YOEP UWRK ANC ANC1P ANC2P DECADE DRIVESP DS ESP ESR
## 1 50000   50   1  52   NA    1   2   920   148     NA       1  2  NA   1
## 2   800    4   1  20   NA    2   1   920   999     NA      NA  2  NA   6
## 3  4800   20   1  52   NA    1   2   920   148     NA       1  2   2   1
## 4    NA   NA  NA  NA   NA   NA   1   920   999     NA      NA  2   2  NA
## 5 34000   50   1  52   NA    1   2   902   920     NA       6  2  NA   1
## 6  9000   50   1  52   NA    1   2    82    22     NA       1  2  NA   1
##   HISP INDP JWAP JWDP LANP MIGPUMA MIGSP MSP NAICSP NATIVITY NOP OC OCCP
## 1    1 7690   88   46   NA      NA    NA   1  5617Z        1  NA  0 4200
## 2    1 7870   NA   NA   NA      NA    NA   1  611M1        1  NA  0 2340
## 3    1 8680  200  119   NA      NA    NA   6   722Z        1   1  1 4020
## 4    1   NA   NA   NA   NA      NA    NA  NA               1   1  1   NA
## 5    1 9590   72   23   NA      NA    NA   6   928P        1  NA  0 7140
## 6    1 5370  101   61   NA       1   215   6  45121        1  NA  0 4700
##   PAOC  PERNP  PINCP POBP POVPIP POWPUMA POWSP QTRBIR RAC1P RAC2P RAC3P
## 1   NA 100000 100000   53    501     600    16      3     1     1    69
## 2    2    800    800   41    501      NA    NA      3     1     1    69
## 3   NA   4800   4800   16    501     600    16      2     1     1    69
## 4   NA     NA     NA   41    501      NA    NA      4     1     1    69
## 5   NA  34000  34000   36    333     400    16      1     9    67    43
## 6    2   9000   9000   16     68     100    16      1     1     1    69
##   RACAIAN RACASN RACBLK RACNHPI RACNUM RACSOR RACWHT RC SFN SFR   SOCP VPS
## 1       0      0      0       0      1      0      1  0  NA  NA 371011   9
## 2       0      0      0       0      1      0      1  0  NA  NA 253000  NA
## 3       0      0      0       0      1      0      1  1  NA  NA 352010  NA
## 4       0      0      0       0      1      0      1  1  NA  NA         NA
## 5       1      0      1       0      2      0      0  0  NA  NA 493011   1
## 6       0      0      0       0      1      0      1  0  NA  NA 411011  NA
##   WAOB FAGEP FANCP FCITP FCOWP FDDRSP FDEYEP FDOUTP FDPHYP FDREMP FDWRKP
## 1    1     0     0     0     0      0      0      0      0      0      0
## 2    1     0     0     0     0      0      0      0      0      0      0
## 3    1     0     0     0     0      0      0      0      0      0      0
## 4    1     0     0     0     0      0      0      0      0      0      0
## 5    1     0     0     0     0      0      0      0      0      0      0
## 6    1     0     0     0     0      0      0      0      0      0      0
##   FENGP FESRP FFERP FGCLP FGCMP FGCRP FHISP FINDP FINTP FJWDP FJWMNP
## 1     0     0     0     0     0     0     0     0     0     0      0
## 2     0     0     0     0     0     0     0     0     0     0      0
## 3     0     0     0     0     0     0     0     0     0     0      0
## 4     0     0     0     0     0     0     0     0     0     0      0
## 5     0     0     0     0     0     0     0     0     0     0      0
## 6     0     0     1     0     0     0     0     0     0     0      0
##   FJWRIP FJWTRP FLANP FLANXP FMARP FMIGP FMIGSP FMILPP FMILSP FMILYP FOCCP
## 1      0      0     0      0     0     0      0      0      0      0     0
## 2      0      0     0      0     0     0      0      0      0      0     0
## 3      0      0     0      0     0     0      0      0      0      0     0
## 4      0      0     0      0     0     0      0      0      0      0     0
## 5      0      0     0      0     0     0      0      0      0      0     0
## 6      0      0     0      0     0     0      1      0      0      0     0
##   FOIP FPAP FPOBP FPOWSP FRACP FRELP FRETP FSCHGP FSCHLP FSCHP FSEMP FSEXP
## 1    0    0     0      0     0     0     0      0      0     0     0     0
## 2    0    0     0      0     0     0     0      0      0     0     0     0
## 3    0    0     0      0     0     0     0      0      0     0     0     0
## 4    0    0     0      0     0     0     0      0      0     0     0     0
## 5    0    0     0      0     0     0     0      0      0     0     0     0
## 6    0    0     0      0     0     0     0      0      0     0     0     0
##   FSSIP FSSP FWAGP FWKHP FWKLP FWKWP FYOEP pwgtp1 pwgtp2 pwgtp3 pwgtp4
## 1     0    0     0     0     0     0     0     87     28    153     93
## 2     0    0     1     0     0     1     0     88     30    167     96
## 3     0    0     0     0     0     0     0     94     33    163    110
## 4     0    0     0     0     0     0     0     91     28    161    100
## 5     0    0     0     0     0     0     0    539    365    288    414
## 6     0    0     0     0     0     0     0    192     34    191    177
##   pwgtp5 pwgtp6 pwgtp7 pwgtp8 pwgtp9 pwgtp10 pwgtp11 pwgtp12 pwgtp13
## 1     26     26     95     93     93      92      87     163      91
## 2     27     25     95    100     99      90      91     164      92
## 3     33     29    119    112    109     110     101     184     103
## 4     28     26     98    106    106      98      88     162      90
## 5    573    293     86    245    450     456     334     352     417
## 6     84     96     31     33    180     118     111     115     188
##   pwgtp14 pwgtp15 pwgtp16 pwgtp17 pwgtp18 pwgtp19 pwgtp20 pwgtp21 pwgtp22
## 1      25     153      89     149      83      25     180      89      23
## 2      26     155      95     154      86      24     190      89      25
## 3      32     190     116     178      95      29     219     104      29
## 4      26     164     103     149      90      24     190      93      25
## 5     103     283     100     108     282     129     408     442     261
## 6     109      98     118      33     120     123      37     185      36
##   pwgtp23 pwgtp24 pwgtp25 pwgtp26 pwgtp27 pwgtp28 pwgtp29 pwgtp30 pwgtp31
## 1     139      91      24      26      87      82      86      90      90
## 2     142      96      26      30      88      85      92     100      94
## 3     182     118      32      35     106      98      97     104     105
## 4     145      95      25      27      88      82      90      90      93
## 5     349     237     383     333     124     367     481     458     336
## 6     178     179     110     105      30      29     200     130      92
##   pwgtp32 pwgtp33 pwgtp34 pwgtp35 pwgtp36 pwgtp37 pwgtp38 pwgtp39 pwgtp40
## 1     151      91      28     144      81     146      95      27      22
## 2     154      91      29     154      88     151      96      27      25
## 3     191     107      35     176     101     168     112      34      28
## 4     157      86      26     146      80     144      93      27      23
## 5     255     614     102     284     117      93     327     102     356
## 6     120     178     101     100     109      34      99     108      33
##   pwgtp41 pwgtp42 pwgtp43 pwgtp44 pwgtp45 pwgtp46 pwgtp47 pwgtp48 pwgtp49
## 1      89     173      27      84     153     149      93      89      91
## 2      93     163      29      83     156     153      96      90      91
## 3     100     184      38     109     192     174     125     113      95
## 4      92     160      28      85     156     148      96      99      90
## 5     106     256     326     290      96     346     571     268     117
## 6     176      36     172     175      99     103      31      37     160
##   pwgtp50 pwgtp51 pwgtp52 pwgtp53 pwgtp54 pwgtp55 pwgtp56 pwgtp57 pwgtp58
## 1      92      90      27      91     139      25      91      29      84
## 2      98      93      27      98     150      28      96      30      85
## 3     107     103      35     104     164      33     110      34      97
## 4      97      93      27     100     151      26      93      30      87
## 5     118     320     263     128     453     298     480     393     307
## 6     104      97     111     190     121     115     114      36     114
##   pwgtp59 pwgtp60 pwgtp61 pwgtp62 pwgtp63 pwgtp64 pwgtp65 pwgtp66 pwgtp67
## 1     149      30      94     140      24      90     147     148      93
## 2     152      30      98     144      24      92     161     163      97
## 3     188      40     110     176      34     113     190     186     107
## 4     144      33     101     152      23      95     148     149      92
## 5     480     282     117     347     323     377     106     239     386
## 6     104      29     189      35     180     172      96     112      28
##   pwgtp68 pwgtp69 pwgtp70 pwgtp71 pwgtp72 pwgtp73 pwgtp74 pwgtp75 pwgtp76
## 1      82      84      87      82      27      92     150      28      78
## 2      88      89      93      84      26      90     159      30      87
## 3      99     101     109      90      28      92     177      33     105
## 4      86      84      87      81      28      94     164      29      88
## 5     309      90      96     294     400      80     489     340     491
## 6      35     237      97     123     119     171     108      97     104
##   pwgtp77 pwgtp78 pwgtp79 pwgtp80
## 1      25      99     159     129
## 2      27      98     167     131
## 3      30     104     206     156
## 4      27     104     156     138
## 5     612     282     462     259
## 6      31     127     108      31
```

```r
head(sqldf("select pwgtp1 from acs"))
```

```
##   pwgtp1
## 1     87
## 2     88
## 3     94
## 4     91
## 5    539
## 6    192
```


En este caso es claro que es la respuesta que solo saca una columna, y desde luego la cuarta no puede ser  (he puesto unos heads por que si no es infumable)

### Question 3

Using the same data frame you created in the previous problem, what is the equivalent function to unique(acs$AGEP)
sqldf("select unique AGEP from acs")
sqldf("select distinct AGEP from acs")
sqldf("select distinct pwgtp1 from acs")
sqldf("select unique * from acs")


y simplemente corremos las 5 posibilidades

```r
unique(acs$AGEP)
```

```
##  [1] 43 42 16 14 29 40 15 28 30  4  1 18 37 39  3 87 70 49 45 50 60 59 61
## [24] 64 35 12 19 31  9  0 33 32 20 88 53 58 69 68 48 24 27 74 56 75 17 38
## [47] 55 26 23 86 81 77  7 51 13 11 82 47 46 80 21 54 78 67 22  2 76  6 71
## [70] 34 10  5 65 62 63 57 52 79 83 66 25 93  8 36 41 44 84 72 73 85 89
```

```r
sqldf("select unique AGEP from acs")
```

```
## Error: RS-DBI driver: (error in statement: near "unique": syntax error)
```

```r
sqldf("select distinct AGEP from acs")
```

```
##    AGEP
## 1    43
## 2    42
## 3    16
## 4    14
## 5    29
## 6    40
## 7    15
## 8    28
## 9    30
## 10    4
## 11    1
## 12   18
## 13   37
## 14   39
## 15    3
## 16   87
## 17   70
## 18   49
## 19   45
## 20   50
## 21   60
## 22   59
## 23   61
## 24   64
## 25   35
## 26   12
## 27   19
## 28   31
## 29    9
## 30    0
## 31   33
## 32   32
## 33   20
## 34   88
## 35   53
## 36   58
## 37   69
## 38   68
## 39   48
## 40   24
## 41   27
## 42   74
## 43   56
## 44   75
## 45   17
## 46   38
## 47   55
## 48   26
## 49   23
## 50   86
## 51   81
## 52   77
## 53    7
## 54   51
## 55   13
## 56   11
## 57   82
## 58   47
## 59   46
## 60   80
## 61   21
## 62   54
## 63   78
## 64   67
## 65   22
## 66    2
## 67   76
## 68    6
## 69   71
## 70   34
## 71   10
## 72    5
## 73   65
## 74   62
## 75   63
## 76   57
## 77   52
## 78   79
## 79   83
## 80   66
## 81   25
## 82   93
## 83    8
## 84   36
## 85   41
## 86   44
## 87   84
## 88   72
## 89   73
## 90   85
## 91   89
```

```r
sqldf("select distinct pwgtp1 from acs")
```

```
##     pwgtp1
## 1       87
## 2       88
## 3       94
## 4       91
## 5      539
## 6      192
## 7      153
## 8      232
## 9      205
## 10     226
## 11     225
## 12     109
## 13     129
## 14     115
## 15     162
## 16     190
## 17     185
## 18     186
## 19      26
## 20      28
## 21     157
## 22      15
## 23      36
## 24     234
## 25     307
## 26      71
## 27      78
## 28      18
## 29      43
## 30     137
## 31      99
## 32      49
## 33      69
## 34      70
## 35      92
## 36     144
## 37     402
## 38     650
## 39     545
## 40     687
## 41      27
## 42      21
## 43     108
## 44     293
## 45     352
## 46      38
## 47     113
## 48     122
## 49      19
## 50      25
## 51      16
## 52      12
## 53      57
## 54     117
## 55     311
## 56     419
## 57     106
## 58       4
## 59       3
## 60     204
## 61     189
## 62     256
## 63     177
## 64     136
## 65     118
## 66      83
## 67      24
## 68     101
## 69       5
## 70     172
## 71     194
## 72      48
## 73      62
## 74      42
## 75      80
## 76      51
## 77      63
## 78      65
## 79      67
## 80     140
## 81     159
## 82     227
## 83     179
## 84      66
## 85      72
## 86     121
## 87      96
## 88     221
## 89     102
## 90      82
## 91      31
## 92       9
## 93       7
## 94     111
## 95     110
## 96     105
## 97     112
## 98      76
## 99      46
## 100     45
## 101     44
## 102     39
## 103     59
## 104     34
## 105    127
## 106    131
## 107     74
## 108     73
## 109     55
## 110     23
## 111     29
## 112    142
## 113    214
## 114     89
## 115    203
## 116    152
## 117     32
## 118     41
## 119     47
## 120    114
## 121     30
## 122     58
## 123     37
## 124     22
## 125    246
## 126    264
## 127    242
## 128    262
## 129    361
## 130    235
## 131     35
## 132     56
## 133    103
## 134     79
## 135    229
## 136    188
## 137    107
## 138    160
## 139     50
## 140     20
## 141    120
## 142    199
## 143    171
## 144    166
## 145     33
## 146     17
## 147    147
## 148     95
## 149     68
## 150    412
## 151      8
## 152    100
## 153     64
## 154    104
## 155    124
## 156     40
## 157     81
## 158     86
## 159     93
## 160    173
## 161     84
## 162     52
## 163     61
## 164     77
## 165      6
## 166    156
## 167    146
## 168    128
## 169    180
## 170    302
## 171    211
## 172    301
## 173    298
## 174    501
## 175    201
## 176    285
## 177    292
## 178    126
## 179    130
## 180    206
## 181    261
## 182    243
## 183    176
## 184    224
## 185    167
## 186     98
## 187    158
## 188    141
## 189    371
## 190    400
## 191    415
## 192    248
## 193    249
## 194    681
## 195    559
## 196    509
## 197    119
## 198    327
## 199    268
## 200    270
## 201    269
## 202    337
## 203    485
## 204    252
## 205    161
## 206     54
## 207     10
## 208     60
## 209    182
## 210    139
## 211     85
## 212    145
## 213    125
## 214    191
## 215    228
## 216    230
## 217    123
## 218     14
## 219    312
## 220    318
## 221    331
## 222    263
## 223    209
## 224    169
## 225    294
## 226    181
## 227    414
## 228    324
## 229    132
## 230    183
## 231     53
## 232    265
## 233    210
## 234    196
## 235    219
## 236    175
## 237    148
## 238    332
## 239    233
## 240    155
## 241    479
## 242    244
## 243    237
## 244    154
## 245    149
## 246    396
## 247    165
## 248    245
## 249    239
## 250    483
## 251     75
## 252    195
## 253    193
## 254    138
## 255    134
## 256     13
## 257    280
## 258    207
## 259     90
## 260    174
## 261    215
## 262    257
## 263    394
## 264    541
## 265    386
## 266    406
## 267    370
## 268    133
## 269     97
## 270    613
## 271    170
## 272    200
## 273    345
## 274    303
## 275    380
## 276    314
## 277    218
## 278     11
## 279    271
## 280    197
## 281    150
## 282    305
## 283    238
## 284    326
## 285    508
## 286    236
## 287    116
## 288    621
## 289    168
## 290    222
## 291    202
## 292    187
## 293    178
## 294    216
## 295    347
## 296    277
## 297    338
## 298    151
## 299    350
## 300    308
## 301    383
## 302    259
## 303    392
## 304    255
## 305    231
## 306    421
## 307    184
## 308    473
## 309    220
## 310    272
## 311    247
## 312    286
## 313    279
## 314    163
## 315    217
## 316    212
## 317    283
## 318    240
## 319    378
## 320    290
## 321    450
## 322    609
## 323    616
## 324    443
## 325    790
## 326    135
## 327    260
## 328    164
## 329    241
## 330    892
## 331    423
## 332    267
## 333    456
## 334    476
## 335    223
## 336    561
## 337    689
## 338    416
## 339    198
## 340    382
## 341    375
## 342    367
## 343    351
## 344    404
## 345    296
## 346    395
## 347    288
## 348    349
## 349    487
## 350    143
## 351    470
## 352    446
## 353    299
## 354    323
## 355    276
## 356    379
## 357    557
## 358    300
## 359    403
## 360    492
## 361    320
## 362    295
## 363    471
## 364    258
## 365    356
## 366    251
## 367    372
## 368    325
## 369    791
## 370    322
## 371    638
## 372    507
## 373    329
## 374    282
## 375    427
## 376    297
## 377    348
## 378    284
## 379    343
## 380    434
## 381    511
## 382    363
## 383    213
## 384    651
## 385    460
## 386    266
## 387    316
## 388    697
## 389    524
## 390    409
## 391    533
## 392    534
## 393    448
## 394    468
## 395    498
## 396    408
## 397    563
## 398    321
## 399    357
## 400    399
## 401    355
## 402    930
## 403    437
## 404    369
## 405    358
## 406    304
## 407    340
## 408    330
## 409    417
## 410    373
## 411    407
## 412    464
## 413    353
## 414    478
## 415    535
## 416    362
## 417    529
## 418    458
## 419    518
## 420    275
## 421    278
## 422    208
## 423    454
## 424    334
## 425    447
## 426    401
## 427    281
## 428    546
## 429    549
## 430    455
## 431    317
## 432    574
## 433    700
## 434    591
## 435    435
## 436    564
## 437    595
## 438    761
## 439    493
## 440    422
## 441    313
## 442    640
## 443    413
## 444    480
## 445    319
## 446    391
## 447    528
## 448    596
## 449    773
## 450    418
## 451    593
## 452    291
## 453    364
## 454    287
## 455    684
## 456    273
## 457    377
## 458    424
## 459    376
## 460      1
## 461    678
## 462    466
## 463    514
## 464    512
## 465    715
## 466    566
## 467    359
## 468    603
## 469    381
## 470    393
## 471    475
## 472    398
## 473    489
## 474    482
## 475    250
## 476    405
## 477    274
## 478    385
## 479    481
## 480    459
## 481    333
## 482    504
## 483    467
## 484    589
## 485    720
## 486    585
## 487    530
## 488    703
## 489    315
## 490    712
## 491    565
## 492    390
## 493    430
## 494    374
## 495    254
## 496    618
## 497    387
## 498    779
## 499    339
## 500    389
## 501    544
## 502    342
## 503    354
## 504    488
## 505    253
## 506    525
## 507    410
## 508    310
## 509    598
## 510    452
## 511    521
## 512    306
## 513    576
## 514    605
## 515    769
## 516    625
## 517    612
## 518    341
## 519    439
## 520      2
## 521    309
## 522    680
## 523    517
## 524    820
## 525    335
## 526    360
## 527    429
## 528    752
## 529    792
## 530    587
## 531    502
## 532    436
## 533    674
## 534    336
## 535    626
## 536    453
## 537    289
## 538    606
## 539    426
## 540    573
## 541    433
## 542    550
## 543    366
## 544    499
## 545    907
## 546    515
## 547    438
## 548    599
## 549    451
## 550    770
## 551    604
## 552    463
## 553    397
```

```r
sqldf("select unique * from acs")
```

```
## Error: RS-DBI driver: (error in statement: near "unique": syntax error)
```


Y aqui comparamos y quitamos los que tienen error
