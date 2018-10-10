hw004\_ntjjmak
================
Nicole Mak
07/10/2018

### There are two tasks for this assignment.

1.  Data reshaping.
2.  Perform a join.

To start, let’s load the packages to be used for data exploration.

``` r
suppressPackageStartupMessages(library(gapminder))
suppressPackageStartupMessages(library(dplyr))
suppressPackageStartupMessages(library(ggplot2))
suppressPackageStartupMessages(library(tidyverse))
suppressPackageStartupMessages(library(knitr))
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

To practise reshaping the data, I have selected prompt \#2. I have not
yet tried `knitr::kable()`, so this is a good chance. Here are the
exercise instructions:

*Make a tibble with one row per year and columns for life expectancy for
two or more countries. Use `knitr::kable()` to make this table look
pretty in your rendered homework. Take advantage of this new data shape
to scatterplot life expectancy for one country against that of another.*

**First, let’s use `dplyr` to get the information we want to focus on.
We will select for the variables (i.e. columns) we want, make sure it is
grouped by country, and filter only for the countries desired. This will
be stored under “reshape”.**

``` r
reshape <- gapminder %>% 
  select(year, country, lifeExp)%>% 
  group_by(country)%>% 
  filter(country == "Canada" | country == "France" | country == "Japan")
```

**Now we can reformat this so that there is only one row per year and
present this data in a table by using `knitr::kable()`. We will round to
the nearest decimal point.**

``` r
spread(reshape, key = country, value = lifeExp) %>% 
  knitr:: kable(format = "markdown", justify = "centre", digits = 1, caption = "Life expectancy 1952-2007 for selected countries: Canada, France, and Japan.")
```

| year | Canada | France | Japan |
| ---: | -----: | -----: | ----: |
| 1952 |   68.8 |   67.4 |  63.0 |
| 1957 |   70.0 |   68.9 |  65.5 |
| 1962 |   71.3 |   70.5 |  68.7 |
| 1967 |   72.1 |   71.5 |  71.4 |
| 1972 |   72.9 |   72.4 |  73.4 |
| 1977 |   74.2 |   73.8 |  75.4 |
| 1982 |   75.8 |   74.9 |  77.1 |
| 1987 |   76.9 |   76.3 |  78.7 |
| 1992 |   78.0 |   77.5 |  79.4 |
| 1997 |   78.6 |   78.6 |  80.7 |
| 2002 |   79.8 |   79.6 |  82.0 |
| 2007 |   80.7 |   80.7 |  82.6 |

**This same data may also be presented nicely with a scatter plot.**

``` r
reshape %>% 
  ggplot(aes(year, lifeExp))+
  geom_point(aes(colour = country))+
  theme_classic()+
  ggtitle("Life Expectancy from 1952-2007")+
  ylab("Life Expectancy (years)")+
  xlab("Year")
```

![](hw04-ntjjmak_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

### The next exercise will be to explore `join`. Here are the instructions for the exercise: Create your own cheatsheet patterned after Jenny’s but focused on something you care about more than comics\!

**First, create data frames. The theme for this is movie stars. Start by
making vectors for each variable. This code chunk shows one way to make
a data
frame:**

``` r
Name <- c('Harrison Ford', 'Gal Gadot', 'Jackie Chan', 'Emma Thompson', 'Leonardo DiCaprio', 'Emily Blunt', 'Natalie Portman')
Sex <- c('M', 'F', 'M', 'F', 'M', 'F', 'F')
Notable_movie <- c('Indiana Jones', 'Wonder Woman', 'Rush Hour', 'Sense and Sensibility', 'Titanic', 'Sicario', 'Star Wars')

Actor.data <- data.frame(Name, Sex, Notable_movie)
```

**This code chunk shows an alternative way to code a data frame.**

``` r
Movie.data <- data_frame(
  Notable_movie =  c('Indiana Jones', 'Wonder Woman', 'Rush Hour', 'Sense and Sensibility', 'Titanic', 'Star Wars', 'The Red Violin', 'Avengers'),
  Genre_of_movie = c('Action', 'Superhero', 'Action', 'Romance', 'Romance', 'SciFi', 'Drama', 'Superhero'))
```

**Next, code the data frames and format them as a tibble. We will store
them as table “x” and table “y”.**

``` r
x <- as.tibble(Actor.data)
y <- as.tibble(Movie.data)
```

**We can even display the as nicer tables using `knitr`**

``` r
as.tibble(x) %>% 
  knitr:: kable(format = "markdown", justify = "centre")
```

| Name              | Sex | Notable\_movie        |
| :---------------- | :-- | :-------------------- |
| Harrison Ford     | M   | Indiana Jones         |
| Gal Gadot         | F   | Wonder Woman          |
| Jackie Chan       | M   | Rush Hour             |
| Emma Thompson     | F   | Sense and Sensibility |
| Leonardo DiCaprio | M   | Titanic               |
| Emily Blunt       | F   | Sicario               |
| Natalie Portman   | F   | Star Wars             |

``` r
as.tibble(y) %>% 
  knitr:: kable(format = "markdown", justify = "centre")
```

| Notable\_movie        | Genre\_of\_movie |
| :-------------------- | :--------------- |
| Indiana Jones         | Action           |
| Wonder Woman          | Superhero        |
| Rush Hour             | Action           |
| Sense and Sensibility | Romance          |
| Titanic               | Romance          |
| Star Wars             | SciFi            |
| The Red Violin        | Drama            |
| Avengers              | Superhero        |

**Let’s try different forms of joining to see how our data is
re-formatted.**

**First up, `inner_join`. Inner join takes all matching rows from “x”
and adds the additional columns from “y” that correspond to them. Notice
that only rows from “x” that had corresponding data from “y” are
included. Therefore, Emily Blunt no longer appears in the joined data.**

``` r
inner_join(x, y) %>% 
  knitr:: kable(format = "markdown", justify = "centre")
```

    ## Joining, by = "Notable_movie"

    ## Warning: Column `Notable_movie` joining factor and character vector,
    ## coercing into character vector

| Name              | Sex | Notable\_movie        | Genre\_of\_movie |
| :---------------- | :-- | :-------------------- | :--------------- |
| Harrison Ford     | M   | Indiana Jones         | Action           |
| Gal Gadot         | F   | Wonder Woman          | Superhero        |
| Jackie Chan       | M   | Rush Hour             | Action           |
| Emma Thompson     | F   | Sense and Sensibility | Romance          |
| Leonardo DiCaprio | M   | Titanic               | Romance          |
| Natalie Portman   | F   | Star Wars             | SciFi            |

**Next we have `semi_join`. Again, only rows from “x” with corresponding
data in “y” will appear. Furthermore, `semi_join` does not display any
columns from “y”. It only shows you the data for the common rows between
the two merged data frames.**

``` r
semi_join(Actor.data, Movie.data) %>% 
  knitr:: kable(format = "markdown", justify = "centre")
```

    ## Joining, by = "Notable_movie"

    ## Warning: Column `Notable_movie` joining factor and character vector,
    ## coercing into character vector

| Name              | Sex | Notable\_movie        |
| :---------------- | :-- | :-------------------- |
| Harrison Ford     | M   | Indiana Jones         |
| Gal Gadot         | F   | Wonder Woman          |
| Jackie Chan       | M   | Rush Hour             |
| Emma Thompson     | F   | Sense and Sensibility |
| Leonardo DiCaprio | M   | Titanic               |
| Natalie Portman   | F   | Star Wars             |

**Let’s see what happens when we do `left_join` and `right_join` and
compare the two.**

``` r
left_join(x, y) %>% 
  knitr:: kable(format = "markdown", justify = "centre")
```

    ## Joining, by = "Notable_movie"

    ## Warning: Column `Notable_movie` joining factor and character vector,
    ## coercing into character vector

| Name              | Sex | Notable\_movie        | Genre\_of\_movie |
| :---------------- | :-- | :-------------------- | :--------------- |
| Harrison Ford     | M   | Indiana Jones         | Action           |
| Gal Gadot         | F   | Wonder Woman          | Superhero        |
| Jackie Chan       | M   | Rush Hour             | Action           |
| Emma Thompson     | F   | Sense and Sensibility | Romance          |
| Leonardo DiCaprio | M   | Titanic               | Romance          |
| Emily Blunt       | F   | Sicario               | NA               |
| Natalie Portman   | F   | Star Wars             | SciFi            |

``` r
right_join(x, y) %>% 
  knitr:: kable(format = "markdown", justify = "centre")
```

    ## Joining, by = "Notable_movie"

    ## Warning: Column `Notable_movie` joining factor and character vector,
    ## coercing into character vector

| Name              | Sex | Notable\_movie        | Genre\_of\_movie |
| :---------------- | :-- | :-------------------- | :--------------- |
| Harrison Ford     | M   | Indiana Jones         | Action           |
| Gal Gadot         | F   | Wonder Woman          | Superhero        |
| Jackie Chan       | M   | Rush Hour             | Action           |
| Emma Thompson     | F   | Sense and Sensibility | Romance          |
| Leonardo DiCaprio | M   | Titanic               | Romance          |
| Natalie Portman   | F   | Star Wars             | SciFi            |
| NA                | NA  | The Red Violin        | Drama            |
| NA                | NA  | Avengers              | Superhero        |

**What do you notice?**

`Left_join` will include all rows of data from “x” and add new columns
from “y”. Any missing matches in the new column pulled from “y” will be
left blank as an *NA*. Such is the case for the movie “Sicario” which
does not appear in the “y” data. Furthermore, “The Red Violin” and
“Avengers” are not rows in “x” and are not even displayed.

`Right_join` is essentially the opposite of `left_join`. It includes all
data from the “y” rows and adds on the columns from “x”. Again, any “x”
data that does not correspond with “y” is left blank and replaced with
an *NA*. Here, we see the “Red Violin” and “Avengers” make their
re-appearance while “Emily Blunt” disappears once again because she does
not have a corresponding row in “y”.

**Let’s try `anti_join` which will filter out all rows in “x” that had
shared data with “y”. We are left with the original “x” columns and only
rows that did not have a “y” match.**

``` r
anti_join(x, y) %>% 
  knitr:: kable(format = "markdown", justify = "centre")
```

    ## Joining, by = "Notable_movie"

    ## Warning: Column `Notable_movie` joining factor and character vector,
    ## coercing into character vector

| Name        | Sex | Notable\_movie |
| :---------- | :-- | :------------- |
| Emily Blunt | F   | Sicario        |

**Last, but not least, we have `full_join`. True to its name, this
requests that all rows of data and columns from both sets are
represented. Missing data is displayed as *NA*.**

``` r
full_join(x, y) %>% 
  knitr:: kable(format = "markdown", justify = "centre")
```

    ## Joining, by = "Notable_movie"

    ## Warning: Column `Notable_movie` joining factor and character vector,
    ## coercing into character vector

| Name              | Sex | Notable\_movie        | Genre\_of\_movie |
| :---------------- | :-- | :-------------------- | :--------------- |
| Harrison Ford     | M   | Indiana Jones         | Action           |
| Gal Gadot         | F   | Wonder Woman          | Superhero        |
| Jackie Chan       | M   | Rush Hour             | Action           |
| Emma Thompson     | F   | Sense and Sensibility | Romance          |
| Leonardo DiCaprio | M   | Titanic               | Romance          |
| Emily Blunt       | F   | Sicario               | NA               |
| Natalie Portman   | F   | Star Wars             | SciFi            |
| NA                | NA  | The Red Violin        | Drama            |
| NA                | NA  | Avengers              | Superhero        |

### All of these “join” functions were from the `dplyr` universe. What about the “merge” function from base R?

**Let’s try it.**

``` r
merge(x, y)
```

    ##           Notable_movie              Name Sex Genre_of_movie
    ## 1         Indiana Jones     Harrison Ford   M         Action
    ## 2             Rush Hour       Jackie Chan   M         Action
    ## 3 Sense and Sensibility     Emma Thompson   F        Romance
    ## 4             Star Wars   Natalie Portman   F          SciFi
    ## 5               Titanic Leonardo DiCaprio   M        Romance
    ## 6          Wonder Woman         Gal Gadot   F      Superhero

``` r
merge(y, x)
```

    ##           Notable_movie Genre_of_movie              Name Sex
    ## 1         Indiana Jones         Action     Harrison Ford   M
    ## 2             Rush Hour         Action       Jackie Chan   M
    ## 3 Sense and Sensibility        Romance     Emma Thompson   F
    ## 4             Star Wars          SciFi   Natalie Portman   F
    ## 5               Titanic        Romance Leonardo DiCaprio   M
    ## 6          Wonder Woman      Superhero         Gal Gadot   F

**What we notice is that the merge function returns the same information
as inner\_join. However, when requesting the coding for the joining of
tables, the sequence of columns on display is not affected by the
written code. Check out the code chunk below and notice that
`inner_join(x, y)` does not return the same results as `inner_join(y,
x)`\! That is, the column order is affected by how you code
    it.**

``` r
inner_join(x, y)
```

    ## Joining, by = "Notable_movie"

    ## Warning: Column `Notable_movie` joining factor and character vector,
    ## coercing into character vector

    ## # A tibble: 6 x 4
    ##   Name              Sex   Notable_movie         Genre_of_movie
    ##   <fct>             <fct> <chr>                 <chr>         
    ## 1 Harrison Ford     M     Indiana Jones         Action        
    ## 2 Gal Gadot         F     Wonder Woman          Superhero     
    ## 3 Jackie Chan       M     Rush Hour             Action        
    ## 4 Emma Thompson     F     Sense and Sensibility Romance       
    ## 5 Leonardo DiCaprio M     Titanic               Romance       
    ## 6 Natalie Portman   F     Star Wars             SciFi

``` r
inner_join(y, x)
```

    ## Joining, by = "Notable_movie"

    ## Warning: Column `Notable_movie` joining character vector and factor,
    ## coercing into character vector

    ## # A tibble: 6 x 4
    ##   Notable_movie         Genre_of_movie Name              Sex  
    ##   <chr>                 <chr>          <fct>             <fct>
    ## 1 Indiana Jones         Action         Harrison Ford     M    
    ## 2 Wonder Woman          Superhero      Gal Gadot         F    
    ## 3 Rush Hour             Action         Jackie Chan       M    
    ## 4 Sense and Sensibility Romance        Emma Thompson     F    
    ## 5 Titanic               Romance        Leonardo DiCaprio M    
    ## 6 Star Wars             SciFi          Natalie Portman   F

### Thanks for having a look at this assignment\!
