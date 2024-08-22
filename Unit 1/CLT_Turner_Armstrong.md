---
title: "Live Session 1 CLT"
author: "Turner Armstrong"
date: "2024-08-22"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

# Simulator to demonstrate CLT
## Control Parameters
```{r}
n1 = 10000000 # size of the population creation
n2 = 50 # sample size per sample for 2nd distribution (we will compare these distributions to the population) 
simulations = 10000 #number of samples and thus number of xbars we will generate in sampling from the population.
df = 2 #degrees of freedom in the population distribution
```

## Data Holder
```{r}
xbar_holder1 = numeric(simulations) # This will hold all the sample means for the first distribution.
```

## Creating, observing, and storing the population
```{r}
population = rchisq(n1,df,ncp=0)
hist(population, col = "blue", main = paste("Distribution of population: n = ", n1), xlab = "Population Histogram", xlim = c(min(population),max(population)))
summary(population) #number summary and the mean of the population
sd(population) #sigma of the population
```
## Sampling and storing from the population
Generate 10,000 samples each of size 50 and find the mean of each sample.  Then store each mean in the xbar_holder vector.

```{r}
for (i in 1:simulations)
{ 
  sample1 = sample(x=population, size=n2, replace = TRUE)
  xbar1 = mean(sample1)
  xbar_holder1[i] = xbar1
}
```

## display the distribution of sample means (plot a histogram of the sample means)
```{r}
#par(mfrow = c(2,1))
#hist(population, col = "blue", main = paste("Distribution of population: n = ", n1), xlab = "Population Histogram", xlim = c(min(population),max(population)))
hist(xbar_holder1, col = "red", main = paste("Distribution of the sample mean: n = ", n2), xlab = "Dist 2 Sample Means", xlim = c(-4,4))
```

## summary statistics of the distribution of the simulated sample means. 
```{r}
summary(population) #5 number summary and the mean of the population
summary(xbar_holder1) #5 number summary and the mean of the sample means
sd(xbar_holder1) # standard deviation of distribution of the sample means

```
