---
title: "Task 4"
output:
  pdf_document: default
  html_document: default
  word_document: default
date: "2023-10-02"
---

# Using R example datasets

**1.Describe briefly the content of the CO2 dataset using the help function**

```{r}
#load the data
data("CO2")
?CO2
```

The experiment is analyzing the cold tolerance of the grass species *Echinochola cruss-galli* by measuring the CO2 response curve for photosynthesis. The data contain the CO2 uptake at several levels of CO2 concentration in the chilled and non-chilled plants.

**2.What is the average and median CO2 uptake of the plants from Quebec and Missisipi?**

```{r, results=FALSE}
library(tidyverse)
library(dplyr)
```

```{r}
data(CO2)
#select the plant originated from quebec only
Quebec <-filter(CO2, Type=="Quebec")
summary(Quebec)
#select the plant originated from Mississippi only
Mississippi<-filter(CO2, Type=="Mississippi")
summary(Mississippi)
```

```{r}

```
Another way is using tapply
```{r}
tapply(CO2$uptake, CO2$Type, mean)
```
```{r}
tapply(CO2$uptake, CO2$Type, median)
```

**[OPTIONAL]In the airway example data from Bioconductor, how many genes are expressed in each sample? How many genes are not expressed in any sample?**

---
title: "Task-5"
output: pdf_document
date: "2023-10-03"
---

#R Functions

**1. Write a function that calculates the ratio of the mean and the median of a given vector**

*symmetrically distributed if the ratio of the mean and median close to 1*

```{r}
x <- c(1:10)
ratio_mean_median <- function(x){
  mean_value <- mean(x, na.rm=TRUE)
  median_value <- median(x, na.rm=TRUE)
  ratio <- mean_value/median_value
  ratio
}
ratio_mean_median(x)
#na.rm=TRUE to handle missing value
```

*right-skewed data if the ratio of the mean and median is greater than 1*

```{r}
y <- c(1,2,3,4,50)
ratio_mean_median(y)
```

*left-skewed data if the ratio of the mean and median is less than 1*

```{r}
z <-c(-2,30,31,32,33,34)
ratio_mean_median(z)
```

**2. Write a function that ignores the lowest and the highest value from a given vector and calculate the mean**

```{r}
x <-c(1:6)
mean_without_max_min <-function(x){
  ignore_max_min <- x[c(-which.max(x), -which.min(x))]
  result<-mean(ignore_max_min)
  result
}
mean_without_max_min(x)
```

**Short explanation about piping**

The pipe operator chains together a sequence of operation by passing the results as an input to the next operation, in a natural and logical order of thinking. The pipes are not recommended to use when the operation is simple (might add unnecessary complexity), too long (hard to debug), has multiple output/input, and the sequence doesn't match the logic.

**Short explanation about apply-family of functions (apply, lapply, sapply)**

These functions apply a specified function to selected rows or columns of matrices, data frame, and list. They offers flexibility and efficiency when dealing with large datasets, particularly during data preprocessing such as data cleaning, normalization, or summarizing the descriptive statistics.
