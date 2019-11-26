# Data for your reprex

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
	
<h2 id="heading--tryfirst">Try this first: _Don't_ use your own data</h2>

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

:info: Did you notice the extra parentheses around each `name <- data.frame(...)` assignment statement? This makes R automatically print the resulting object. It's a nice trick to use when making reprexes, since it lets you and your audience quickly check that the data frame came out the way you expect!

```
(very_basic <- data.frame(
  group = c("A", "A", "B", "B", "C", "C"),
  var_integer = c(1L, 2L, 1L, 3L, 2L, 2L),
  var_numeric = c(4.3, 3.1, 4.5, 2.8, 6.4, 5.3)
))

str(very_basic)

set.seed(1)

(fancier <- data.frame(
  group = rep(LETTERS[1:3], each = 2),
  var_integer = sample.int(3, size = 6, replace = TRUE),
  var_numeric = rnorm(6, mean = 5, sd = 1)
))

str(fancier)
```

```
# Generate data that includes a sequence of datetimes

```


```
# Using expand.grid()
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

str(oyster_growth)
```

#### Making a sample data set using `tibble::tribble()`

The [`tidyverse`](https://www.tidyverse.org/) package [`tibble`](https://tibble.tidyverse.org/) has a function called [`tribble()`](https://tibble.tidyverse.org/reference/tribble.html) designed especially for typing in a small data set by hand:

```
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
```

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

- Annotated bibliography of other reprex data links
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM2ODM1ODk0MiwtMTg4Mjk3NDA4MCwtMT
IwMDk4NjQ4MCwzMTg0NDY5ODIsLTQyODc0ODI0OV19
-->