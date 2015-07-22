---
title: "Starting with data"
date: "03/03/2015"
output: html_document
layout: topic
minutes: 20
---


> ## Learning Objectives {.objectives}
>
> * Introducing data frames
> * Load in data (CSV files)
> * Explore the structure and the content of the data in R
> * Understand what are factors and how to manipulate them

# What are data frames?

`data.frame` is the _de facto_ data structure for most tabular data and what we
use for statistics and plotting.

A `data.frame` is a collection of vectors of identical lengths. Each vector
represents a column, and each vector can be of a different data type (e.g.,
characters, integers, factors). The `str()` function is useful to inspect the
data types of the columns.

A `data.frame` can be created by the functions `read.csv()` or `read.table()`, which can be used to import spreadsheets from your hard drive (or the web). As we see in the pull-down menu that appears after tab-completion there are a number of functions for loading in files. The `read.table` function requires the user to provide specific arguments whereas for `read.csv` this is set by default. _Note that `read.csv` can also accept other delimiter files simply by passing in the `sep` argument_

> ### Note: {.callout}
> By default, `data.frame` converts (= coerces) columns that contain characters
> (i.e., text) into the `factor` data type. Depending on what you want to do with
> the data, you may want to keep these columns as `character`. To do so,
> `read.csv()` and `read.table()` have an argument called `stringsAsFactors` which
> can be set to `FALSE`.


# Loading in files

We are studying two different celltypes in mice and want to evaluate how gene expression differs in WT versus Knockout (KO).  The experimental design setup is stored as a `.csv` file: each row holds information for a single animal, and the columns represent `genotype`(WT or KO),  `celltype` (typeA or typeB), and `replicate number`.

To load in our metadata, we need to locate the `mouse_exp_design.csv` file. We will use
`read.csv()` to load into memory (as a `data.frame`) the content of the CSV
file. Using the same command function as our previous session, but **this time we will assign it to a variable**.


```r
metadata <- read.csv(file="http://fasrc.github.io/2015-07-22_SWC-R/class_data/mouse_exp_design.csv")
```

This statement doesn't produce any output because assignment doesn't display
anything. If we want to check that our data has been loaded, we can print the
variable's value: 


```r
metadata
```

```
##          genotype celltype replicate
## sample1        Wt    typeA         1
## sample2        Wt    typeA         2
## sample3        Wt    typeA         3
## sample4        KO    typeA         1
## sample5        KO    typeA         2
## sample6        KO    typeA         3
## sample7        Wt    typeB         1
## sample8        Wt    typeB         2
## sample9        Wt    typeB         3
## sample10       KO    typeB         1
## sample11       KO    typeB         2
## sample12       KO    typeB         3
```

__At this point, make sure all participants have the data loaded__

By default, using the `read.csv` function will load in the data and assign the first row of the table to be our **column names**. Additionally since our header has one less name than there are columns R automatically assigns the **first column as row names**. 
We can look at the values assigned for each by using `row.names` and `col.names`.


```r
rownames(metadata)
colnames(metadata)
```

> ### Challenge {.challenge}
> We can change the default settings by adding in arguments when we read in the data by setting `header = FALSE`. Check to see how the dataframe has changed. What happens if we load in data using `read.table`? 

 **Load the data in again using default settings and `read.csv` to continue.**

Suppose we had a larger file, we might not want to display all the contents in the console. Instead we could check the top (the first 6 lines) of this `data.frame` using the function `head()`:


```r
head(metadata)
```

Let's now check the __str__ucture of this `data.frame` in more details with the
function `str()`:


```r
str(metadata)
```

```
## 'data.frame':	12 obs. of  3 variables:
##  $ genotype : Factor w/ 2 levels "KO","Wt": 2 2 2 1 1 1 2 2 2 1 ...
##  $ celltype : Factor w/ 2 levels "typeA","typeB": 1 1 1 1 1 1 2 2 2 2 ...
##  $ replicate: int  1 2 3 1 2 3 1 2 3 1 ...
```

__You can also get this information from the "Environment" tab in RStudio.__

# Inspecting `data.frame` objects

We already saw how the functions `head()` and `str()` can be useful to check the
content and the structure of a `data.frame`. Here is a non-exhaustive list of
functions to get a sense of the content/structure of the data.

* Size:
    * `dim()` - returns a vector with the number of rows in the first element, and
    the number of columns as the second element (the __dim__ensions of the object)
    * `nrow()` - returns the number of rows
    * `ncol()` - returns the number of columns
* Content:
    * `head()` - shows the first 6 rows
    * `tail()` - shows the last 6 rows
* Names:
    * `names()` - returns the column names (synonym of `colnames()` for `data.frame`
	objects)
   * `rownames()` - returns the row names
* Summary:
   * `str()` - structure of the object and information about the class, length and
	content of  each column
   * `summary()` - summary statistics for each column

Note: most of these functions are "generic", they can be used on other types of
objects besides `data.frame`.

> ### Challenge {.challenge}
> * What is the class of the object `metadata`?
> * How many rows and how many columns are in this object?
> * Load in data again, storing it as `test_data` and using `stringsAsFactors=F`. How does this change the data?

As you can see, the columns `genotype` and `celltype` are of a special class called
`factor`. Before we learn more about the `data.frame` class, we are going to
talk about factors. They are very useful but not necessarily intuitive, and
therefore require some attention.


## Factors

Factors are used to represent categorical data. Factors can be ordered or
unordered and are an important class for statistical analysis and for plotting.

Factors are stored as integers, and have labels associated with these unique
integers. While factors look (and often behave) like character vectors, they are
actually integers under the hood, and you need to be careful when treating them
like strings.

Once created, factors can only contain a pre-defined set values, known as
*levels*. By default, R always sorts *levels* in alphabetical order. For
instance, if you have a factor with 2 levels:


```r
sex <- factor(c("male", "female", "female", "male"))
```

R will assign `1` to the level `"female"` and `2` to the level `"male"` (because
`f` comes before `m`, even though the first element in this vector is
`"male"`). You can check this by using the function `levels()`, and check the
number of levels using `nlevels()`:


```r
levels(sex)
```

```
## [1] "female" "male"
```

```r
nlevels(sex)
```

```
## [1] 2
```

Sometimes, the order of the factors does not matter, other times you might want
to specify the order because it is meaningful (e.g., "low", "medium", "high") or
it is required by particular type of analysis. For example, in this case you might want the "low" group to be your base level. That is, we are only interested in changes relative to "low".


```r
food <- factor(c("low", "high", "medium", "high", "low", "medium", "high"))

relevel(food, ref="low") # set base level
```

Additionally, specifying the order of the levels allows to compare levels:


```r
food <- factor(food, levels=c("low", "medium", "high"))
levels(food)
min(food) ## doesn't work
food <- factor(food, levels=c("low", "medium", "high"), ordered=TRUE)
levels(food)
min(food) ## works!
```

In R's memory, these factors are represented by numbers (1, 2, 3). They are better than using simple integer labels because factors are self describing: `"low"`, `"medium"`, and `"high"`" is more descriptive than `1`, `2`, `3`. Which is low?  You wouldn't be able to tell with just integer data. Factors have this
information built in. It is particularly helpful when there are many levels.

### Converting factors

If you need to convert a factor to a character vector, simply use
`as.character(x)`.

Converting a factor to a numeric vector is however a little trickier, and you
have to go via a character vector. Compare:


```r
f <- factor(c(1, 5, 10, 2))
as.numeric(f)               ## wrong! and there is no warning...
as.numeric(as.character(f)) ## works...
as.numeric(levels(f))[f]    ## The recommended way.
```
