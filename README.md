---
title: "Stat380_FinalProject_Hainley_Sepich"
author: "Joseph Sepich and Connor Hainley"
date: "2019-04-30"
output: 
  html_document:
    keep_md: yes
  html_notebook: default
---

# Front matter


```r
# always clean up R environment
rm(list = ls())
# load all packages here
library(mdsr) # book package of utilities
library(stringr) # utility package for strings
library(tidyr) # tidyverse utilities
library(lubridate) # date utility package
library(data.table) # using fread function
library(rvest) # web scraping package
library(readxl) # read execel files

# user defined functions
# readTables

# data
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


```r
# First read in all csv files into single data table
dataPath <- "G:\\GitRepos\\Stat380FinalProjectSepichHainley\\GDP\\"
```

```r
files <- list.files(path = dataPath,
                    pattern = "ALL_AREAS_[0-9]*_[0-9]*.csv$")
bigBoii <- data.frame(GeoFIPS = character(), Region = character(),
                      stringsAsFactors = FALSE)
for (i in 1:length(files)) {
  bigBoii <- rbind(bigBoii, fread(file = paste0(dataPath,files[i])), fill = TRUE)
}
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











