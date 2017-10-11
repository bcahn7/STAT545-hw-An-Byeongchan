# STAT545-hw04-An-Byeongchan




```r
suppressPackageStartupMessages(library(tidyverse))
```

```
## Warning: package 'tidyverse' was built under R version 3.4.2
```

```r
suppressPackageStartupMessages(library(gapminder))
```


### Choose your own adventure

- Pick a join prompt and do it.
I used the dataset `areas` which was dealt with in class. I tried to combine gapminder data in 2007 with `areas`. As I used right_join(), `g1` preserves all the rows of `areas`. Here, I did not specify a character vector of variables to join by using `by = "country"`. This was because there was only one variable in common. 
In addition, I compared `full_join()` with `left_join()`. Because `gapminder` does not have `"Vatican City"` which is included in `areas`, `full_join()` creates one more observation (which is for `Vatican City`), compared to `left_join()`

```r
areas <- data.frame(country=c("Canada", "United States", "India", "Vatican City"),
                     area=c(998.5*10^6, 983.4*10^6, 328.7*10^6, 44))

g1 <- gapminder %>% 
  filter(year == 2007) %>% 
  right_join(areas)
```

```
## Joining, by = "country"
```

```
## Warning: Column `country` joining factors with different levels, coercing
## to character vector
```

```r
g1
```

```
## # A tibble: 4 x 7
##         country continent  year lifeExp        pop gdpPercap      area
##           <chr>    <fctr> <int>   <dbl>      <int>     <dbl>     <dbl>
## 1        Canada  Americas  2007  80.653   33390141  36319.24 998500000
## 2 United States  Americas  2007  78.242  301139947  42951.65 983400000
## 3         India      Asia  2007  64.698 1110396331   2452.21 328700000
## 4  Vatican City      <NA>    NA      NA         NA        NA        44
```

```r
# The number of observations using full_join()
nrow(full_join(gapminder, areas, by = "country"))
```

```
## Warning: Column `country` joining factors with different levels, coercing
## to character vector
```

```
## [1] 1705
```

```r
# The number of observations using left_join()
nrow(left_join(gapminder, areas, by = "country"))
```

```
## Warning: Column `country` joining factors with different levels, coercing
## to character vector
```

```
## [1] 1704
```

- Pick one of the data reshaping prompts and do it.
I trid to use `gather()` for long format and `spread()` for wide format.

```r
g2 <- g1 %>% 
  select(country, continent, pop, gdpPercap, area) %>% 
  gather(key = "Measures", value = "My_value", pop, gdpPercap, area)
g2
```

```
## # A tibble: 12 x 4
##          country continent  Measures     My_value
##            <chr>    <fctr>     <chr>        <dbl>
##  1        Canada  Americas       pop 3.339014e+07
##  2 United States  Americas       pop 3.011399e+08
##  3         India      Asia       pop 1.110396e+09
##  4  Vatican City      <NA>       pop           NA
##  5        Canada  Americas gdpPercap 3.631924e+04
##  6 United States  Americas gdpPercap 4.295165e+04
##  7         India      Asia gdpPercap 2.452210e+03
##  8  Vatican City      <NA> gdpPercap           NA
##  9        Canada  Americas      area 9.985000e+08
## 10 United States  Americas      area 9.834000e+08
## 11         India      Asia      area 3.287000e+08
## 12  Vatican City      <NA>      area 4.400000e+01
```

```r
g2 %>% 
  spread(key = "Measures", value = "My_value")
```

```
## # A tibble: 4 x 5
##         country continent      area gdpPercap        pop
## *         <chr>    <fctr>     <dbl>     <dbl>      <dbl>
## 1        Canada  Americas 998500000  36319.24   33390141
## 2         India      Asia 328700000   2452.21 1110396331
## 3 United States  Americas 983400000  42951.65  301139947
## 4  Vatican City      <NA>        44        NA         NA
```


### General data reshaping and relationship to aggregation

__Problem__: You have data in one "shape" but you wish it were in another. Usually this is because the alternative shape is superior for presenting a table, making a figure, or doing aggregation and statistical analysis.

__Solution__: Reshape your data. For simple reshaping, `gather()` and `spread()` from `tidyr` will suffice. Do the thing that it possible / easier now that your data has a new shape.

__Prompts__:

Activity #1
- two `tidyr` functions
1. `gather(key = "key", value = "value", ...)`

2. `spread(key = "key", value = "value", ...)`
Make sure that there is no duplicate to use `spread()`. When there are more-than-one observations (which have same values except for "key" values) for the same "key" value, the function does not work. This can be fixed by distinguishing each observation using other variables or using `dcast()` putting the mean, variance, or sum to the value (`dcast()` is the function in `reshape2`)

Tyler Rinker's [minimal guide to `tidyr`](https://github.com/trinker/tidyr_in_a_nutshell).

Activity #2
  * Make a tibble with one row per year and columns for life expectancy for two or more countries.
    - Use `knitr::kable()` to make this table look pretty in your rendered homework.
    - Take advantage of this new data shape to scatterplot life expectancy for one country against that of another.


```r
g3 <- gapminder %>% 
  select(country, year, lifeExp) %>% 
  filter(country %in% c("Korea, Rep.", "Japan", "Canada", "Australia")) %>% 
  spread(key = "country", value = "lifeExp")
knitr::kable(g3, format = "markdown")
```



| year| Australia| Canada|  Japan| Korea, Rep.|
|----:|---------:|------:|------:|-----------:|
| 1952|    69.120| 68.750| 63.030|      47.453|
| 1957|    70.330| 69.960| 65.500|      52.681|
| 1962|    70.930| 71.300| 68.730|      55.292|
| 1967|    71.100| 72.130| 71.430|      57.716|
| 1972|    71.930| 72.880| 73.420|      62.612|
| 1977|    73.490| 74.210| 75.380|      64.766|
| 1982|    74.740| 75.760| 77.110|      67.123|
| 1987|    76.320| 76.860| 78.670|      69.810|
| 1992|    77.560| 77.950| 79.360|      72.244|
| 1997|    78.830| 78.610| 80.690|      74.647|
| 2002|    80.370| 79.770| 82.000|      77.045|
| 2007|    81.235| 80.653| 82.603|      78.623|



Activity #3

  * Compute some measure of life expectancy (mean? median? min? max?) for all possible combinations of continent and year. Reshape that to have one row per year and one variable for each continent. Or the other way around: one row per continent and one variable per year.
    - Use `knitr::kable()` to make these tables look pretty in your rendered homework.
    - Is there a plot that is easier to make with the data in this shape versis the usual form? If so (or you think so), try it! Reflect.

Activity #4

  * In [Window functions](http://stat545.com/block010_dplyr-end-single-table.html#window-functions), we formed a tibble with 24 rows: 2 per year, giving the country with both the lowest and highest life expectancy (in Asia). Take that table (or a similar one for all continents) and reshape it so you have one row per year or per year * continent combination.

Activity #5

  * Previous TA Andrew MacDonald has a nice [data manipulation sampler](https://gist.github.com/aammd/11386424). Make up a similar set of exercises for yourself, in the abstract or (even better) using Gapminder or other data, and solve them.

### Join, merge, look up

__Problem__: You have two data sources and you need info from both in one new data object.

__Solution__: Perform a __join__, which borrows terminology from the database world, specifically SQL.

__Prompts__:

Activity #1

  * Create a second data frame, complementary to Gapminder. Join this with (part of) Gapminder using a `dplyr` join function and make some observations about the process and result. Explore the different types of joins. Examples of a second data frame you could build:
    - One row per country, a country variable and one or more variables with extra info, such as language spoken, NATO membership, national animal, or capitol city. If you really want to be helpful, you could attempt to make a pull request to resolve [this issue](https://github.com/jennybc/gapminder/issues/13), where I would like to bring ISO country codes into the gapminder package.
    - One row per continent, a continent variable and one or more variables with extra info, such as northern versus southern hemisphere.

Activity #2

  * Create your own cheatsheet patterned [after mine](bit001_dplyr-cheatsheet.html) but focused on something you care about more than comics! Inspirational examples:
    - Pets I have owned + breed + friendly vs. unfriendly + ??. Join to a table of pet breed, including variables for furry vs not furry, mammal true or false, etc.
    - Movies and studios....
    - Athletes and teams....

You will likely need to iterate between your data prep and your joining to make your explorations comprehensive and interesting. For example, you will want a specific amount (or lack) of overlap between the two data.frames, in order to demonstrate all the different joins. You will want both the data frames to be as small as possible, while still retaining the expository value.

Activity #3

  * This is really an optional add-on to either of the previous activities.
  * Explore the base function `merge()`, which also does joins. Compare and contrast with dplyr joins.
  * Explore the base function `match()`, which is related to joins and merges, but is really more of a "table lookup". Compare and contrast with a true join/merge.
  
