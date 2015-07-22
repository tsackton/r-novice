---
title: "R syntax and Datatypes"
date: "03/03/2015"
output: html_document
layout: topic
minutes: 45
---

> ## Learning Objectives {.objectives}
>
> * Familiarize students with R syntax
> * Understand the concepts of objects and assignment
> * Create vectors and data types
> * Utilizing functions
> * Installing packages and loading libraries



## Assignment operator

`<-` is the assignment operator; it is like an arrow that points from the value to the object assigning values on the right to objects on the left. Mostly similar to `=` but not always. Learn to use `<-` as it is good programming practice. Using `=` in place of `<-` can lead to issues down the line.

_Shortcut_: typing `Alt + -` (push `Alt`, the key next to your space bar at the same time as the `-` key) will write ` <- ` in a single keystroke.


You can get output from R simply by typing in math in the console


```r
3 + 5
12/7
```

However, to do useful and interesting things, we need to **assign values to objects**. To create objects, we need to give it a name followed by the assignment operator `<-` and the value we want to give it:


```r
weight_kg <- 55
```

### Naming variables

* Objects can be given any name such as `x`, `current_temperature`, or `subject_id`. You want your object names to be explicit and not too long. 
* They cannot start with a number (`2x` is not valid but `x2` is) nor can they contain hyphens. 
* R is case sensitive (e.g., `weight_kg` is different from `Weight_kg`). 
* There are some names that cannot be used because they are reserved the names of fundamental functions in R
(e.g., `if`, `else`, `for`, see [here](https://stat.ethz.ch/R-manual/R-devel/library/base/html/Reserved.html)
for a complete list). 
* Even if it's allowed, it's best to not use other function names (e.g., `c`, `T`, `mean`, `data`, `df`, `weights`). In doubt check the help to see if the name is already in use. 

When assigning a value to an object, R does not print anything. You can force it to
print the value by using parentheses or by typing the name:


```r
(weight_kg <- 55)
weight_kg
```

Now that R has `weight_kg` in memory, we can do arithmetic with it. For
instance, we may want to convert this weight in pounds (weight in pounds is 2.2
times the weight in kg):


```r
2.2 * weight_kg
```

We can also change a variable's value by assigning it a new one:



```r
weight_kg <- 57.5
2.2 * weight_kg
```

```
## [1] 126.5
```

This means that assigning a value to one variable does not change the values of
other variables.  For example, let's store the animal's weight in pounds in a
variable.


```r
weight_lb <- 2.2 * weight_kg
```

and then change `weight_kg` to 100.


```r
weight_kg <- 100
```
What do you think is the current content of the object `weight_lb`? 126.5 or 220?

_Note: When typing out a variable that is stored try pressing the `Tab` key after typing only `weight`. You will find that RStudio will tab-complete the variable name._ 

> ### Challenge {.challenge}
>
> What are the values after each statement in the following?
 

```r
mass <- 47.5           # mass?
age  <- 122            # age?
mass <- mass * 2.0     # mass?
age  <- age - 20       # age?
massIndex <- mass/age  # massIndex?
```

## Vectors and data types

A vector is the most common and basic data structure in R, and is pretty much
the workhorse of R. It's a group of values, mainly either numbers or
characters (or can be both). You can assign this list of values to a variable, just like you
would for one item. For example we can create a vector of animal weights:


```r
weights <- c(50, 60, 65, 82)
```

A vector can also contain characters:


```r
animals <- c("mouse", "rat", "dog")
```

Alternatively a vector can contain both:


```r
scores <- c("A", "B", 80, 60, 20)
scores
```

There are many functions that allow you to inspect the content of a
vector. `length()` tells you how many elements are in a particular vector:


```r
length(weights)
length(animals)
```

`class()` indicates the class (the type of element) of an object:


```r
class(weights)
```

```
## [1] "numeric"
```

```r
class(animals)
```

```
## [1] "character"
```

The function `str()` provides an overview of the object and the elements it
contains. It is a really useful function when working with large and complex
objects:


```r
str(weights)
```

```
##  num [1:4] 50 60 65 82
```

```r
str(animals)
```

```
##  chr [1:3] "mouse" "rat" "dog"
```

You can add elements to your vector simply by using the concatenate function denoted by `c()` function:


```r
weights <- c(weights, 90) # adding at the end
weights <- c(30, weights) # adding at the beginning
weights
```

```
## [1] 30 50 60 65 82 90
```

What happens here is that we take the original vector `weights`, and we are
adding another item first to the end of the other ones, and then another item at
the beginning. We can do this over and over again to build a vector or a
dataset. As we program, this may be useful to autoupdate results that we are
collecting or calculating.

We just saw 2 of the 6 **data types** that R uses: `"character"` and `"numeric"`. The other 4 are:    

* `"logical"` for `TRUE` and `FALSE` (the boolean data type; true and false values do not require quotations)
* `"integer"` for integer numbers (e.g., `2L`, the `L` indicates to R that it's an integer)
* `"complex"` to represent complex numbers with real and imaginary parts (e.g.,
  `1+4i`) and that's all we're going to say about them
* `"raw"` that we won't discuss further

> ### Challenge {.challenge}
> Try creating a logical vector that is the same length as the `weights` vector. Assign a `TRUE` value for values that are multiples of 10, otherwise assign `FALSE`. Use the help manual to see how integer variable differs from the numeric.

Vectors are one of the many **data structures** that R uses. Other important
ones are lists (`list`), matrices (`matrix`), data frames (`data.frame`) and
factors (`factor`).

## Functions and their arguments

Functions are **"self contained" modules of code that accomplish a specific task**. Functions usually take in data, process it, and return a result. We have already used a few examples of basic functions above i.e `length`, `class` and `str`.

Let's look at a more advanced function call below `read.csv`. This function is used to read in data from a csv (comma separated values) file. There are numerous other functions to load in data depending on your filetype, we will discuss this in detail in the next section.

_Note: When typing out read.csv try pressing the `Tab` key after typing only `read`. You will find that a drop-down menu will appear listing all `read` options for loading in files. The window to the right gives you more information on the function and its arguments as you scroll down and highlight each individually._ 



```r
read.csv(file="http://fasrc.github.io/2015-07-22_SWC-R/class_data/mouse_exp_design.csv")
```

The `file=` part inside the parentheses is called an **argument**, and most functions use arguments. Arguments modify the behavior of the function. Typically, they take some input (e.g., some data, an object) and other
options to change what the function will return, or how to treat the data provided. Simple functions like the function `length` don't need additional modifications. It will take input (i.e. vector), process it (i.e. count the number of elements) and return value.

Note that arguments can take objects as values, like so:


```r
mouse_exp_design<-c("http://fasrc.github.io/2015-07-22_SWC-R/class_data/mouse_exp_design.csv")
read.csv(file=mouse_exp_design)
```

Most functions can take several arguments, but most are specified by default so you don't have to enter them. To see these default values, you can either type `args(read.csv)` or look at the help for this function (e.g., `?read.csv`).


```r
args(read.csv)
```

```
## function (file, header = TRUE, sep = ",", quote = "\"", dec = ".", 
##     fill = TRUE, comment.char = "", ...) 
## NULL
```

If you provide the arguments in the exact same order as they are defined you
don't have to name them:


```r
read.csv(file=mouse_exp_design, header=TRUE) # is identical to:
read.csv(mouse_exp_design, TRUE)
```

However, it's usually not recommended practice because it's a lot of remembering
to do, and if you share your code with others that includes less known functions
it makes your code difficult to read. If you include names **do not use the assignment operator**. A `=` should be used to specify the values of arguments in functions. (It's however OK to not include the names
of the arguments for basic functions like `mean`, `min`, etc...)

Another advantage of naming arguments, is that the order doesn't matter:


```r
read.csv(file=mouse_exp_design, header=TRUE) # is identical to:
read.csv(header=TRUE, file=mouse_exp_design)
```

## Packages and Libraries

**Packages** are collections of R functions, data, and compiled code in a well-defined format. The directory where packages are stored is called the **library**. The two terms are sometimes used synonomously and there has been [discussion](http://www.r-bloggers.com/packages-v-libraries-in-r/) amongst the community to resolve this. It is somewhat counter-intuitive to _load a package_ using the `library()` function 
and so you can see how confusion can arise.


There are a set of **standard (or base) packages** which are considered part of the R source code and automatically available as part of your R installation.
Base packages contain the basic functions that allow R to work, and enable standard statistical and graphical functions on datasets; for example all of the functions that we have been using so far in our examples.

You can check what base packages are loaded by typing into the console:


```r
sessionInfo()

R version 3.1.2 (2014-10-31)
Platform: x86_64-pc-linux-gnu (64-bit)

locale:
 [1] LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C               LC_TIME=en_US.UTF-8        LC_COLLATE=en_US.UTF-8     LC_MONETARY=en_US.UTF-8   
 [6] LC_MESSAGES=en_US.UTF-8    LC_PAPER=en_US.UTF-8       LC_NAME=C                  LC_ADDRESS=C               LC_TELEPHONE=C            
[11] LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C       

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base    
```

In this course we will mostly be using functions from the standard base packages. However, the more you work with R you will come to realize that there is a cornucopia of R packages that offer a wide variety of functionality. To use additional packages will require installation. 
Packages for R can be installed from the [CRAN](http://cran.r-project.org/) package repository. An example is given below as we install the `gplots` package required for some images we will create later on.


```r
install.packages('gplots')
```

Alternatively, packages can also be installed from [Bioconductor]() by using the `biocLite.R` installation script. You will first need to install Bioconductor and all the standard packages (this only needs to be done once ever):


```r
source("http://bioconductor.org/biocLite.R")
biocLite()
```

Once you have the standard installed, you can add additional packages using the `biocLite.R` script. If it's a new R session you will also have to source the script again. Here we will install another package useful for visualization `ggplot2`:


```r
biocLite('ggplot2')
```


Once you have the package installed, you can load it into your R session for use. Note that quotations are not required here.


```r
library(gplots)
library(ggplot2)
```
