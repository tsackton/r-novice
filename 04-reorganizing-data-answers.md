---
title: "Answers to challenges in Re-organizing data"
layout: topic
---
### Challenge {.challenge}
* First you will use what you have learned previously to read in the file and check to make see if:

1. all of the Ensemble IDs in the count matrix are contained in the RPKM matrix
2. the order of Ensemble Ids is the same in both data frames
3. subset such that you have two data files that have matching row names


```r
# Answer to exercise
head(counts) # take a peek inside

all(row.names(data_ordered) %in% row.names(counts))
all(row.names(data_ordered) == row.names(counts))    # this will give an error

# There is a difference in dimensions
dim(counts)
dim(data_ordered)

# Find the matching rows for the smaller of the two matrices
match_rows <- match(row.names(data_ordered), row.names(counts))
match_counts <- counts[match_rows,]

# Double check to see that all row names match
all(row.names(data_ordered) == row.names(match_counts))
```


* Use the code provided below to generate a dataframe `df1` of coloured blocks. Given the dataframe, try the following tasks:

1. The length and width of the blocks are provided, can you add a column to include the following height values: `20, 20, 30`?
2. We have information for an additional block that is yellow, except we don't have height for information (height =20; width= 15). Can you still add the yellow block in as an additional row?


```r
df1 <- data.frame(color=c("red", "green", "blue"), length=c(15,20,26), width=c(20,25,35))
```


```r
# Answer to add height
height <- c(20,20,30)
df1 <- cbind(df1, height)

# Answer to add yellow
yellow <- c("yellow", 20,15,NA)
df1$color <- factor(df1$color, levels=c("red", "green", "blue", "yellow"))
rbind(df1, yellow)
```
