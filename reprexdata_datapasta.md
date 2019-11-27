# Self-contained data with `datapasta`

Including data in a self-contained way is a common stumbling block for people who are new to creating reproducible examples. Here's how some clever tools from the [`datapasta`](https://github.com/milesmcbain/datapasta) package can help.

- [Is `datapasta` the right choice?](#heading--rightchoice)   
- [How to use `datapasta`](#heading--howto)
- [Tweaks](#heading--tweaks)
   - [Transform your data into even prettier `tribble` code](#heading--tribble)
   - [Transform your data into `data.table` code](#heading--datatable)
   - [Use a keyboard shortcut](#heading--keyboard)
  
<h2 id="heading--rightchoice">🛑 Is <code>datapasta</code> the right choice?</h2>

If you can answer **YES** to **ALL** of these questions, then you're ready to pasta! :grinning:

1. My data is **in a spreadsheet** :heavy_check_mark:
2. I am using the **RStudio Desktop IDE** :heavy_check_mark:
3. My data is **short** (20 rows or fewer) :heavy_check_mark:

:frowning: Answered **no**? All is not lost!

<details>
<summary>Click here for more help</summary>

1. :thinking: My data is somewhere else.
	- Already loaded into R? The [`dput()` method]() might be a better fit.

2. :disappointed: I'm using [RStudio Server](https://rstudio.com/products/rstudio/#rstudio-server), [RStudio Cloud](https:://rstudio.cloud/), or some other editor! 

   The `datapasta` features this method relies on require RStudio IDE-specific integrations, but unfortunately [will not work in RStudio Server or RStudio Cloud](https://github.com/MilesMcBain/datapasta/issues/73). While a [limited subset](https://github.com/MilesMcBain/datapasta#use-with-other-editors) of `datapasta`'s tools can be used in other editors, that subset does not include the functions needed here.

   If your data are in a spreadsheet and you are working RStudio Server, RStudio Cloud, or some other editor, your best bet is probably the [`read_tsv()` method]().

3. :sweat_smile: My data is longer than 20 rows.

   In most cases, your reproducible example doesn't need all of your data. If your data is in a spreadsheet, try copying a small number of rows to a new spreadsheet and starting from there. If your data is on a webpage, try copying it into a spreadsheet first, and cutting it down to just a few rows.
   
   If you _really, truly_ need to include a whole lot of your own data in a reproducible example, then try [hosting your data online]().
   
</details>

<h2 id='heading--howto'>How to use <code>datapasta</code></h2>

:warning: The `datapasta` maneuvers described here might feel odd and unexpected! It's strongly recommended that you read these instructions all the way through before jumping in, to save yourself from confusion :sweat_smile:.

### What's going to happen

The `datapasta` package's big trick is that it lets you copy some data from a spreadsheet and then invoke a command that causes the copied data to be inserted into your RStudio script file. The magical part is that along the way, `datapasta` **transforms your copied data into a block of code** that creates a data frame filled with that same copied data.

To start, you'll **copy** the data you want to use from a spreadsheet. Its ultimate destination is the script file where you are working on your reproducible example — but the transformed data will need to be assigned to a variable name! So you will first **type** a name and assignment arrow into your script file by hand. _Then_ you will **choose a command from the RStudio Addins menu** to paste in your data, magically transformed into data frame code :sparkles:.

The result will be a few lines of code in your reproducible example script that create a data frame containing your data in a completely self-contained way that is both easy to read and easy to run — reprex perfection! :trophy:

### Step by step

1. You should be working on your reproducible example in a script file. Check that you are set up correctly to use the `datapasta` package:
	- Make sure you have installed  `datapasta` with `install.packages("datapasta")`, and that you see a <span style="font-size:smaller">"DATAPASTA"</span> section somewhere in your RStudio Addins menu.
	- That's it! You are using `datapasta` tools to _edit_ your reproducible example script, but you are not using `datapasta` as part of the script itself, so there is no need to include it in your `library()` statements.

2. Open your spreadsheet, then **select and copy** the data you want to use in your reproducible example (don't forget the column headers!).

   ![awesome_data_sheet_selected](awesome_data_sheet_selected.png)

3. **Move your cursor to your script file**, placing it on a blank line.

4. **Type** the variable name you want to use for this data frame in your reproducible example, and an assignment arrow (`<-`). When you're done, your script file might look like:

   ```
   library(tidyverse)

   awesome_data <- 

   awesome_data %>%
     group_by(super_group) %>%
     summarize(stupendous = max(huge_value, na.rm = TRUE))
   ```

5. **Open the RStudio Addins menu and choose "Paste as data.frame"** (from the `datapasta` section). Your data will appear in your script file, transformed into a lovely block of `data.frame()` code! :woman_mage: 

   ```
   library(tidyverse)

   awesome_data <- data.frame(stringsAsFactors=FALSE,
                   super_group = c("ace", "ace", "ace", "brill", "brill", "brill", "chic",
                                   "chic", "chic"),
                    huge_value = c(15708.46, 7924.17, 6896.971, 19911.978, 4483.261, 3472.984,
                                   2802.558, 2193.002, 10893.316)

   awesome_data %>%
     group_by(super_group) %>%
     summarize(stupendous = max(huge_value, na.rm = TRUE))
   ```

   You're done! :tada:

<h2 id='heading--tweaks'>Tweaks</h2>

 <h3 id='heading--tribble'>Transform your data into even prettier <code>tribble</code> code</h3>

The [`tribble()`](https://tibble.tidyverse.org/reference/tribble.html) command from the tidyverse package `tibble` creates small data frames (technically, [`tbl_df`](https://tibble.tidyverse.org/)s) in an extremely readable way. Using `datapasta`, you can turn your copied data into a block of `tribble()` code by **choosing "Paste as tribble"** from the RStudio Addins menu instead of "Paste as data.frame". 

`datapasta` is smart enough to write `tibble::tribble()`, using the package name and [double colon operator](https://rdrr.io/r/base/ns-dblcolon.html). This means means that your reproducible example technically [doesn't need](https://stackoverflow.com/questions/23232791/is-it-a-good-practice-to-call-functions-in-a-package-via) a `library(tribble)` (or `library(tidyverse)`) statement at the top to make the code work. However, keep in mind that the `tibble::tribble()` code still **will not run** unless you actually have the `tibble` package installed on your system.

For our example above, "Paste as tribble" gives a result like this:
```
awesome_data <- tibble::tribble(
  ~super_group, ~huge_value,
         "ace",    15708.46,
         "ace",     7924.17,
         "ace",    6896.971,
       "brill",   19911.978,
       "brill",    4483.261,
       "brill",    3472.984,
        "chic",    2802.558,
        "chic",    2193.002,
        "chic",   10893.316
  )
```
 Pretty! :nail_care:
 
 <h3 id='heading--datatable'>Transform your data into <code>data.table</code> code</h3>
 
If your reproducible example is slicing and dicing data with the [`data.table`](https://rdatatable.gitlab.io/data.table/) package, it might seem awfully convenient to have `datapasta` transform your copied data directly into a `data.table`. This feature is not yet available in the [CRAN release](https://cran.r-project.org/web/packages/datapasta/index.html) of `datapasta` (as of version 3.0.0), but it _is_ available in the [development version](https://github.com/MilesMcBain/datapasta) of `datapasta` on GitHub.

1. Install the `remotes` package, which provides tools for installing packages from many different locations: 
   `install.packages("remotes")`
   
2. Install the development version of `datapasta` using:
   `remotes::install_github("MilesMcBain/datapasta")`

3. Follow the main `datapasta` instructions, but  **choose "Paste as data.table"** from the RStudio Addins menu instead of "Paste as data.frame"

`datapasta` is smart enough to write `data.table::data.table()`, using the package name and [double colon operator](https://rdrr.io/r/base/ns-dblcolon.html). This means that your reproducible example technically [doesn't need](https://stackoverflow.com/questions/23232791/is-it-a-good-practice-to-call-functions-in-a-package-via) a `library(data.table)` statement at the top to make the data code work. However, keep in mind that the `data.table::data.table()` code still **will not run** unless you actually have the `data.table` package installed on your system. And if you're using `data.table` functions in your reproducible example, you will almost certainly want to have `library(data.table)` at the top anyway!

For our example above, "Paste as data.table" gives a result like this:
```
awesome_data <- data.table::data.table(
  super_group = c("ace","ace","ace","brill","brill",
                  "brill","chic","chic","chic"),
   huge_value = c(15708.46,7924.17,6896.971,19911.978,
                  4483.261,3472.984,2802.558,2193.002,10893.316)
)
```

 <h3 id='heading--keyboard'>Use a keyboard shortcut</h3>

If you're `datapasta`-ing a lot, you might get tired of pointing and clicking on the RStudio Addins menu every time. Luckily, Addins are designed so that you can assign your own keyboard shortcuts to them :grinning:. See here for instructions: 

https://rstudio.github.io/rstudioaddins/#keyboard-shorcuts

As a starting point, the authors of `datapasta` [recommend](https://github.com/MilesMcBain/datapasta#getting-data-into-source) assigning the following shortcuts:

- Paste as data.frame: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>Shift</kbd> + <kbd>d</kbd>
- Paste as tribble: <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>t</kbd>
<!--stackedit_data:
eyJoaXN0b3J5IjpbODQxNDY0Mjc4LDM0NDA4MzU1NCwtOTE0NT
UwNjk4LDE4MzQ1NTgyMSwtMTkyODE0NjI3OCwxMjY5ODE2ODI3
LC0xMTYyNDExODk3LC0xODg2NDA4NTg0LC0zMTkzMjAxNyw4Nz
Y3NDM3NDcsLTIzMzQ2OTMyOCwtMjcxOTQ3MTAwLC0xNjA3MDA1
NDI1XX0=
-->
