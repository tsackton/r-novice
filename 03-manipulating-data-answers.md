---
title: "Answers to challenge in manipulating data"
output: html_document
layout: topic
---

### Challenges {.challenge}

* Using the new functions you have learned we can now "re-create your `metadata` file.  For this activity create three vectors corresponding to the three columns (`genotype`, `celltype`, `replicate`) in our `metadata`. BONUS: Use the function `data.frame()` to combine the vectors into a dataframe. #Hint: This function takes in each column as an argument by giving it name, and the `c()` function concatenates the values into a vector_. 


```r
# Answer to exercise
genotype=rep(c("Wt", "KO"), each=3, len=12)
celltype=c(rep("typeA", 6), rep("typeB", 6))
replicate=rep(seq(1,3), 4)
```


* The function `nrow()` on a `data.frame` returns the number of rows. Use it, in conjuction with `seq()` to create a new `data.frame` called `data_by_2` that includes every other row of the metadata.


```r
# Answer to exercise
metadata <- read.csv(file='meta/mouse_exp_design.csv')
data_by_2  <- metadata[seq(1, nrow(metadata), by=2),]

## or step-by-step
select_rows <- seq(1, nrow(metadata), by=2)
data_by_2  <- metadata[select_rows,]
```
