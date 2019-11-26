# Self-contained data with `dput`

Including data in a self-contained way is a common stumbling block for people who are new to creating reproducible examples. Here's how the built-in R function `dput()` can help.

- [Is `dput()` the right choice?](#heading--rightchoice)   
- [How to use `dput()`](#heading--howto)   
- [Tweaks](#heading--tweaks)
  - [Why did my `dput()` get indented super deeply when I pasted it?](#heading--unindent)
  - [How can I make `dput()` work on my `data.table`?](#heading--datatable)

<h2 id="heading--rightchoice">🛑 Is <code>dput()</code> the right choice?</h2>

If you can answer **YES** to **ALL** of these questions, then go forth and `dput()`! :grinning:

1. My data is **already loaded into R** :heavy_check_mark:
2. My data is in a data frame or tibble, **NOT** a `data.table` :heavy_check_mark:
3. My data frame or tibble is **short** (20 rows or fewer) :heavy_check_mark:

:frowning: Answered **no**? All is not lost!

<details>
<summary>Click here for more help</summary>

1. :spiral_notepad: My data is in a spreadsheet or text file (such as a CSV).
   - Try the [`datapasta` method]() instead!

2. :thinking: My data is in a `data.table`.
   - You _can_ still use `dput()`, but you'll need to do a few special maneuvers to get things working. See the [instructions below]().

3. :sweat_smile: My data frame or tibble is longer than 20 rows.

   In most cases, your reproducible example doesn't need all of your data. Here's how to cut it down:

   - Use the first (or last) few rows using `head()` or `tail()`:

      ```
      # A long built-in data frame
      nrow(warpbreaks)

      # First 10 rows only
      wb_head <- head(warpbreaks, 10)

      # Last 10 rows only
      wb_tail <- tail(warpbreaks, 10)

      # Results
      wb_head
      wb_tail
      ```
   - Sample a random selection of rows:

      ```
      # Always set.seed() to make your sample reproducible!
      set.seed(1234)

      # Randomly choose 10 rows, base R style
      wb_sample_int <- warpbreaks[sample.int(nrow(warpbreaks), 10), ]

      # `dplyr` has some useful helpers!
      library(dplyr)

      # Randomly choose 10 rows, tidyverse style
      wb_sample_n <- sample_n(warpbreaks, 10)

      # Randomly choose 2 rows from each combination
      # of grouping variables
      wb_sample_groups <- warpbreaks %>%
        group_by(wool, tension) %>%
        sample_n(2)

      # Results
      wb_sample_int
      wb_sample_n
      wb_sample_groups
      ```
   If you _really, truly_ need to include a whole lot of your own data in a reproducible example, then try [hosting your data online]().
</summary>

<h2 id='heading--howto'>How to use <code>dput()</code></h2>

:warning: The `dput()` maneuvers described here might feel odd and unexpected! It's strongly recommended that you read these instructions all the way through before jumping in, to save yourself from confusion :sweat_smile:.

### What's going to happen

You will run `dput()` on a data frame that already exists in your workspace, causing a strange looking block of code to get printed to the console :thinking:. This code is like a **recipe** for recreating your data frame.

You'll **copy** the recipe code from the console. Its ultimate destination is the script file where you are working on your reproducible example — but the recipe needs to be assigned to a variable name! So you will first **type** a name and assignment arrow into your script file by hand. _Then_ you will **paste** the recipe block in next to the assignment arrow.

The result will be a block of code in your reproducible example script that recreates your data frame in a completely self-contained way. It will look awfully ugly :sweat_smile:, but people will be delighted because they can now run your code very easily :grinning:.

### Step by step

1. You should be working on your reproducible example in a script file, and the data frame you want to include in your example should already be loaded in your workspace.
   - Make sure your reproducible example script file is open
   - If you're using the RStudio IDE, verify that the data frame you want to include looks the way you expect in the **Environment** pane. Outside of RStudio, you can check by running `str()` on your data frame at the console.    

2. **Move your cursor to the console**, and enter the `dput()` command, with the name of your data frame inside the parentheses.

   If the data frame you wanted to include in your reproducible example was called `awesome_data`, your console line would look like:

   ```
   > dput(awesome_data)
   ```

   Remember, _don't_ type this in your script file! Type it next to the console prompt, and hit <kbd>Return</kbd> (or <kbd>Enter</kbd>) to run the code.

3. A strange looking blob of code will appear in the console! :sparkles: :robot: This is your data frame recipe :woman_cook:.

4. **Copy** the entire strange looking blob of code from the console. **Do not** copy the line where you typed `dput(`_your data frame_`)`!

5. **Move your cursor to your script file**, placing it on a blank line.

6. **Type** the variable name you want to use for this data frame in your reproducible example, and an assignment arrow (`<-`).

   You can absolutely keep the same name from the data frame that you used to create the recipe! When you're done, your script file might look like:

   ```
   library(tidyverse)

   awesome_data <-

   awesome_data %>%
     group_by(super_group) %>%
     summarize(stupendous = max(huge_value, na.rm = TRUE))
   ```
7. **Paste** your data frame recipe next to the assignment arrow.

   ```
   library(tidyverse)

   awesome_data <- structure(list(super_group = structure(c(1L, 1L, 1L, 2L, 2L,
   2L, 3L, 3L, 3L), .Label = c("ace", "brill", "chic"), class = "factor"),
    huge_value = c(15708.4598764777, 7924.16975880042, 6896.97058452293,
    19911.9784161448, 4483.26090117916, 3472.98388415948, 2802.55834804848,
    2193.0019413121, 10893.3162470348)), class = "data.frame", row.names = c(NA,
    -9L))

   awesome_data %>%
     group_by(super_group) %>%
     summarize(stupendous = max(huge_value, na.rm = TRUE))
   ```

   You're done! :tada:

<h2 id='heading--tweaks'>Tweaks</h2>

<h3 id='heading--unindent'>Why did my <code>dput()</code> get indented super deeply when I pasted it?</h3>

If you're using the RStudio IDE, then you may have the **Auto-indent code after paste** option turned on. This causes `dput()` code recipes to become extremely wide (and even uglier than usual) as soon as you paste them into your script file.

![wide_dput_screenshot]()

You can turn the auto-indent option off (Tools > Global Options… > Code > Editing). But perhaps you like this feature in general and just want a quick fix for your pasted `dput()` recipes? If so, try this:

1. Select the entire pasted  `dput()` recipe, including the variable name and assignment arrow.
2. From the **Code** menu, choose:
   - **Comment/Uncomment Lines**, then…
   - **Reflow Comment**, then…
   - **Comment/Uncomment Lines** one more time

![reflow_comment_trick_gif]()

Ahhh, much better! :relieved: And of course, all of those commands have [keyboard shortcuts](https://support.rstudio.com/hc/en-us/articles/200711853-Keyboard-Shortcuts), which is even speedier.

<h3 id='heading--datatable'>How can I make <code>dput()</code> work on my <code>data.table</code>?</h3>

One of the `data.table` package's benefits is that its `data.table` objects can be [modified "in place"](https://rdatatable.gitlab.io/data.table/articles/datatable-reference-semantics.html), whereas in many cases regular R data frames must be copied internally when they are modified. As part of making this work, each `data.table` is given a [special attribute called `.internal.selfref`](https://stackoverflow.com/questions/20687235/#20688045). Unfortunately, this attribute [does not play nicely](https://stackoverflow.com/questions/25533332/) with `dput()`.

If you run `dput()` on a `data.table`, you'll see the `.internal.selfref` attribute appear near the end of the resulting output:

```
> library(data.table)
> dt <- data.table(x = c("b", "a", "c"), y = c(1, 3, 6))
> dput(dt)
structure(list(x = c("b", "a", "c"), y = c(1, 3, 6)), row.names = c(NA,
-3L), class = c("data.table", "data.frame"), .internal.selfref = <pointer: 0x5559123d3de0>)
```

If you try to actually use that `dput()` recipe in a script, you'll get an error because the angle brackets in `<pointer: 0x5559123d3de0>` are not valid R syntax.

```
> dt <- structure(list(x = c("b", "a", "c"), y = c(1, 3, 6)),
+       row.names = c(NA, -3L), class = c("data.table", "data.frame"),
+       .internal.selfref = <pointer: 0x5559123d3de0>)
Error: unexpected '<' in:
"      row.names = c(NA, -3L), class = c("data.table", "data.frame"),
      .internal.selfref = <"
```

In fact, you won't even be able to use the [`reprex`](https://reprex.tidyverse.org/) package on a reproducible example containing such a `dput()` recipe! `reprex` rendering will fail with an error like:

```
Rendering reprex...
Error: callr subprocess failed: <text>:20:27: unexpected '<'
19:       row.names = c(NA, -3L), class = c("data.table", "data.frame"),
20:       .internal.selfref = <
                              ^
```

:worried: How can this be fixed?

#### Option 1: edit the `dput()` recipe by hand

1. Paste your `data.table` `dput()` recipe into your reproducible example script file.

2. Locate the `.internal.selfref` attribute near the end of the block of recipe code. It will look something like:

   `.internal.selfref = <pointer: 0x5559123d3de0>`

3. Delete **just** that part of the recipe code _and_ the comma immediately before it.

   **Before:** After pasting in a `dput()` recipe, your reproducible example script might look like this…

   ```
   library(data.table)

   dt <- structure(list(x = c("b", "a", "c"), y = c(1, 3, 6)),
         row.names = c(NA, -3L), class = c("data.table", "data.frame"),
         .internal.selfref = <pointer: 0x5559123d3de0>)

   dt[, z:=4L]

   dt
   ```

   **After**: Deleting `.internal.selfref` (and its preceding comma!) leaves you with…

   ```
   library(data.table)

   dt <- structure(list(x = c("b", "a", "c"), y = c(1, 3, 6)),
         row.names = c(NA, -3L), class = c("data.table", "data.frame"))

   dt[, z:=4L]

   dt
   ```

#### Option 2: strip `.internal.selfref` before you run `dput()`

1. _Before_ running `dput()` on your `data.table`, remove the `.internal.selfref` attribute using `setattr()`.

   For a `data.table` named `dt`, you would run this line **at the console** (not in your script!):

   `> setattr(dt, ".internal.selfref", NULL)`

2. Continue as usual, running `dput(`_your data.table_`)` at the console and pasting the result into your reproducible example script.

#### Finish Up

Whichever option you chose, you will now have a `dput()` recipe that runs in R. However, it's not quite a proper `data.table` object anymore because it's missing `.internal.selfref`. To fix that, you'll need to include a line in your reproducible example script that runs `data.table::setDT()` on the pseudo-`data.table` that was created by your `dput()` recipe.

**Example:**

Having followed one of the options above, you're left with this reproducible example script:

```
library(data.table)

dt <- structure(list(x = c("b", "a", "c"), y = c(1, 3, 6)),
      row.names = c(NA, -3L), class = c("data.table", "data.frame"))

dt[, z:=4L]

dt
```

If you try running this code, you'll notice a detailed warning from `data.table` complaining about how `dt` is malformed:

``` r
library(data.table)

dt <- structure(list(x = c("b", "a", "c"), y = c(1, 3, 6)),
      row.names = c(NA, -3L), class = c("data.table", "data.frame"))

dt[, z:=4L]
#> Warning in `[.data.table`(dt, , `:=`(z, 4L)): Invalid .internal.selfref
#> detected and fixed by taking a (shallow) copy of the data.table so
#> that := can add this new column by reference. At an earlier point, this
#> data.table has been copied by R (or was created manually using structure()
#> or similar). Avoid names<- and attr<- which in R currently (and oddly)
#> may copy the whole data.table. Use set* syntax instead to avoid copying: ?
#> set, ?setnames and ?setattr. If this message doesn't help, please report
#> your use case to the data.table issue tracker so the root cause can be
#> fixed or this message improved.

dt
#>    x y z
#> 1: b 1 4
#> 2: a 3 4
#> 3: c 6 4
```
<sup>Created on 2019-10-17 by the [reprex package](https://reprex.tidyverse.org) (v0.3.0)</sup>

To correct the problem, we'll do as the warning suggests and add a `setDT()` call to the reproducible example code:

```
library(data.table)

dt <- setDT(
  structure(list(x = c("b", "a", "c"), y = c(1, 3, 6)),
  row.names = c(NA, -3L), class = c("data.table", "data.frame"))
)

dt[, z:=4L]

dt
```

Much better! :tada:

``` r
library(data.table)

dt <- setDT(
  structure(list(x = c("b", "a", "c"), y = c(1, 3, 6)),
  row.names = c(NA, -3L), class = c("data.table", "data.frame"))
)

dt[, z:=4L]

dt
#>    x y z
#> 1: b 1 4
#> 2: a 3 4
#> 3: c 6 4
```
<sup>Created on 2019-10-17 by the [reprex package](https://reprex.tidyverse.org) (v0.3.0)</sup>
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MjU4NzkwMDQsLTExNzEwMzk2MDYsMT
czODEwNjg4LDE5MzMxNDUyMzcsODk2OTQxMTc3XX0=
-->