[tips-code]: https://github.com/jcblum/community-faqs/blob/master/code-formatting_6246.md
[reprex]: reprex.md
[newbie]: reprex_newbie.md
[package]: reprex_package.md
[install]: reprex_install-packages.md
[shiny-cloud]: reprex_shiny_cloud.md
[data]: reprexdata_advanced.md
[dput]: reprexdata_dput.md
[datapasta]: reprexdata_datapasta.md
[readr]: reprexdata_readr.md
[remote]: reprexdata_remote.md

# How to get data into your reproducible example

Questions discussed here often involve working with data. How do you include data in a self-contained, reproducible example?

- [Try this first: _Don't_ use your own data](#heading--tryfirst)
	- [Use a built-in data set](#heading--builtin)
	- [Generate a small example data set](#heading--generate)
- [Use your own data](#heading--owndata)
	- [`dput()` method](#heading--dput)
	- [`datapasta` method](#heading-datapasta)
	- [`read_tsv()` method](#heading--readtsv)
	- [Post your data online](#heading--online)
	- [Other options](#heading--other)
	
<h2 id="heading--tryfirst">Try this first: <em>Don't</em> use your own data</h2>

It's natural to start out trying to make a reprex using the data you are already working with, but many questions don't actually depend on the details of your particular data. Your reprex will often be simpler and easier for others to understand if you _don't_ use your own data at all.

See if you can make one of these options work, first! :grinning:

<h3 id="heading--builtin">Use a built-in data set</h3>

R and its core packages come with lots of data sets already built in! Other packages often include even more built-in data sets. These data sets have usually been specifically chosen to make it easy to show how things work.

You can see a list of all the built-in data available to you by running `data()` at the console. To see data sets included with packages, make sure those packages have been loaded with `library()`, first.

To learn about any of the datasets in the list, try using the help function, `?`. For example, typing `?iris` at the console will bring up the help file for the built-in `iris` data set. It can also be helpful to look at the structure of the data set using `str()`.

It can take a little thinking to reimagine your problem in terms of a built-in data set. Try following these steps:

1. Look at the structure of your data using `str()`. What type of data is in each column?

   Remember, your question might not involve all the columns in your data frame. Focus on just the ones you were actually using in the code you are asking about.

2. Find a built-in data set that has columns with the same types as your data. The quickest way to check is by running `str()` on the built-in data set. Or try one of these popular built-in data sets:
   - [`iris`](https://rdrr.io/r/datasets/iris.html): four numeric response variables, one categorical grouping variable
   - [`warpbreaks`](https://rdrr.io/r/datasets/warpbreaks.html): one numeric response, two  categorical grouping variables
   - [`mtcars`](https://rdrr.io/r/datasets/mtcars.html): eleven numeric variables (some can be treated as categorical grouping variables)
   - [`cars`](https://rdrr.io/r/datasets/cars.html): two numeric variables; appropriate for a simple `y ~ x` correlation
   - [`quakes`](https://rdrr.io/r/datasets/quakes.html): locations (given by latitude and longitude), and three associated numeric variables

   Bigger data sets: If there's something about your problem that specifically requires using a larger data set, here are two "medium data" options:
   - [`ggplot2::diamonds`](https://ggplot2.tidyverse.org/reference/diamonds.html): 50,000 observations (rows), with numeric and [ordinal](https://stats.idre.ucla.edu/other/mult-pkg/whatstat/what-is-the-difference-between-categorical-ordinal-and-interval-variables/) variables
   - [`nycflights13::flights`](https://cran.r-project.org/package=nycflights13): 336,776 observations (rows), with numeric, character, and date-time variables

3. Compose your reprex using the built-in data set. Replace references to your own data frame with the name of the built-in data set, and make sure to use the built-in data set's column names instead of the ones from your own data.

<h3 id="heading--generate">Generate a small example data set</h3>

R makes it pretty easy to construct small data frames by hand. Here are some tips on how to do it:

#### Useful data generating functions

- [`letters` and `LETTERS`](https://rdrr.io/r/base/Constants.html) are built-in vectors containing the 26 lowercase and uppercase letters of the [Latin alphabet](https://en.wikipedia.org/wiki/ISO_basic_Latin_alphabet).
- [`month.name` and `month.abb`](https://rdrr.io/r/base/Constants.html) are built-in vectors containing the English names of the months of the year, and their respective three-letter abbreviations
- [`rep()`](https://rdrr.io/r/base/rep.html) repeats a value (or a vector of values) a specified number of times
- [`seq()` and `seq.int()`](https://rdrr.io/r/base/seq.html) produce sequences of numbers
- [`seq.Date()`](https://rdrr.io/r/base/seq.Date.html) and [`seq.POSIXt()`](https://rdrr.io/r/base/seq.POSIXt.html) produce sequences of dates and datetimes
- [`sample()` and `sample.int()`](https://rdrr.io/r/base/sample.html) can generate random samples and permutations from a vector
- [`rnorm()`](https://rdrr.io/r/stats/Normal.html) draws random variates from a normal distribution; [`runif()`](https://rdrr.io/r/stats/Uniform.html) does the same for a uniform distribution
   - There are [many other distributions](https://rdrr.io/r/stats/Distributions.html) available! Run `?Distributions` at the console to see them all!
   - If you're using one of the [`rxxx()`](https://rdrr.io/r/stats/Distributions.html) functions to draw random variates, remember to make your example reproducible by first calling [`set.seed()`](https://rdrr.io/r/base/Random.html).
- [`expand.grid()`](https://rdrr.io/r/base/expand.grid.html) generates a data frame with all the possible combinations of a set of variables, which can save quite a bit of typing.

#### Making a sample data set using `data.frame()`

If you don’t mind typing, you can stick to basics and make your data frame like this:

``` r
(very_basic <- data.frame(
  group = c("A", "A", "B", "B", "C", "C"),
  var_integer = c(1L, 2L, 1L, 3L, 2L, 2L),
  var_numeric = c(4.3, 3.1, 4.5, 2.8, 6.4, 5.3)
))
#>   group var_integer var_numeric
#> 1     A           1         4.3
#> 2     A           2         3.1
#> 3     B           1         4.5
#> 4     B           3         2.8
#> 5     C           2         6.4
#> 6     C           2         5.3

str(very_basic)
#> 'data.frame':    6 obs. of  3 variables:
#>  $ group      : Factor w/ 3 levels "A","B","C": 1 1 2 2 3 3
#>  $ var_integer: int  1 2 1 3 2 2
#>  $ var_numeric: num  4.3 3.1 4.5 2.8 6.4 5.3
```

> :information_source: Did you notice the extra parentheses around the `name <- data.frame(...)` assignment statement? This makes R automatically print the resulting object. It's a nice trick to use when making reprexes, since it lets you and your audience quickly check that the data frame came out the way you expect!
 
R can also help you come up with your example values. This is especially useful if the data are supposed to follow a particular pattern or structure.

``` r
set.seed(1)

(fancier <- data.frame(
  group = rep(LETTERS[1:3], each = 2),
  var_integer = sample.int(3, size = 6, replace = TRUE),
  var_numeric = rnorm(6, mean = 5, sd = 1)
))
#>   group var_integer var_numeric
#> 1     A           1    5.414641
#> 2     A           3    3.460050
#> 3     B           1    4.071433
#> 4     B           2    4.705280
#> 5     C           1    4.994233
#> 6     C           3    7.404653

str(fancier)
#> 'data.frame':    6 obs. of  3 variables:
#>  $ group      : Factor w/ 3 levels "A","B","C": 1 1 2 2 3 3
#>  $ var_integer: int  1 3 1 2 1 3
#>  $ var_numeric: num  5.41 3.46 4.07 4.71 4.99 ...
```

<sup>Created on 2019-12-24 by the [reprex package](https://reprex.tidyverse.org) (v0.3.0)</sup>

And here’s one way you might generate sequences of dates or date-times:

``` r
(date_sequence <- data.frame(
  date = seq.Date(
    from = as.Date("2018-01-15"),
    to = as.Date("2018-06-30"),
    by = "month"
  ),
  measurement = c(4.3, 3.1, 4.5, 2.8, 6.4, 5.3)
))
#>         date measurement
#> 1 2018-01-15         4.3
#> 2 2018-02-15         3.1
#> 3 2018-03-15         4.5
#> 4 2018-04-15         2.8
#> 5 2018-05-15         6.4
#> 6 2018-06-15         5.3

str(date_sequence)
#> 'data.frame':    6 obs. of  2 variables:
#>  $ date       : Date, format: "2018-01-15" "2018-02-15" ...
#>  $ measurement: num  4.3 3.1 4.5 2.8 6.4 5.3

(datetime_sequence <- data.frame(
  date_time = seq.POSIXt(
    from = ISOdatetime(2018, 6, 22, 14, 00, 00, tz = "UTC"),
    by = 30,
    length.out = 6
  ),
  measurement = c(4.3, 3.1, 4.5, 2.8, 6.4, 5.3)
))
#>             date_time measurement
#> 1 2018-06-22 14:00:00         4.3
#> 2 2018-06-22 14:00:30         3.1
#> 3 2018-06-22 14:01:00         4.5
#> 4 2018-06-22 14:01:30         2.8
#> 5 2018-06-22 14:02:00         6.4
#> 6 2018-06-22 14:02:30         5.3

str(datetime_sequence)
#> 'data.frame':    6 obs. of  2 variables:
#>  $ date_time  : POSIXct, format: "2018-06-22 14:00:00" "2018-06-22 14:00:30" ...
#>  $ measurement: num  4.3 3.1 4.5 2.8 6.4 5.3
```

<sup>Created on 2019-12-24 by the [reprex package](https://reprex.tidyverse.org) (v0.3.0)</sup>


The `expand.grid()` function can save a lot of typing (and mistakes) if you need to generate data with a factorial structure.

``` r
oyster_growth <- data.frame(
  expand.grid(
    list(temp_C = c(15, 20, 25),
         salinity = c(20, 30),
         diet = c("low", "high"))
  ),
  growth_mm = c(
    rnorm(6, mean = 3, sd = 1), # low diet
    rnorm(6, mean = 5, sd = 2)  # high diet
  )
)

oyster_growth
#>    temp_C salinity diet growth_mm
#> 1      15       20  low 1.6409840
#> 2      20       20  low 3.6903998
#> 3      25       20  low 1.2429809
#> 4      15       30  low 2.9477181
#> 5      20       30  low 3.0538102
#> 6      25       30  low 2.2948256
#> 7      15       20 high 5.3081953
#> 8      20       20 high 5.3486715
#> 9      25       20 high 7.3352834
#> 10     15       30 high 0.7476454
#> 11     20       30 high 4.9605814
#> 12     25       30 high 6.8629113

str(oyster_growth)
#> 'data.frame':    12 obs. of  4 variables:
#>  $ temp_C   : num  15 20 25 15 20 25 15 20 25 15 ...
#>  $ salinity : num  20 20 20 30 30 30 20 20 20 30 ...
#>  $ diet     : Factor w/ 2 levels "low","high": 1 1 1 1 1 1 2 2 2 2 ...
#>  $ growth_mm: num  1.64 3.69 1.24 2.95 3.05 ...
```

<sup>Created on 2019-12-24 by the [reprex package](https://reprex.tidyverse.org) (v0.3.0)</sup>

#### Making a sample data set using `tibble::tribble()`

The [`tidyverse`](https://www.tidyverse.org/) package [`tibble`](https://tibble.tidyverse.org/) has a function called [`tribble()`](https://tibble.tidyverse.org/reference/tribble.html) designed especially for typing in a small data set by hand:

``` r
library(tibble)

sea_stars <- tribble(
  ~common_name,         ~n_arms,  ~observed,                ~is_ophiuroid,
  "Six Rayed Star",      6,        as.Date("2019-06-25"),    FALSE,
  "Bat Star",            5,        as.Date("2019-10-04"),    FALSE,
  "Bat Star",            6,        as.Date("2019-10-09"),    FALSE,
  "Ochre Star",          5,        as.Date("2019-10-05"),    FALSE,
  "Morning Sun Star",   13,        as.Date("2019-03-26"),    FALSE,
  "Daisy Brittle Star",  5,        as.Date("2019-09-29"),    TRUE
)

sea_stars
#> # A tibble: 6 x 4
#>   common_name        n_arms observed   is_ophiuroid
#>   <chr>               <dbl> <date>     <lgl>       
#> 1 Six Rayed Star          6 2019-06-25 FALSE       
#> 2 Bat Star                5 2019-10-04 FALSE       
#> 3 Bat Star                6 2019-10-09 FALSE       
#> 4 Ochre Star              5 2019-10-05 FALSE       
#> 5 Morning Sun Star       13 2019-03-26 FALSE       
#> 6 Daisy Brittle Star      5 2019-09-29 TRUE
```

<sup>Created on 2019-12-24 by the [reprex package](https://reprex.tidyverse.org) (v0.3.0)</sup>

<h2 id="heading--owndata">Use your own data</h2>

<h3 id="heading--dput"><a href="reprexdata_dput.md"><code>dput()</code> Method</a></h3>

#### Pros & Cons

:heavy_plus_sign: Built in to R, does not require installing any packages  
:heavy_plus_sign: Handles many different column types

:heavy_minus_sign: Output is not very readable, may get formatted sub-optimally by RStudio
:heavy_minus_sign: Requires tweaking to use with `data.table` objects

<h3 id="heading--datapasta"><a href="reprexdata_datapasta.md"><code>datapasta</code> Method</a></h3>

#### Pros & Cons

:heavy_plus_sign: Excellent if you have data in a spreadsheet or an existing data frame  
:heavy_plus_sign: Very readable output

:heavy_minus_sign: Requires installing a package  
:heavy_minus_sign: Only works when using the RStudio Desktop IDE (won't work on RStudio Server, RStudio Cloud, or in other editors)  
:heavy_minus_sign: Handles a limited variety of common column types  

<h3 id="heading--readtsv"><a href="reprexdata_readr.md"><code>read_tsv()</code> Method</a></h3>

#### Pros & Cons

:heavy_plus_sign: Works in situations where `datapasta` fails (e.g., RStudio Server and RStudio Cloud)  
:heavy_plus_sign: If you already have `tidyverse` installed, then you're set

:heavy_minus_sign: Handles a limited variety of common column types  
:heavy_minus_sign: Only handles cases where data is already in a spreadsheet

<h3 id="heading--online"><a href="reprexdata_remote.md">Post your data online</a></h3>

#### Pros & Cons

:heavy_plus_sign: Allows you to demonstrate problems that depend on specific, non-tiny data sets

:heavy_minus_sign: Your example will no longer be purely self-contained  
:heavy_minus_sign: Helpers may be wary of running code that downloads files from the internet

<h3 id="heading--other">Other options</h3>

- People here suggested several more ways of getting data into a reprex in this discussion: https://community.rstudio.com/t/best-practices-how-to-prepare-your-own-data-for-use-in-a-reprex-if-you-can-t-or-don-t-know-how-to-reproduce-a-problem-with-a-built-in-dataset/5346

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc2NjM2NTg3LC0xNTMwMjA0NTksLTM2OD
M1ODk0MiwtMTg4Mjk3NDA4MCwtMTIwMDk4NjQ4MCwzMTg0NDY5
ODIsLTQyODc0ODI0OV19
-->