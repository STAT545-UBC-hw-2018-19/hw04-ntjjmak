hw004\_ntjjmak
================
Nicole Mak
07/10/2018

## There are two tasks for this assignment.

# 1\. Data reshaping.

# 2\. Perform a join.

To start, let’s load the packages to be used for data exploration.

``` r
suppressPackageStartupMessages(library(gapminder))
suppressPackageStartupMessages(library(dplyr))
suppressPackageStartupMessages(library(ggplot2))
```

## Exercise \#1: Reshaping data

The data to be used for the exercise is “gapminder”.

Here is the data set in its original form:

``` r
gapminder
```

    ## # A tibble: 1,704 x 6
    ##    country     continent  year lifeExp      pop gdpPercap
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Afghanistan Asia       1952    28.8  8425333      779.
    ##  2 Afghanistan Asia       1957    30.3  9240934      821.
    ##  3 Afghanistan Asia       1962    32.0 10267083      853.
    ##  4 Afghanistan Asia       1967    34.0 11537966      836.
    ##  5 Afghanistan Asia       1972    36.1 13079460      740.
    ##  6 Afghanistan Asia       1977    38.4 14880372      786.
    ##  7 Afghanistan Asia       1982    39.9 12881816      978.
    ##  8 Afghanistan Asia       1987    40.8 13867957      852.
    ##  9 Afghanistan Asia       1992    41.7 16317921      649.
    ## 10 Afghanistan Asia       1997    41.8 22227415      635.
    ## # ... with 1,694 more rows

To practise reshaping the data,

``` r
summary(ChickWeight)
```

    ##      weight           Time           Chick     Diet   
    ##  Min.   : 35.0   Min.   : 0.00   13     : 12   1:220  
    ##  1st Qu.: 63.0   1st Qu.: 4.00   9      : 12   2:120  
    ##  Median :103.0   Median :10.00   20     : 12   3:120  
    ##  Mean   :121.8   Mean   :10.72   10     : 12   4:118  
    ##  3rd Qu.:163.8   3rd Qu.:16.00   17     : 12          
    ##  Max.   :373.0   Max.   :21.00   19     : 12          
    ##                                  (Other):506
