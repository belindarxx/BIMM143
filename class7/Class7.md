Class 7 R Functions and packages
================
Belinda Xue
10/22/2019

# R Functions Revisited

Source my functions from last day

``` r
source("http://tinyurl.com/rescale-R")
# function that run another file/source
# online file or can be local file
# the glasses on the tab name means "read only"
```

``` r
rescale(1:10)
```

    ##  [1] 0.0000000 0.1111111 0.2222222 0.3333333 0.4444444 0.5555556 0.6666667
    ##  [8] 0.7777778 0.8888889 1.0000000

``` r
# take all numerical input and expel to 0-10
```

``` r
rescale(c(1,10,5,NA,6))
```

    ## [1] 0.0000000 1.0000000 0.4444444        NA 0.5555556

``` r
# na.rm default is false
# but rescale function have na.rm= TRUE, so fix the NA already; otherwise will be all NA
```

``` r
# is.numeric is asking whether those are numbers
is.numeric(1:10)
```

    ## [1] TRUE

``` r
# asking wheter those are numbers
is.numeric(c(1,5,NA,10))
```

    ## [1] TRUE

``` r
is.numeric(c(1,5,NA,"bb"))
```

    ## [1] FALSE

``` r
# ! filp the orignal answers; from T to F
!is.numeric(c(1,5,NA,"bb"))
```

    ## [1] TRUE

``` r
# orignal is false, but with ! would be true
!is.numeric(c(1,5,NA,10))
```

    ## [1] FALSE

``` r
# orginail is true, but with ! would be False
```

the **\!**

``` r
# rescale2(c(1:10, "bb")) give you error
# would said "Error: Input x should be numeric"
# rescale2 only want numbers!! 
```

## In-class example of writing function\! both\_na() example

Question is “How many TRUE values are there?” Write a function to find
where there are NA elements in two input vectors

First make some simple input where I know the answer

``` r
# Lets define an example x and y
x <- c( 1, 2, NA, 3, NA) 
y <- c(NA,3,NA,3, 4)
```

Look online and found the **is.na()** function And the **which()**
fucntion tells me where the TRUE values are

``` r
is.na(x)
```

    ## [1] FALSE FALSE  TRUE FALSE  TRUE

``` r
# give you either true or false for all vectors
# True thing is where NA is 
which(is.na(x))
```

    ## [1] 3 5

``` r
# tell you exactly which element of vector is NA
# try with y too
is.na(y)
```

    ## [1]  TRUE FALSE  TRUE FALSE FALSE

``` r
which(is.na(y))
```

    ## [1] 1 3

The AND function requires two input TRUE to give a
TRUE

``` r
is.na(x) & is.na(y)
```

    ## [1] FALSE FALSE  TRUE FALSE FALSE

``` r
# the & symbol... only give you TRUE when both vector is TRUE; only input is NA will give you TRUE; only one NA? give you FALSE
```

Taking the **sum()** of TRUE FALSE vector will tell me how many TRUE
elements I have. This is my working snippet\!\!

``` r
sum(is.na(x) & is.na(y))
```

    ## [1] 1

``` r
# sum up numbers of TRUE
sum(c(TRUE, TRUE, FALSE, TRUE))
```

    ## [1] 3

### Now turn it into a function\!

``` r
both_na <- function(x, y) {
  # BODY is the statement/ working snippet
  sum(is.na(x) & is.na(y))
}
```

``` r
both_na(x, y)
```

    ## [1] 1

Test Function

``` r
 x <-  c(NA, NA, NA)
y1 <- c(1, NA, NA)
y2 <- c(1, NA, NA, NA)
```

``` r
both_na(x, y1)
```

    ## [1] 2

``` r
# 有两个共同的TRUE; cuz got two column of NA
both_na(x, y2)
```

    ## Warning in is.na(x) & is.na(y): longer object length is not a multiple of
    ## shorter object length

    ## [1] 3

``` r
# will give you ?? cuz y2 is longer than x
# x is not as long as y2, will recycle x
```

``` r
x2 <- c(NA,NA)
both_na(x2, y2)
```

    ## [1] 3

Side note: This is re-cycle example of the colors

``` r
plot(1:10, col=c("red","blue","green"))
```

![](Class7_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

``` r
# gonna recycle the color red and blue for each dot
# shorter vector will align with teh longer vector
```

``` r
 x <-  c(NA, NA, NA)
y3 <- c(1, NA, NA, NA, NA, NA, NA)
both_na(x, y3)
```

    ## Warning in is.na(x) & is.na(y): longer object length is not a multiple of
    ## shorter object length

    ## [1] 6

``` r
# will make x the same length as y3
# view x as NA NA NA (NA NA NA NA)
# should get 6

x <-  c(1, NA, NA)
y3 <- c(1, NA, NA, NA, NA, NA, NA)
both_na(x, y3)
```

    ## Warning in is.na(x) & is.na(y): longer object length is not a multiple of
    ## shorter object length

    ## [1] 4

``` r
# will make x the same length as y3
# view x as 1 NA NA (1 NA NA 1)
# same as this x <- c(1, NA, NA, 1, NA, NA, 1)
# should get 4
```

``` r
length(x)
```

    ## [1] 3

``` r
length(y3)
```

    ## [1] 7

``` r
# tell me how long is the x or y3
# match them? will get recylce problem

7 == 7
```

    ## [1] TRUE

``` r
7 != 7
```

    ## [1] FALSE

``` r
# does 7 equal to 7
# does 7 NOT equal to 7
```

``` r
both_na2 <- function(x, y) {
  if(length(x) != length(y)) {
    stop("Inputs x and y should be the same length!")
    # the stop is where you input your error messange
  }
  sum(is.na(x) & is.na(y))
}
```

``` r
# both_na2(x, y3)
# test # 
```

# Practice writing function\! Grade example

``` r
# Student 1
c(100, 100, 100, 100, 100, 100, 100, 90)
```

    ## [1] 100 100 100 100 100 100 100  90

``` r
# Student 2
c(100, NA, 90, 90, 90, 90, 97, 80)
```

    ## [1] 100  NA  90  90  90  90  97  80

Name the vectors

``` r
s1 <- c(100, 100, 100, 100, 100, 100, 100, 90)
s2 <- c(100, NA, 90, 90, 90, 90, 97, 80)
```

me testing some function

``` r
drop_lowest <- sum(s1) - min(s1)
mean(s1)
```

    ## [1] 98.75

Student 1 grades

``` r
# which number in s1 is the lowest?
s1 [which.min(s1)]
```

    ## [1] 90

``` r
# a - sign give you everthing except the min 90
s1 [ -which.min(s1)]
```

    ## [1] 100 100 100 100 100 100 100

``` r
# take the mean of that => give you s1 avg after dropping the lowest grade
mean (s1 [ -which.min(s1)])
```

    ## [1] 100

Student 2 Grades **THIS DOES NOT WORK WHEN WE HAVE NA\!\! :(**

``` r
# which number in s1 is the lowest?
s2 [which.min(s2)]
```

    ## [1] 80

``` r
# a - sign give you everthing except the min 80
s2 [ -which.min(s2)]
```

    ## [1] 100  NA  90  90  90  90  97

``` r
# take the mean of that => give you s1 avg after dropping the lowest grade
mean (s2 [ -which.min(s2)])
```

    ## [1] NA

Need to fix the NA for student 2\!

``` r
# give you the total length??
which.min(s2)
```

    ## [1] 8

``` r
# which number in s1 is the lowest?
s2 [which.min(s2)]
```

    ## [1] 80

``` r
# a - sign give you everthing except the min 80
s2 [ -which.min(s2)]
```

    ## [1] 100  NA  90  90  90  90  97

``` r
# take the mean of that => give you s1 avg after dropping the lowest grade
# ignore the NA by na.rm = TRUE
mean (s2 [ -which.min(s2)], na.rm= TRUE)
```

    ## [1] 92.83333

``` r
# check whether s1 or s1 have NA using "ANY"
any(is.na(s1))
```

    ## [1] FALSE

``` r
any(is.na(s2)) 
```

    ## [1] TRUE

#### We have our working code\! Now turn it into a first function\!

``` r
grade <- function(x) {
  if( any(is.na(x)) ) {
    warning("Student is missing a homework!")
  }
  mean (x [ -which.min(x)], na.rm= TRUE)
  }
```

``` r
grade(s1)
```

    ## [1] 100

``` r
grade(s2)
```

    ## Warning in grade(s2): Student is missing a homework!

    ## [1] 92.83333

###### ???? another example??

``` r
grade2 <- function(x) {
  if( any(is.na(x)) ) {
    warning("Student is missing a homework!")
  }
  sum (x [ -which.min(x)], na.rm= TRUE) / (length(x)-1)
}
```

``` r
s3 <- c(100, NA, NA, NA, NA)
grade2(s3)
```

    ## Warning in grade2(s3): Student is missing a homework!

    ## [1] 0

#### side note of the grade example…

``` r
url <- "https://tinyurl.com/gradeinput"
hw <- read.csv(url, row.names=1)
```

``` r
apply(hw, 1, grade)
```

    ## Warning in FUN(newX[, i], ...): Student is missing a homework!
    
    ## Warning in FUN(newX[, i], ...): Student is missing a homework!
    
    ## Warning in FUN(newX[, i], ...): Student is missing a homework!
    
    ## Warning in FUN(newX[, i], ...): Student is missing a homework!

    ##  student-1  student-2  student-3  student-4  student-5  student-6 
    ##   91.75000   82.50000   84.25000   88.00000   88.25000   89.00000 
    ##  student-7  student-8  student-9 student-10 student-11 student-12 
    ##   94.00000   93.75000   87.75000   81.33333   86.00000   91.75000 
    ## student-13 student-14 student-15 student-16 student-17 student-18 
    ##   92.25000   87.75000   83.33333   89.50000   88.00000   97.00000 
    ## student-19 student-20 
    ##   82.75000   82.75000

``` r
# apply (x, margin, function, ...)
```

# Collabrative CRAN packages

``` r
# Go to class website and find Lec 7 "Collaborative Google Doc based notes on selected R packages", click the link inside the doc
# our group is doing ggplot2 package
# install using "install.packages("tidyverse")"
# read the package using "library(ggplot2)"
library(ggplot2)
ggplot(mpg, aes(displ, hwy, colour = class)) + 
  geom_point()
```

![](Class7_files/figure-gfm/unnamed-chunk-33-1.png)<!-- -->

``` r
# example of plotting the graph using ggplot2
```
