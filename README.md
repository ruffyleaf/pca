Principal Component Analysis
==============================

Principal Component Analysis in R.

uscrime.csv consists of the following variables:
------
state - State Abbreviation
land - Land area
popu - 1985 Population
murd - Murder
rape - Rape
robb - Robbery
assa - Assault
burg - Burglary
larc - Larceny
auto - Auto theft
reg - US States Region number
      1 - Northeast
      2 - Midwest
      3 - South
      4 - West
div - US States division number
      1 - New England
      2 - Mid-Atlantic
      3 - E N Central
      4 - W N Central
      5 - S Atlantic
      6 - E S Central
      7 - W S Central
      8 - Mountain
      9 - Pacific

str(uscrime)
'data.frame':  50 obs. of  12 variables:
 $ state: Factor w/ 50 levels "AK","AL","AR",..: 21 30 46 19 39 7 34 31 38 35 ...
 $ land : int  33265 9279 9614 8284 1212 5018 49108 7787 45308 41330 ...
 $ popu : int  1164 998 535 5822 968 3174 17783 7562 11853 10744 ...
 $ murd : num  1.5 2 1.3 3.5 3.2 3.5 7.9 5.7 5.3 6.6 ...
 $ rape : num  7 6 10.3 12 3.6 9.1 15.5 12.9 11.3 16 ...
 $ robb : num  12.6 12.1 7.6 99.5 78.3 ...
 $ assa : int  62 36 55 88 120 87 209 90 90 116 ...
 $ burg : int  562 566 731 1134 1019 1084 1414 1041 594 854 ...
 $ larc : int  1055 929 969 1531 2186 1751 2025 1689 1001 1944 ...
 $ auto : int  146 172 124 878 859 484 682 557 340 493 ...
 $ reg  : int  1 1 1 1 1 1 1 1 1 2 ...
 $ div  : int  1 1 1 1 1 1 2 2 2 3 ...