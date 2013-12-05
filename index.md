---
title       : Overview of R 
subtitle    : Some concepts & cool Stuff
author      : Ian Munoz
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
---

## Summary

1. Variables & Data Structures



--- .class #id 

## Vectors

Define some Vectors
```
a <- c(1,2,5.3,6,-2,4) # numeric vector
b <- c("one","two","three") # character vector
c <- c(TRUE,TRUE,TRUE,FALSE,TRUE,FALSE) #logical vector
```
```
> a
[1]  1.0  2.0  5.3  6.0 -2.0  4.0
> b
[1] "one"   "two"   "three"
> c
[1]  TRUE  TRUE  TRUE FALSE  TRUE FALSE
> 
```

---

## Vectors

Refer to  elements in a Vector

```
>a[c(2,4)] # 2nd and 4th elements of vector
[1] 2 6
> b[1:2]
[1] "one" "two"
> a[c]
[1]  1.0  2.0  5.3 -2.0
```

---

## Matrices

```
# generates 5 x 4 numeric matrix 
x<-matrix(1:20, nrow=5,ncol=4)

# another example
cells <- c(1,26,24,68)
rnames <- c("R1", "R2")
cnames <- c("C1", "C2") 
mymatrix <- matrix(cells, nrow=2, ncol=2, byrow=TRUE,
dimnames=list(rnames, cnames))
```
```
> mymatrix
   C1 C2
R1  1 26
R2 24 68
```

---

## Matrices

Identify rows, columns or elements using subscripts.

```
> x[,4] # 4th column of matrix
[1] 16 17 18 19 20

> x[3,] # 3rd row of matrix 
[1]  3  8 13 18

> x[2:4,1:3] # rows 2,3,4 of columns 1,2,3
     [,1] [,2] [,3]
[1,]    2    7   12
[2,]    3    8   13
[3,]    4    9   14

```

---

## Data Frames

A data frame is more general than a matrix, in that different columns can have different modes (numeric, character, factor, etc.). This is similar to SAS and SPSS datasets.

```
d <- c(1,2,3,4)
e <- c("red", "white", "red", NA)
f <- c(TRUE,TRUE,TRUE,FALSE)
mydata <- data.frame(d,e,f)
names(mydata) <- c("ID","Color","Passed") # variable names
```
```
> mydata
  ID Color Passed
1  1   red   TRUE
2  2 white   TRUE
3  3   red   TRUE
4  4  <NA>  FALSE
```

---

## Data Frames- Accessing data

```
mydata[2:3] # columns 2,3 of data frame
mydata[c("ID","Color")] # columns ID and Age from data frame
mydata$ID # variable x1 in the data frame
```
```
> mydata[2:3] # columns 2,3 of data frame
  Color Passed
1   red   TRUE
2 white   TRUE
3   red   TRUE
4  <NA>  FALSE
> mydata[c("ID","Color")] # columns ID and Age from data frame
  ID Color
1  1   red
2  2 white
3  3   red
4  4  <NA>
> mydata$ID # variable x1 in the data frame
[1] 1 2 3 4
```

---

## Lists

An ordered collection of objects (components). A list allows you to gather a variety of (possibly unrelated) objects under one name.

```
# example of a list with 4 components - 
# a string, a numeric vector, a matrix, and a scaler 
w <- list(name="Fred", mynumbers=d, mymatrix=x, age=5.3)
# example of a list containing two lists 
v <- c(w,w)
```

---

## The List

```
> w
$name
[1] "Fred"

$mynumbers
[1] 1 2 3 4

$mymatrix
     [,1] [,2] [,3] [,4]
[1,]    1    6   11   16
[2,]    2    7   12   17
[3,]    3    8   13   18
[4,]    4    9   14   19
[5,]    5   10   15   20

$age
[1] 5.3
```

---

## Accessing the list

```
> w[[2]] # 2nd component of the list
[1] 1 2 3 4
> w[["mynumbers"]] # component named mynumbers in list
[1] 1 2 3 4
> w$name
[1] "Fred"
```

---

## Factors
Tell R that a variable is nominal by making it a factor. The factor stores the nominal values as a vector of integers in the range [ 1... k ] (where k is the number of unique values in the nominal variable), and an internal vector of character strings (the original values) mapped to these integers.

```
# variable gender with 20 "male" entries and 
# 30 "female" entries 
gender <- c(rep("male",20), rep("female", 30)) 
gender <- factor(gender) 
# stores gender as 20 1s and 30 2s and associates
# 1=female, 2=male internally (alphabetically)
# R now treats gender as a nominal variable 
summary(gender)
```

---

## Some Useful Functions

```
length(mydata) # number of elements or components
str(mydata)    # structure of an object 
names(mydata)  # names

c(mydata,mydata,...)       # combine objects into a vector
cbind(a, a, ...) # combine objects as columns
rbind(a, a, ...) # combine objects as rows 

object     # prints the object

ls()       # list current objects
rm(object) # delete an object
```

---

## Read some flat files

```
# comma separated values
dat.csv <- read.csv("http://www.ats.ucla.edu/stat/data/hsb2.csv")
# tab separated values
dat.tab <- read.table("http://www.ats.ucla.edu/stat/data/hsb2.txt",
  header=TRUE, sep = "\t")
```

---

## Some   *foreign* data types

```
require(foreign)
# SPSS files
dat.spss <- read.spss("http://www.ats.ucla.edu/stat/data/hsb2.sav",
  to.data.frame=TRUE)
# Stata files
dat.dta <- read.dta("http://www.ats.ucla.edu/stat/data/hsb2.dta")
```

---

## Write some data

```
#write.csv(dat.csv, file = "path/to/save/filename.csv")

#write.table(dat.csv, file = "path/to/save/filename.txt", sep = "\t", na=".")

#write.dta(dat.csv, file = "path/to/save/filename.dta")

#write.xlsx(dat.csv, file = "path/to/save/filename.xlsx", sheetName="hsb2")

# save to binary R format (can save multiple datasets and R objects)
#save(dat.csv, dat.dta, dat.spss, dat.txt, file = "path/to/save/filename.RData")
```

---

## ggplot2

```
library(ggplot2)
head(iris) # by default, head displays the first 6 rows. see `?head`
head(iris, n = 10) # we can also explicitly set the number of rows to display
```

```
qplot(Sepal.Length, Petal.Length, data = iris)
# Plot Sepal.Length vs. Petal.Length, using data from the `iris` data frame.
# * First argument `Sepal.Length` goes on the x-axis.
# * Second argument `Petal.Length` goes on the y-axis.
# * `data = iris` means to look for this data in the `iris` data frame.   
```

---

## ggplot2

<iframe src='figures\Rplot.png'></iframe>


---

## Call a python file

```
d<- system('python pyfile.py', intern=TRUE)

```
```
> d
[1] "1"  "19" "3" 
```

---



Sources:

http://www.ats.ucla.edu/stat/r/seminars/intro.htm

















