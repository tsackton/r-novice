---
title: "Data Manipulation"
date: "03/03/2015"
output: html_document
layout: topic
minutes: 45
---

> ## Learning Objectives {.objectives}
> * Indexing and sequences
> * Accessing elements of a dataframe
> * Visualizing using `table`, `barplot`


# Indexing and sequences

## Vectors

If we want to extract one or several values from a vector, we must provide one
or several indices in square brackets, just as we do in math. For instance:


```r
food[2]
food[c(3, 2)] #concantenate the values we want to explore
food[2:4]
```

R indexes start at 1. Programming languages like Fortran, MATLAB, and R start
counting at 1, because that's what human beings typically do. Languages in the C
family (including C++, Java, Perl, and Python) count from 0 because that's
simpler for computers to do.

`:` is a special function that creates numeric vectors of integer in increasing
or decreasing order, test `1:10` and `10:1` for instance. The function `seq()`
(for __seq__uence) can be used to create more complex patterns:


```r
seq(1, 10, by=2)
seq(5, 10, length.out=3)       # equal breaks of sequence into vector length = length.out
seq(50, by=5, length.out=10)   # sequence 50 by 5 until you hit vector length = length.out
seq(1, 8, by=3)                # sequence by 3 until you hit 8
```
Another useful function in creating sequences is `rep`, which _rep_licates elements of vector (or list, but not covered here). In it's simplest form you can replicate a value a specified number of times. More complex operations include replicating a sequence in a specified order.


```r
rep(51:54, 2)
rep(51:54, each = 2)       # not the same.
rep(51:54, c(2,1,2,1))   # specify replicate number for each element individually
rep(51:54, each = 2, len = 4)    # only first 4 elements displayed
rep(51:54, each = 2, len = 10)   # 8 integers plus two recycled 1's.
rep(51:54, each = 2, times = 3)  # length 24, 3 complete replications
```

> ### Challenge {.challenge}
> Using the new functions you have learned we can now **re-create** your `metadata` file.  For this activity create three vectors corresponding to the three columns (`genotype`, `celltype`, `replicate`) in our `metadata`. BONUS: Use the function `data.frame()` to combine the vectors into a dataframe. _Hint: This function takes in each column as an argument by giving it name, and the `c()` function concatenates the values into a vector_. 



## Dataframes

Our `metadata` frame has rows and columns (it has 2 dimensions), so if we want to extract some specific data from it we need to specify the "coordinates" we want from it. Row numbers come first, followed by column numbers.


```r
metadata[1, 1]   # first element in the first column of the data frame
metadata[1, 3]   # first element in the 3rd column
metadata[1:3, ] # first three rows
metadata[3, ]    # the 3rd element for all columns
metadata[ ,3]    # the entire 3rd column
```

> ### Challenge {.challenge}
> The function `nrow()` on a `data.frame` returns the number of rows. Use it, in conjuction with `seq()` to create a new `data.frame` called `data_by_2` that includes every other row of the metadata.


For larger datasets, it can be tricky to remember the column
number that corresponds to a particular variable. (Are species names in column 5
or 7? oh, right... they are in column 6). In some cases, in which column the
variable will be can change if the script you are using adds or removes
columns. It's therefore often better to use column names to refer to a
particular variable, and it makes your code easier to read and your intentions
clearer.

You can do operations on a particular column, by selecting it using the `$`
sign. In this case, the entire column is a vector. For instance, to extract all
the gentotypes from our dataset, we can use: `metadata$genotype`. You can use
`names(metadata)` or `colnames(metadata)` to remind yourself of the column names.

In some cases, you may way to select more than one column. You can do this using
the square brackets and concatenating a vector of strings that correspond to column names: 


```r
metadata[, c("genotype", "celltype")]
```

```
##          genotype celltype
## sample1        Wt    typeA
## sample2        Wt    typeA
## sample3        Wt    typeA
## sample4        KO    typeA
## sample5        KO    typeA
## sample6        KO    typeA
## sample7        Wt    typeB
## sample8        Wt    typeB
## sample9        Wt    typeB
## sample10       KO    typeB
## sample11       KO    typeB
## sample12       KO    typeB
```

## Plots
In our metadata file we have two factors `genotype` and `celltype`. While the `summary()` function tabulates numbers of samples and how they are distributed, we can go one step further with the `table` function which builds a contingeny table of the counts at each combination of factor levels. 


```r
twofactor <- metadata[, c("genotype", "celltype")]
table(twofactor) 
```

```
##         celltype
## genotype typeA typeB
##       KO     3     3
##       Wt     3     3
```

We can then take that table and visualize it using `barplot`. Samples are divided by celltype and the proportion of WT and KO are represented by different shades of grey within each bar.


```r
barplot(table(twofactor), legend=TRUE) 
```

<img src="figure/unnamed-chunk-9-1.png" title="plot of chunk unnamed-chunk-9" alt="plot of chunk unnamed-chunk-9" style="display: block; margin: auto;" />
