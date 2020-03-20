# 02-compiling-advanced-r-mh0816
02-compiling-advanced-r-mh0816 created by GitHub Classroom
---
title: "Problems and Solutions to Compile a PDF Version of Advanced R"
author: "Li Minghui"
date: "2020/3/19"
output: html_document
---

## 前言
已经成功将rmd文件编译成完整的html格式，但是pandoc和Miktex将html格式转为pdf格式确遇到问题:Cannot find Inconsolata.mf.
待更新......

## 准备工作
首先克隆Hadley Wickham的github存储库的源代码到git本地仓库,网址参考：<https://github.com/hadley/adv-r/>

## devtools()使用过程中遇到的问题
```{r}
devtools::install_github("hadley/sloop")
devtools::install_github("hadley/emo")
```
但是出现了：
`Error : Failed to install 'sloop' from GitHub: schannel: failed to receive handshake, SSL/TLS connection failed`    
然后我在Git bash中输入：    
`git config --global http.sslBackend "openssl"`    
`git config --global http.sslCAInfo C:/Users/86130/Desktop/adv-r`    
其中，第二行代码中的地址要改成自己放adv-r文件夹的地址

## bookdown()使用过程中遇到的问题
```{r}
bookdown::render_book("index.Rmd", output_format = "bookdown::pdf_book")
```

## Introduction.Rmd
### 1.缺少安装包
```{r}
Error in loadNamespace(name) : there is no package called 'desc'
Error in loadNamespace(name) : there is no package called 'sessioninfo'
Error in library(lobstr) : there is no package called 'lobstr'
```
### 可以通过如下代码安装所需要的包
```{r}
install.packages("desc")
install.packages("sessioninfo")
install.packages("lobstr")
```

### 2.无效的多字节字符串
```{r}
Quitting from lines 223-235 (Introduction.Rmd) 
Error in cat(paste0(contributors$desc, collapse = ", ")) : 
  invalid multibyte string at '<86>,<4e>A (\@kfeng123), Karl Forner (\@kforner), Kirill Sevastyanenko (\@kirillseva), Brian Knaus (\@knausb), Kirill M眉ller (\@krlmlr), Kriti Sen Sharma (\@ksens), Kai Tang (鍞愭伜锛<89>,NA (\@ktang), Kevin Wright (\@kwstat), suo.lawrence.liu@gmail.com (\@Lawrence-Liu), \@ldfmrails, Kevin Kainan Li (\@legendre6891), Rachel Severson (\@leighseverson), Laurent Gatto (\@lgatto), C. Jason Liang (\@liangcj), Steve Lianoglou (\@lianos), Yongfu Liao (\@liao961120), Likan (\@likanzhan), \@lindbrook, Lingbing Feng (\@Lingbing), Marcel Ramos (\@LiNk-NY), Zhongpeng Lin (\@linzhp), Lionel Henry (\@lionel-), Llu铆s (\@llrs), myq (\@lrcg), Luke W Johnston (\@lwjohnst86), Kevin Lynagh (\@lynaghk), \@MajoroMask, Malcolm Barrett (\@malcolmbarrett), \@mannyishere, \@mascaretti, Matt (\@mattbaggott), Matthew Grogan (\@mattgrogan), \@matthewhillary, Matthieu Gomez (\@matthieugomez), Matt Malin (\@mattmalin), Mauro Lepore (\@maurolepore), Max Ghenis (\@MaxGhenis), M
Calls: local ... withCallingHandlers -> withVisible -> eval -> eval -> cat
```
在224行添加代码 `encoding = "UTF-8"` 即可：
```{r}
contributors <- read.csv("contributors.csv", stringsAsFactors = FALSE, encoding = "UTF-8")
```

## Conditions.Rmd
### 缺少包
```{r}
Quitting from lines 788-794 (Conditions.Rmd) 
Error in library(testthat) : there is no package called 'testthat'
```
### 安装包
```{r}
install.packages("testthat")
```

## Functionals.Rmd
### 缺少包
```{r}
Quitting from lines 726-734 (Functionals.Rmd) 
Error in loadNamespace(name) : there is no package called 'tibble'
```
### 安装包
```{r}
install.packages("tibble")
```

## Function-operators.Rmd
'Error in .f(.x[[i]], .y[[i]], ...) : 无法打开 URL'https://adv-r.hadley.nz' Calls: local ...withCallingHandlers -> withVisible -> eval -> -> walk2 -> map2 -> .f 停止执行'
在243行将 'https://adv-r.hadley.nz' 改为 'https://adv-r.hadley.nz/' 即可

## R6.Rmd
### 缺少包
```{r}
Quitting from lines 535-550 (R6.Rmd) 
Error in loadNamespace(name) : there is no package called 'DBI'
```
### 安装包
```{r}
install.packages("DBI")
```
### 缺少包
```{r}
Quitting from lines 535-550 (R6.Rmd) 
Error in loadNamespace(name) : there is no package called 'RSQLite'
```
### 安装包
```{r}
install.packages("RSQLite")
```

## Big-picture.Rmd
### 原代码
```{r}
library(dlyr)

con <- DBI::dbConnect(RSQLite::SQLite(), filename = ":memory:")
mtcars_db <- copy_to(con, mtcars)
```
### 报错
```{r}
Quitting from lines 214-226 (Big-picture.Rmd) 
Error in library(dlyr) : 不存在叫'dlyr'这个名字的程辑包
Calls: local ... withCallingHandlers -> withVisible -> eval -> eval -> library
```
### 修改
```{r}
library(dblyr)

con <- DBI::dbConnect(RSQLite::SQLite(), filename = ":memory:")
mtcars_db <- copy_to(con, mtcars)
```
### 安装包
```{r}
install.packages("dbplyr")
```

## Perf-measure.Rmd
### 缺少包
```{r}
Quitting from lines 38-40 (Perf-measure.Rmd) 
Error in library(profvis) : there is no package called 'profvis'

Quitting from lines 38-40 (Perf-measure.Rmd) 
Error in library(bench) : there is no package called 'bench'

Quitting from lines 233-234 (Perf-measure.Rmd) 
Error in loadNamespace(name) : there is no package called 'ggbeeswarm'
```
### 安装包
```{r}
install.packages("profvis")
install.packages("bench")
install.packages("ggbeeswarm")
```

## Rcpp.Rmd
需要安装 Rtools
