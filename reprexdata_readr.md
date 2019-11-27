# Self-contained data with `read_tsv()`

Including data in a self-contained way is a common stumbling block for people who are new to creating reproducible examples. Here's how the [tidyverse](https://www.tidyverse.org/) function [`read_tsv()`](https://readr.tidyverse.org/reference/read_delim.html), from the [`readr`](https://readr.tidyverse.org/) package, can help.

- [Is `read_tsv()` the right choice?](#heading--rightchoice)   
- [How to use `read_tsv()`](#heading--howto)

<h2 id="heading--rightchoice">🛑 Is <code>read_tsv()</code> the right choice?</h2>

If you can answer **YES** to **ALL** of these questions, then carry on! :grinning:

1. My data is **in a spreadsheet** :heavy_check_mark:
2. I can't or don't want to use the [`datapasta` method]()  :heavy_check_mark:
3. My data is **short** (20 rows or fewer) :heavy_check_mark:

:frowning: Answered **no**? All is not lost!

<details>
<summary>Click here for more help</summary>

1. :thinking: My data is somewhere else.
	- Already loaded into R? The [`dput()` method]() might be a better fit.

2. :spaghetti: `datapasta` works fine on my system! 

   If the `datapasta` package works well for you, then you should probably try the [`datapasta` method](). It's a bit less fiddly than using `read_tsv()` and it can handle a wider variety of inputs.

3. :sweat_smile: My data is longer than 20 rows.

   In most cases, your reproducible example doesn't need all of your data. If your data is in a spreadsheet, try copying a small number of rows to a new spreadsheet and starting from there. If your data is on a webpage, try copying it into a spreadsheet first, and cutting it down to just a few rows.
   
   If you _really, truly_ need to include a whole lot of your own data in a reproducible example, then try [hosting your data online]().
   
</details>

<h2 id='heading--howto'>How to use <code>read_tsv()</code></h2>

:warning: The `read_tsv()` maneuvers described here might feel odd and unexpected! It's strongly recommended that you read these instructions all the way through before jumping in, to save yourself from confusion :sweat_smile:.

### What's going to happen

You will **copy** your data from a spreadsheet, hopefully producing a tab-delimited block of text. Its ultimate destination is the script file where you are working on your reproducible example — but the text block needs to be assigned to a variable name! 

So you will first **type** a name, an assignment arrow, and quotation marks into your script file by hand. _Then_ you will **paste** the text block in between the quotation marks next to the assignment arrow.

Finally, you'll add a line to your reproducible example script that uses `read_tsv()` to parse your text block into a data frame. The result will be a few lines of code in your reproducible example script that create a data frame from your data in a completely self-contained way. It will look a bit clunky :sweat_smile:, but people will be delighted because they can now run your code very easily :grinning:.

### Step by step

1. You should be working on your reproducible example in a script file. Check that you are set up correctly to use commands from the `readr` package:
	-  Make sure you have installed either `readr` by itself, or the `tidyverse` collection of R packages with `install.packages("readr")` or `install.packages("tidyverse")`
	- Make sure your reproducible example has either `library(tidyverse)` or `library(readr)` at the top

3. Open your spreadsheet, then **select and copy** the data you want to use in your reproducible example (don't forget the column headers!).

   ![awesome_data_sheet_selected](awesome_data_sheet_selected.png)

4. **Move your cursor to your script file**, placing it on a blank line.

5. **Type** the variable name you want to use for the copied block of text, followed by an assignment arrow (`<-`) and an empty pair of quotation marks (`""`). When you're done, your script file might look like:

   ```
   library(tidyverse)

   awesome_data_text <- ""

   awesome_data %>%
     group_by(super_group) %>%
     summarize(stupendous = max(huge_value, na.rm = TRUE))
   ```

6. **Paste** your copied data _between_ the pair of quotation marks.

   ```
   library(tidyverse)

   awesome_data_text <- "super_group	huge_value
   ace	15708.46
   ace	7924.17
   ace	6896.971
   brill	19911.978
   brill	4483.261
   brill	3472.984
   chic	2802.558
   chic	2193.002
   chic	10893.316"

   awesome_data %>%
     group_by(super_group) %>%
     summarize(stupendous = max(huge_value, na.rm = TRUE))
   ```

7. On a new line, **type** in the variable name you want to use for your data frame in your reproducible example, followed by an assignment arrow (`<-`) and the command `read_tsv()` with the name of your text block variable inside the parentheses.

   ```
   library(tidyverse)

   awesome_data_text <- "super_group	huge_value
   ace	15708.46
   ace	7924.17
   ace	6896.971
   brill	19911.978
   brill	4483.261
   brill	3472.984
   chic	2802.558
   chic	2193.002
   chic	10893.316"

   awesome_data <- read_tsv(awesome_data_text)

   awesome_data %>%
     group_by(super_group) %>%
     summarize(stupendous = max(huge_value, na.rm = TRUE))
   ```

   You're done! :tada:
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAzMTM2Nzc3MCwtODg0NTg1NzAyLDY3OT
Q2MzY1NSwtNjgzMTQ1MDMxLDQwNTA5MTYyMiwxNTc2ODYwMzg1
LC0xNzc4ODA2MTYwLDExMDAyMzc3MjUsLTE5MTYzODQ2ODIsLT
E2MDcxNjM1MzQsLTExNjg5NzA2NDMsMTYyODI2MzY2LDEyOTAx
NTk2MzBdfQ==
-->
