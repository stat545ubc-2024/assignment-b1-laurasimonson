Assignment B1
================
2024-10-29

# Assignment B1 - Stat 545B

#### By Laura Simonson

Assignment B1 covers making a function, documenting it, and testing it.
The purpose of making functions in R is to avoid repeatedly duplicating
code, which is important to shorten code and makes the code easier to
correct.

### Exercise 1: Making a Function & Exercise 2: Documenting the Function

First load the required packages for this assignment

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(testthat)
```

    ## 
    ## Attaching package: 'testthat'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     matches

``` r
library(devtools)
```

    ## Loading required package: usethis

    ## 
    ## Attaching package: 'devtools'

    ## The following object is masked from 'package:testthat':
    ## 
    ##     test_file

I am creating a function that will calculate the mean, median and range
for numeric values of any given dataset.

The function is documented with the roxygen2 skeleton, which contains
title, parameters, details, return, and example sections.

``` r
#' Mean, Median and Range Function
#' @description This function will calculate the mean, median and range values for numeric vectors.
#' @param x is the numeric vectors of interest.  
#' @param na.rm is a logical value to indicate whether NA values should be removed before computation. The default is false. 
#' @details This function will return an error message for any non-numeric values that are inputted. 
#' @return This function will return a vector with 4 items. The following elements will be returned:
#' \item{a}{The mean of the numbers in data set.}
#' \item{b}{The median of the numbers in data set.}
#' \item{c}{The range of the numbers in data set, represented as the last two numbers in the return, the minimum and maximum values.}
#' @examples This function can be used for data sets with NA values and for datasets without NA values
#' With NA values
#' mean_median_range(c(1, 2, 3, 4, 5, NA, 6), na.rm = TRUE)
#' Without NA values
#' mean_median_range(c(10, 20, 30, 40, 50))

mean_median_range <- function(x, na.rm = FALSE){
  if(!is.numeric(x)){
    stop("Input is not numeric, this function requires numeric values.")
    }
  a = mean(x, na.rm = na.rm)
  b = median(x, na.rm = na.rm)
  c = range(x, na.rm = na.rm)
  c(a,b,c(c))
}
```

Now that mean, median and range function has been created and
documented, we can use it to find these values of data sets.

### Exercise 3: Include Examples

#### Example 1

We can create a data set with numerical values that the
mean_median_range function can calculate the mean, median and range
values of.

``` r
ex_dataset <- c(1, 2, 3, 5, 7, 9, 11, 12, 13, 14, 15, 17, 19, 20) # Data set with random numbers 

mean_median_range(ex_dataset)
```

    ## [1] 10.57143 11.50000  1.00000 20.00000

The function tells us that in this example dataset, the mean is 10.571,
the median is 11.5, and the range is between 1 and 20.

#### Example 2

We can also use the mean_median_range function to calculate these values
of a numerical category within an already existing dataset. For example,
in the palmer penguins dataset, we can use this function to find the
mean, median and mode of body_mass_g of the penguins.

First load the palmerpenguins dataset

``` r
library(palmerpenguins)
```

``` r
mean_median_range(penguins$body_mass_g, na.rm = TRUE) 
```

    ## [1] 4201.754 4050.000 2700.000 6300.000

``` r
# use the $ to find the body_mass_g category within the penguins dataset 
# set na.rm equal to TRUE so that the NA values in this category are ignored by the function, otherwise the mean, median and range are calculated as NA. 
```

The function tells us that in the body_mass_g category in the palmer
penguins dataset, the mean is 4201.754, the median is 4050, and the
range is between 2700 and 6300.

#### Example 3

We cannot use this function to find the mean, median and range of a
category that is not numeric. For example, in the palmer penguins
dataset, this function would not work if it was asked to find the mean,
median and range of the species column.

``` r
mean_median_range(penguins$species)
```

    ## Error in mean_median_range(penguins$species): Input is not numeric, this function requires numeric values.

The error message tells us that “Input is not numeric, this function
requires numeric values.” and we are therefore unable to calculate the
mean, median and range of this categorical variable in the palmer
penguins dataset.

### Exercise 4: Test the Function

Testing that the function created works is important to ensure that the
function works as it was intended to and to help pinpoint any errors if
the function does not work as expected.

#### Test 1

We can first test that the mean_median_range function works correctly
when tested on a vector that contains no NA values, such as a data set
containing the numbers 1 to 10.

``` r
test_that("mean_median_range function works correctly with no NA's", {
firsttest <- mean_median_range(1:10)
  expect_equal(firsttest[1], 5.5)
  expect_equal(firsttest[2], 5.5)
  expect_equal(firsttest[3:4], c(1, 10))
})
```

    ## Test passed 🌈

We see a test passed message come up after running the code, indicating
that there is no errors when the function is used on a dataset that does
not have any missing values.

#### Test 2

Next, we can check how the mean_median and range function handles
missing values by removing the missing values in one case (part 1) and
keeping them in another (part 2), using a dataset that contains the
numbers 1 to 5 and a NA value.

``` r
test_that("mean_median_range function works correctly with NA's", {
second1test <- mean_median_range(c(1:5, NA), na.rm = TRUE)
  expect_equal(second1test[1], 3)
  expect_equal(second1test[2], 3)
  expect_equal(second1test[3:4], c(1, 5))

second2test <- mean_median_range(c(1:5, NA))
  expect_equal(second2test[1], NA_real_)   
  expect_equal(second2test[2], NA_real_)    
  expect_equal(second2test[3:4], c(NA_real_, NA_real_))
})
```

    ## Test passed 🌈

The test passed message comes up after running the code, showing that
the function can properly handle removing NA values from a data set and
keeping the NA values in the dataset.

#### Test 3

We can test that the function will not work if the input of the function
is characters and not numeric, such as with a data set that contains
different kinds of fruit.

``` r
test_that("mean_median_range function does not work when input is not numeric", {
expect_error(mean_median_range(c("apple", "banana", "strawberry", "grape")), "Input is not numeric, this function requires numeric values.")
})
```

    ## Test passed 🥇

We see the test passed message come up again after testing this
function, indicating that when the data is categorical or characters,
the stop message will come up and the function will not calculate the
mean, median and range.

#### Test 4

The mean_median_range function has an expected output of 4 values, 1 for
mean, 1 for median and 2 values for range. We can verify that the
function does produce the output of the expected length using a vector
that has no NA’s.

``` r
test_that("mean_median_range function returns an output of the correct length", {
fourthtest <- mean_median_range(1:10)
  expect_length(fourthtest, 4)
})
```

    ## Test passed 🎉

The test passed message shows up after this code chunk, indicating that
the function does produce the expected outcome length with 4 variables.
