---
title: "Answers to challenge in starting with data"
output: html_document
layout: topic
---


### Challenge {.challenge}
* What is the class of the object `metadata`?

```r
# Answer to exercise
> class(metadata)
[1] "data.frame"
```
* How many rows and how many columns are in this object?

```r
# Answer to exercise
> dim(metadata)
[1] 12  3
```
* Load in data again, storing it as `test_data` and using `stringsAsFactors=F`. How does this change the data?

Answer: data are stored as characters instead of factors in columns 1 and 2 (genotype and celltype)

```r
# Answer to exercise
> str(metadata)
'data.frame':  12 obs. of  3 variables:
 $ genotype : Factor w/ 2 levels "KO","Wt": 2 2 2 1 1 1 2 2 2 1 ...
 $ celltype : Factor w/ 2 levels "typeA","typeB": 1 1 1 1 1 1 2 2 2 2 ...
 $ replicate: int  1 2 3 1 2 3 1 2 3 1 ...
> str(test_data)
 'data.frame':	12 obs. of  3 variables:
 $ genotype : chr  "Wt" "Wt" "Wt" "KO" ...
 $ celltype : chr  "typeA" "typeA" "typeA" "typeA" ...
 $ replicate: int  1 2 3 1 2 3 1 2 3 1 ...
```
