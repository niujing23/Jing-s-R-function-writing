# Jing-s-R-function-writing
practice R function writing
---
title: "defination function"
author: "JING NIU"
date: "September 9, 2015"
output: html_document
---

```{r libraries}
rm(list=ls())
library(stringi)
library(stringr)
library(tidyr)
library(truncnorm)
library(dplyr)
library(PKPDdatasets)
```

#create dataframe
```{r}
a<-rtruncnorm(24,mean=log(23.8),sd=1,a=log(7.0),b=log(62.6))
wt <- exp(a)
hist(wt)
wt
id <- seq(1,24)
raw_dat <-data.frame(id,wt)
raw_data <- raw_dat %>% arrange(wt) %>% mutate(time=0, more_fouryr=ifelse(wt<33,0,1)) %>% arrange(id)
```

#creat def_fun
```{r}
def_fun<-function(df){
  
  g<-rep(0,times=ncol(df))
  p<-rep(0,times=ncol(df))
         
for (i in 1:ncol(df)){
  p[i]<-c(type <- class(df[,i]))
  b <- colnames(df)
  g[i] <-c(max(stri_length(df[,i])))
  define<-data.frame(name<-b,type<-p,length<-g)
}
  return(define)
}
```

#test in different dataframe
```{r}
def_fun(df=raw_data)
def_fun(df=mtcars)
def_fun(df=sd_oral_richpk)
```
