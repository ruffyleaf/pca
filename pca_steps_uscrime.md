Principal Component Analysis of uscrime.csv
========================================================

Data Exploration and Data Preparation
-----

```r
# Read in the data into a dataframe
uscrime <- read.csv("uscrime.csv")

# Display the first few entries
head(uscrime)
```

```
##   state  land popu murd rape robb assa burg larc auto reg div
## 1    ME 33265 1164  1.5  7.0 12.6   62  562 1055  146   1   1
## 2    NH  9279  998  2.0  6.0 12.1   36  566  929  172   1   1
## 3    VT  9614  535  1.3 10.3  7.6   55  731  969  124   1   1
## 4    MA  8284 5822  3.5 12.0 99.5   88 1134 1531  878   1   1
## 5    RI  1212  968  3.2  3.6 78.3  120 1019 2186  859   1   1
## 6    CT  5018 3174  3.5  9.1 70.4   87 1084 1751  484   1   1
```

```r

# Display the structure of the data
str(uscrime)
```

```
## 'data.frame':	50 obs. of  12 variables:
##  $ state: Factor w/ 50 levels "AK","AL","AR",..: 21 30 46 19 39 7 34 31 38 35 ...
##  $ land : int  33265 9279 9614 8284 1212 5018 49108 7787 45308 41330 ...
##  $ popu : int  1164 998 535 5822 968 3174 17783 7562 11853 10744 ...
##  $ murd : num  1.5 2 1.3 3.5 3.2 3.5 7.9 5.7 5.3 6.6 ...
##  $ rape : num  7 6 10.3 12 3.6 9.1 15.5 12.9 11.3 16 ...
##  $ robb : num  12.6 12.1 7.6 99.5 78.3 ...
##  $ assa : int  62 36 55 88 120 87 209 90 90 116 ...
##  $ burg : int  562 566 731 1134 1019 1084 1414 1041 594 854 ...
##  $ larc : int  1055 929 969 1531 2186 1751 2025 1689 1001 1944 ...
##  $ auto : int  146 172 124 878 859 484 682 557 340 493 ...
##  $ reg  : int  1 1 1 1 1 1 1 1 1 2 ...
##  $ div  : int  1 1 1 1 1 1 2 2 2 3 ...
```

```r

# Summary of the data
summary(uscrime)
```

```
##      state         land             popu            murd      
##  AK     : 1   Min.   :  1212   Min.   :  509   Min.   : 0.50  
##  AL     : 1   1st Qu.: 37241   1st Qu.: 1236   1st Qu.: 3.50  
##  AR     : 1   Median : 56214   Median : 3266   Median : 6.20  
##  AZ     : 1   Mean   : 72374   Mean   : 4762   Mean   : 6.86  
##  CA     : 1   3rd Qu.: 83242   3rd Qu.: 5654   3rd Qu.: 9.57  
##  CO     : 1   Max.   :591004   Max.   :26365   Max.   :15.30  
##  (Other):44                                                   
##       rape           robb            assa            burg     
##  Min.   : 3.6   Min.   :  6.5   Min.   : 21.0   Min.   : 286  
##  1st Qu.:10.3   1st Qu.: 46.8   1st Qu.: 84.5   1st Qu.: 682  
##  Median :14.9   Median : 76.7   Median :125.0   Median : 871  
##  Mean   :15.6   Mean   :101.5   Mean   :135.4   Mean   : 931  
##  3rd Qu.:19.4   3rd Qu.:126.9   3rd Qu.:191.5   3rd Qu.:1140  
##  Max.   :36.0   Max.   :443.3   Max.   :293.0   Max.   :1753  
##                                                               
##       larc           auto          reg            div      
##  Min.   : 694   Min.   : 78   Min.   :1.00   Min.   :1.00  
##  1st Qu.:1424   1st Qu.:219   1st Qu.:2.00   1st Qu.:3.00  
##  Median :1923   Median :343   Median :3.00   Median :5.00  
##  Mean   :1944   Mean   :368   Mean   :2.66   Mean   :5.12  
##  3rd Qu.:2316   3rd Qu.:514   3rd Qu.:3.75   3rd Qu.:7.75  
##  Max.   :3550   Max.   :878   Max.   :4.00   Max.   :9.00  
## 
```

```r

# Check for missing values
sum(complete.cases(uscrime))
```

```
## [1] 50
```

```r

# Keep the complete cases only
uscrime <- uscrime[complete.cases(uscrime), ]
```


Preparing for factorization
---------
1. We prepare the variables for factorization
2. Analyse the factorability using Correlation, significance and also the sampling adequacy


```r
# We want to factorize only the variables that make some sense
uscrimepc <- uscrime[, c(4:10)]

library(Hmisc)
```

```
## Loading required package: grid
## Loading required package: lattice
## Loading required package: survival
## Loading required package: splines
## Loading required package: Formula
## 
## Attaching package: 'Hmisc'
## 
## The following objects are masked from 'package:base':
## 
##     format.pval, round.POSIXt, trunc.POSIXt, units
```

```r

# Analyse the Variables Correlation and Significance
rcorr(as.matrix(uscrimepc))
```

```
##      murd rape robb assa burg larc auto
## murd 1.00 0.52 0.34 0.81 0.28 0.06 0.11
## rape 0.52 1.00 0.55 0.70 0.68 0.60 0.44
## robb 0.34 0.55 1.00 0.56 0.62 0.44 0.62
## assa 0.81 0.70 0.56 1.00 0.52 0.32 0.33
## burg 0.28 0.68 0.62 0.52 1.00 0.80 0.70
## larc 0.06 0.60 0.44 0.32 0.80 1.00 0.55
## auto 0.11 0.44 0.62 0.33 0.70 0.55 1.00
## 
## n= 50 
## 
## 
## P
##      murd   rape   robb   assa   burg   larc   auto  
## murd        0.0001 0.0154 0.0000 0.0517 0.6549 0.4477
## rape 0.0001        0.0000 0.0000 0.0000 0.0000 0.0014
## robb 0.0154 0.0000        0.0000 0.0000 0.0015 0.0000
## assa 0.0000 0.0000 0.0000        0.0001 0.0250 0.0191
## burg 0.0517 0.0000 0.0000 0.0001        0.0000 0.0000
## larc 0.6549 0.0000 0.0015 0.0250 0.0000        0.0000
## auto 0.4477 0.0014 0.0000 0.0191 0.0000 0.0000
```

```r

# Check the Kaiser-Meyer-Olkin factor adequacy Values above 0.5 are
# considered adequate.
library(psych)
```

```
## 
## Attaching package: 'psych'
## 
## The following object is masked from 'package:Hmisc':
## 
##     describe
```

```r
KMO(uscrimepc)
```

```
## Kaiser-Meyer-Olkin factor adequacy
## Call: KMO(r = uscrimepc)
## Overall MSA =  0.79
## MSA for each item = 
## murd rape robb assa burg larc auto 
## 0.65 0.90 0.87 0.74 0.80 0.75 0.84
```

```r

# Using Bartlett's test to check if the Correlation Matrix is an Identity
# matrix. If the p-value is low, then we can reject the null hypothesis that
# the Correlation Matrix is an Identity matrix.
cortest.bartlett(uscrimepc)
```

```
## R was not square, finding R from data
```

```
## $chisq
## [1] 236.5
## 
## $p.value
## [1] 2.12e-38
## 
## $df
## [1] 21
```


Principal Component Analysis without rotation
-----------------

```r
# Note that with the nfactor, we use all variables first and slowly cut down
# the variables for use.
p1 <- principal(uscrimepc, nfactor = 7, rotate = "NULL")
# Check the loadings
p1$loadings
```

```
## 
## Loadings:
##      PC1    PC2    PC3    PC4    PC5    PC6    PC7   
## murd  0.557  0.771         0.192  0.101         0.215
## rape  0.851  0.139 -0.286 -0.173 -0.378              
## robb  0.782         0.480 -0.376                     
## assa  0.784  0.546                             -0.284
## burg  0.881 -0.308 -0.123         0.145 -0.293       
## larc  0.728 -0.480 -0.404         0.179  0.210       
## auto  0.714 -0.438  0.375  0.350 -0.168              
## 
##                  PC1   PC2   PC3   PC4   PC5   PC6   PC7
## SS loadings    4.077 1.432 0.631 0.340 0.248 0.140 0.132
## Proportion Var 0.582 0.205 0.090 0.049 0.035 0.020 0.019
## Cumulative Var 0.582 0.787 0.877 0.926 0.961 0.981 1.000
```

```r

scree(uscrimepc, factors = F)
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 

```r

p2 <- principal(uscrimepc, nfactor = 2, rotate = "NULL")
# Check the loadings
p2$loadings
```

```
## 
## Loadings:
##      PC1    PC2   
## murd  0.557  0.771
## rape  0.851  0.139
## robb  0.782       
## assa  0.784  0.546
## burg  0.881 -0.308
## larc  0.728 -0.480
## auto  0.714 -0.438
## 
##                  PC1   PC2
## SS loadings    4.077 1.432
## Proportion Var 0.582 0.205
## Cumulative Var 0.582 0.787
```

```r

# Let's try rotation. default is VARIMAX rotation
p2r <- principal(uscrimepc, nfactor = 2)
```

```
## Loading required package: GPArotation
```

```r
# Check the loadings
p2r$loadings
```

```
## 
## Loadings:
##      RC1    RC2   
## murd         0.951
## rape  0.599  0.620
## robb  0.660  0.424
## assa  0.302  0.906
## burg  0.890  0.280
## larc  0.870       
## auto  0.835       
## 
##                  RC1   RC2
## SS loadings    3.131 2.377
## Proportion Var 0.447 0.340
## Cumulative Var 0.447 0.787
```

```r

# Try another rotation - Oblimin
p2ro <- principal(uscrimepc, nfactor = 2, rotate = "oblimin")
print(p2ro$loadings, digits = 3, cutoff = 0.4, sort = T)
```

```
## 
## Loadings:
##      TC1    TC2   
## rape  0.539  0.516
## robb  0.632       
## burg  0.895       
## larc  0.907       
## auto  0.866       
## murd         0.992
## assa         0.877
## 
##                  TC1   TC2
## SS loadings    3.123 2.145
## Proportion Var 0.446 0.306
## Cumulative Var 0.446 0.753
```

