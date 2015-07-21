---
layout: topic
title: Answers to challenges in Analyzing and Plotting Data
---

### Challenge {.challenge}
* Compute the [standard error](http://en.wikipedia.org/wiki/Standard_error) for "sample1". (hints: there is no built-in function to compute standard errors, but there may be functions for the different components of the formula)


```r
# sample SD divided by the square root of number of observations
sd <- sd(annotated_rpkm[,'sample1'], na.rm=T)
n <- nrow(annotated_rpkm)
sem <- sd / sqrt(n)
```


*  The previous challenge asked you to compute the standard error for "sample1". Using the `apply` function to generate a vector of standard error values for each sample. Use a boxplot to illustrate the differences in standard error between WT and KO samples. 


```r
# sample SD divided by the square root of number of observations
getSEM <-function(x) {sd(x) / sqrt(length(x))}
sem <- apply(annotated_rpkm[,2:ncol(annotated_rpkm)], 2, getSEM)

# boxplot
df <- cbind(metadata, sem=sem)
boxplot(sem ~ genotype, df)
```

