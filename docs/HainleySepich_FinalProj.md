---
title: "Stat380_FinalProject_Hainley_Sepich"
author: "Joseph Sepich and Connor Hainley"
date: "Due: 04/30/2019"
output: 
  html_document:
    keep_md: yes
  html_notebook: default
---

# Front matter


```
## Warning: package 'mdsr' was built under R version 3.5.3
```

```
## Warning: package 'mosaic' was built under R version 3.5.2
```

```
## Loading required package: dplyr
```

```
## Warning: package 'dplyr' was built under R version 3.5.3
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```
## Loading required package: lattice
```

```
## Loading required package: ggformula
```

```
## Warning: package 'ggformula' was built under R version 3.5.2
```

```
## Loading required package: ggplot2
```

```
## Loading required package: ggstance
```

```
## Warning: package 'ggstance' was built under R version 3.5.2
```

```
## 
## Attaching package: 'ggstance'
```

```
## The following objects are masked from 'package:ggplot2':
## 
##     geom_errorbarh, GeomErrorbarh
```

```
## 
## New to ggformula?  Try the tutorials: 
## 	learnr::run_tutorial("introduction", package = "ggformula")
## 	learnr::run_tutorial("refining", package = "ggformula")
```

```
## Loading required package: mosaicData
```

```
## Warning: package 'mosaicData' was built under R version 3.5.2
```

```
## Loading required package: Matrix
```

```
## 
## The 'mosaic' package masks several functions from core packages in order to add 
## additional features.  The original behavior of these functions should not be affected by this.
## 
## Note: If you use the Matrix package, be sure to load it BEFORE loading mosaic.
```

```
## 
## In accordance with CRAN policy, the 'mdsr' package 
##            no longer attaches
## the 'tidyverse' package automatically.
## You may need to 'library(tidyverse)' in order to 
##            use certain functions.
```

```
## Warning: package 'tidyr' was built under R version 3.5.3
```

```
## 
## Attaching package: 'tidyr'
```

```
## The following object is masked from 'package:Matrix':
## 
##     expand
```

```
## Warning: package 'lubridate' was built under R version 3.5.2
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following object is masked from 'package:base':
## 
##     date
```

```
## Warning: package 'data.table' was built under R version 3.5.3
```

```
## 
## Attaching package: 'data.table'
```

```
## The following objects are masked from 'package:lubridate':
## 
##     hour, isoweek, mday, minute, month, quarter, second, wday,
##     week, yday, year
```

```
## The following objects are masked from 'package:dplyr':
## 
##     between, first, last
```

```
## Warning: package 'rvest' was built under R version 3.5.3
```

```
## Loading required package: xml2
```

```
## Warning: package 'readxl' was built under R version 3.5.2
```
# Obtaining the data

Links to download data from BEA:

GDP by area:  https://apps.bea.gov/regional/downloadzip.cfm
GDP: https://www.bea.gov/data/gdp/gross-domestic-product
Homeland Security: https://www.dhs.gov/immigration-statistics/yearbook/2017


Codes to know:

* GDP in current dollars SAGDP2
* Compensation of Employees SAGDP4
* Real GDP in chained SAGDP9
* Per capita real GDP SAGDP10

## Compile GDP data into tables based on code



```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 62. Expected 30 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>

## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 62. Expected 30 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 5462. Expected 29 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early
## on line 4. Expected 30 fields but found 33. Consider fill=TRUE and
## comment.char=. First discarded non-empty line: <<"00000" ,"United
## States*", ,SAGDP2N,"Gross domestic product (GDP) by state","Millions of
## current dollars",3,"11"," Agriculture, forestry, fishing, and hunting",
## 108636.5,99756.5,92590.4,98311.7,99835.6,95629.0,113953.5,142945.2,128346.7,125130.4,144062.3,147244.0,129967.8,146299.0,180944.9,179572.7,215600.6,200841.6,181220.2,164913.2,169225.2>>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early
## on line 4. Expected 44 fields but found 46. Consider fill=TRUE and
## comment.char=. First discarded non-empty line: <<"00000" ,"United
## States", ,SAGDP2S,"Gross domestic product (GDP) by state","Millions
## of current dollars",3,"A"," Agriculture, forestry, and fishing",
## 20385.9,19502.3,22274.3,23338.1,22800.9,23505.5,26195.5,27297.9,29423.8,34306.8,51974.9,50099.2,51707.9,50278.6,50787.2,59091.9,69972.7,62566.8,76827.0,73278.6,58978.9,79601.9,80516.3,78229.3,84294.0,85182.0,98724.7,104602.3,98401.9,109105.2,98846.0,116215.4,103036.4,129420.2,126638.5>>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 5466. Expected 30 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 4682. Expected 44 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 5466. Expected 30 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 4682. Expected 44 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 5466. Expected 30 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 4682. Expected 44 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 5466. Expected 30 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 4682. Expected 44 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 5466. Expected 30 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 4682. Expected 44 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 5462. Expected 30 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early on line
## 4682. Expected 30 fields but found 1. Consider fill=TRUE and comment.char=.
## First discarded non-empty line: <<"Note: See the included footnote file.">>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early
## on line 4. Expected 30 fields but found 33. Consider fill=TRUE and
## comment.char=. First discarded non-empty line: <<"00000" ,"United
## States", ,SAGDP9N,"Real GDP by state","Millions of chained 2012
## dollars",3,"11"," Agriculture, forestry, fishing, and hunting",
## 140286.0,136879.5,141020.5,161798.9,156154.9,161617.5,174162.5,188091.9,196126.0,199349.4,176568.7,180294.9,199976.1,193856.2,186395.0,179573.0,209387.5,210511.6,224592.0,234231.4,222984.8>>
```

```
## Warning in fread(file = paste0(dataPath, files[i])): Stopped early
## on line 4. Expected 30 fields but found 32. Consider fill=TRUE and
## comment.char=. First discarded non-empty line: <<"00000" ,"United
## States", ,SAGDP9S,"Real GDP by state","Millions of chained
## 1997 dollars",3,"A"," Agriculture, forestry, and fishing",
## 56532.8,55047.6,59758.9,59377.3,75038.6,79465.3,57685.9,74980.5,89167.9,89557.5,92592.3,85159.3,94542.1,100949.4,102649.4,113466.4,99239.7,119176.7,103793.3,116476.3,126638.5>>
```


```r
write.csv(bigBoii, file = paste0(dataPath,"compositeTable.csv"))
```


```r
bigBoii <- fread(file = paste0(dataPath,"compositeTable.csv"))
# SAGDP2
current <- bigBoii %>%
  filter(grepl("^SAGDP2(N|S)$", TableName))
write.csv(current, file = paste0(dataPath,"SAGDP2.csv"))
```


```r
# SAGDP4
compensation <- bigBoii %>%
  filter(grepl("^SAGDP4(N|S)$", TableName))
write.csv(compensation, file = paste0(dataPath,"SAGDP4.csv"))
```


```r
# SAGDP9
real <- bigBoii %>%
  filter(grepl("^SAGDP9(N|S)$", TableName))
write.csv(real, file = paste0(dataPath,"SAGDP9.csv"))
```


```r
# SAGDP10
perCapita <- bigBoii %>%
  filter(grepl("^SAGDP10(N|S)$", TableName))
write.csv(perCapita, file = paste0(dataPath,"SAGDP10.csv"))
```
 
## Scraping Immigration statistics 
 

```r
# returns immigration table found on the page of a specific url
readTable <- function(url) {
  table <- url %>%
            read_html() %>%
            html_nodes(xpath=paste0('/html/body/div[2]/section/div/div/div[2]/',
                                    'div/section/div/div/div/article/div[1]/',
                                    'div[2]/div/div/table')) %>%
            html_table()
  table <- table[[1]]
}
```


```r
# Started putting tables online in 2014, prior they are in csv for download.
# Use 2013, 2004 and scrape 2014-2017
dataPath <- paste0(substr(dataPath, 1, nchar(dataPath)-4),"Immigration/")
```

```r
# Scrape data from 2014-2017
immigrants <- data.frame(stringsAsFactors = FALSE)
year <- 2014
while (year <= 2017) {
  url <- paste0("https://www.dhs.gov/immigration-statistics/yearbook/",year,
                "/table22")
  if (year == 2014) {
    immigrants <- readTable(url)
  } else {
    immigrants <- immigrants %>%
      inner_join(readTable(url), by = c("State or Territory of Residence"))
  }
  year <- year + 1
}
# Read in and add data from 8_ - 2013
# Table33
# 2103 table 22
files <- list.files(path = dataPath)
data1 <- read_excel(paste0(dataPath,files[1]))
```

```
## New names:
## * `` -> ...2
## * `` -> ...3
## * `` -> ...4
## * `` -> ...5
## * `` -> ...6
## * ... and 5 more problems
```

```r
data2 <- read_excel(paste0(dataPath,files[2]))
```

```
## New names:
## * `` -> ...2
## * `` -> ...3
## * `` -> ...4
## * `` -> ...5
## * `` -> ...6
## * ... and 14 more problems
```

```r
data1 <- data1[1:(length(data1$`Table 22.`)-3),]
data1 <- data1[3:length(data1$`Table 22.`),]
data1[1,1] <- "State or Territory of Residence"

data2 <- data2 %>%
  filter(!is.na(`TABLE 33.`))
data2 <- data2[1:(length(data2$`TABLE 33.`)-2),]
data2 <- data2[2:length(data2$`TABLE 33.`),]
data2[1,1] <- data1[1,1]

colnames(data1) <- as.character(unlist(data1[1,]))
data1 = data1[-1, ]

colnames(data2) <- as.character(unlist(data2[1,]))
data2 = data2[-1, ]

# Convert data types to numeric to match with data1
colsNum <- colnames(data2)
colsNum <- colsNum[2:length(colsNum)]
data2[colsNum] <- sapply(data2[colsNum],as.numeric)
```

```
## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion

## Warning in lapply(X = X, FUN = FUN, ...): NAs introduced by coercion
```

```r
colsNum <- colnames(immigrants)
colsNum <- colsNum[2:length(colsNum)]
immigrants[colsNum] <- sapply(immigrants[colsNum],function(x) gsub(",","",x))
immigrants[colsNum] <- sapply(immigrants[colsNum],as.numeric)

immigrants <- immigrants %>%
      inner_join(data1, by = c("State or Territory of Residence"))
immigrants <- immigrants %>%
      inner_join(data2, by = c("State or Territory of Residence"))
```
 
## Read in tables

```r
dataPath <- paste0(substr(dataPath, 1, nchar(dataPath)-12),"GDP/")
current <- fread(file = paste0(dataPath,"SAGDP2.csv"))
compensation <- fread(file = paste0(dataPath,"SAGDP4.csv"))
real <- fread(file = paste0(dataPath,"SAGDP9.csv"))
perCapita <- fread(file = paste0(dataPath,"SAGDP10.csv"))
```












