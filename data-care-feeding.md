Data Care and Feeding
================

<!-- 
use this code for comments between chunks
-->

``` r
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.3     v purrr   0.3.4
    ## v tibble  3.1.1     v dplyr   1.0.5
    ## v tidyr   1.1.3     v stringr 1.4.0
    ## v readr   1.4.0     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(skimr)        ## install.packages("skimr")
#  this is part of tidyverse -- library(dplyr)

library(gapminder)  #install.packages("gapminder")

#
#in console
#   str(gapminder)
#   print(gapminder, n=10)
#   
#   to make a df into tibble use x1 <- as_tibble(original_df)  
#   
#   dim(df) will show dimensions of the df
#   

#simple plot use base R
```

### Simple Plots of Data

``` r
plot(lifeExp ~ year, gapminder)
```

![](data-care-feeding_files/figure-gfm/simple%20plots%20of%20data-1.png)<!-- -->

``` r
plot(lifeExp ~ gdpPercap, gapminder)
```

![](data-care-feeding_files/figure-gfm/simple%20plots%20of%20data-2.png)<!-- -->

``` r
plot(lifeExp ~ log(gdpPercap), gapminder)
```

![](data-care-feeding_files/figure-gfm/simple%20plots%20of%20data-3.png)<!-- -->

``` r
hist(gapminder$lifeExp)
```

![](data-care-feeding_files/figure-gfm/simple%20plots%20of%20data-4.png)<!-- -->

### Looking at Variables

``` r
hist(gapminder$lifeExp)
```

![](data-care-feeding_files/figure-gfm/looking%20at%20variables-1.png)<!-- -->

``` r
summary(gapminder$lifeExp)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   23.60   48.20   60.71   59.47   70.85   82.60

``` r
summary(gapminder$year)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    1952    1966    1980    1980    1993    2007

``` r
table(gapminder$year)
```

    ## 
    ## 1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 2002 2007 
    ##  142  142  142  142  142  142  142  142  142  142  142  142

``` r
#factor Data
summary(gapminder$continent)
```

    ##   Africa Americas     Asia   Europe  Oceania 
    ##      624      300      396      360       24

``` r
table(gapminder$continent)
```

    ## 
    ##   Africa Americas     Asia   Europe  Oceania 
    ##      624      300      396      360       24

``` r
barplot(table(gapminder$continent))
```

![](data-care-feeding_files/figure-gfm/looking%20at%20variables-2.png)<!-- -->

### Demonstration of ggplot

``` r
p <- ggplot(filter(gapminder, continent != "Oceania"),
            aes(x = gdpPercap, y = lifeExp)) # just initializes, creates a base of the data to graph, excludes "Oceania"

p <- p + scale_x_log10() # log the x axis the right way, further defines "p"

p + geom_point() # scatterplot
```

![](data-care-feeding_files/figure-gfm/Demo%20of%20ggplot-1.png)<!-- -->

``` r
p + geom_point(aes(color = continent)) # map continent to color as an aesthetic for a new scatterplot, note that Oceania is not in the legend
```

![](data-care-feeding_files/figure-gfm/Demo%20of%20ggplot-2.png)<!-- -->

``` r
p + geom_point(alpha = (1/3), size = 3) + geom_smooth(lwd = 1.5, se = FALSE)
```

    ## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'

![](data-care-feeding_files/figure-gfm/Demo%20of%20ggplot-3.png)<!-- -->

``` r
#> `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'
# size = diameter of the point (try 13)
# alpha = color density of the point, but not sure what it is based on (try 1/13 or 3)
# lwd = line width
# se = a cloud to illustrate the standard error
# 
#  this would be good code to use with the maple sap data


p + geom_point(alpha = (1/3), size = 3) + facet_wrap(~ continent) +
  geom_smooth(lwd = 1.5, se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](data-care-feeding_files/figure-gfm/Demo%20of%20ggplot-4.png)<!-- -->

``` r
#> `geom_smooth()` using method = 'loess' and formula 'y ~ x'
```
