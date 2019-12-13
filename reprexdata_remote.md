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

# Self-contained data with data posted online

Including data in a self-contained way is a common stumbling block for people who are new to creating reproducible examples, especially when demonstrating your problem requires using a specific data set that is too big for [other methods](). As a last resort when other approaches have failed, here's how you can include remote, online data in a reproducible example.

- [Is online data the right choice?](#heading--rightchoice)   
- [How to use online data in a reproducible example](#heading--howto)
- [Tweaks](#heading--tweaks)
  - [Can I post my data somewhere other than GitHub?](#heading--elsewhere)

<h2 id="heading--rightchoice">🛑 Is online data the right choice?</h2>

Including online data in a reproducible example is almost never strictly necessary and goes against the ideal of making your example _self-contained_. Using this method may discourage some helpers from wanting to work with your code. However, it can be a useful thing to try if you can't make anything else work — just be sure you've considered your other options!

If you can answer **YES** to **ALL** of these questions, then carry on! :grinning:

1. I already tried using just a small subset of my data :heavy_check_mark:
2. I already tried using [a data set that's built into R]() :heavy_check_mark:
3. I already tried [generating example data]()  :heavy_check_mark:

:frowning: Answered **no**? All is not lost!

<details>
<summary>Click here for more help</summary>

1. :sweat_smile: I haven't tried using a small subset of my data. How do I do that?

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

2. :sweat_smile: I haven't tried using a built-in data set. How do I do that?

   There are lots of small example data sets that come built into R, and some packages include even bigger data sets. It will save both you and your helpers headaches if you can write your example using one of these data sets instead of using your own data. Check out this [list of recommended built-in data sets]() to get started.

2. :sweat_smile: I haven't tried generating example data. How do I do that?

   With a few lines of code, R can construct all sorts of example data for you, and make it as big or as small as you need. Using example data generated in code is the most purely self-contained method possible, and can prevent your helpers from getting distracted by details of your real data that aren't related to your problem. It's also a good skill to develop if your real data are often too sensitive to share. Check out this [list of recommended data generating functions]() to get started.
   
</details>

<h2 id="heading--howto">How to use online data in a reproducible example</h2>

### What's going to happen

You will start by **exporting** your data in a text-only format (e.g., CSV) and **posting** it online. Since your reproducible example will depend on the link to your online data working, and since people may reasonably be suspicious of code that downloads files from the internet, you'll use a method for posting your data that is transparent and robust.

Once your data is posted online, you will **copy** a link to the online data. The link's ultimate destination is the script file where you are working on your reproducible example — but it needs to be assigned to a variable name! 

So you will first **type** a name, an assignment arrow, and quotation marks into your script file by hand. _Then_ you will **paste** the link in between the quotation marks next to the assignment arrow.

Finally, you'll add a line to your reproducible example script that uses an appropriate data import command to download the data from your link and parse it into a data frame. The result will be a few lines of code in your reproducible example script that create a data frame from your online data. People will be delighted because they can now easily run your code :grinning:.

### Step by step

1. You should be working on your reproducible example in a script file. The data you want to include in your example should have already been exported to a text-only format, such as [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) or [TSV](https://en.wikipedia.org/wiki/Tab-separated_values).
   - Make sure your reproducible example script file is open
   - Locate your exported text-only data file using your computer's file explorer

2. **Post** your exported data to [GitHub](https://www.github.com), either in a repository or as a [Gist](https://help.github.com/en/github/writing-on-github/creating-gists).

   If you've never used GitHub before, then you should post your data as a Gist. Gists are a simple way of posting files or code on GitHub.

   - Sign up for a GitHub account, if you don't already have one
   - After signing in to GitHub, go to https://gist.github.com/
   - Drag your text file onto the large empty box to upload the data
   - Choose either **Create public gist** or **Create secret gist** (either will work for this case)
   
3. **Copy** a link to the **raw** version of your posted data. For a Gist:
   - Click on the <kbd>Raw</kbd> button in the file title bar. The raw data file will load in your browser.
   - Copy the URL from your browser's address bar. It should look something like:
      ```
      https://gist.githubusercontent.com/username/56fb7ecfbd4a6c563e0c87b18a1cbed4/raw/e9ab94c8c31320d1c2fedeaddda21279f875df1e/File_name.csv
      ``` 

4. **Move your cursor to your script file**, placing it on a blank line.

5. **Type** the variable name you want to use for the copied URL, followed by an assignment arrow (`<-`) and an empty pair of quotation marks (`""`). When you're done, your script file might look like:

   ```
   library(tidyverse)

   awesome_data_url <- ""

   awesome_data %>%
     group_by(super_group) %>%
     summarize(stupendous = max(huge_value, na.rm = TRUE))
   ```

6. **Paste** your copied URL _between_ the pair of quotation marks.

   ```
   library(tidyverse)

   awesome_data_url <- "https://gist.githubusercontent.com/username/56fb7ecfbd4a6c563e0c87b18a1cbed4/raw/e9ab94c8c31320d1c2fedeaddda21279f875df1e/awesome_data.csv"

   awesome_data %>%
     group_by(super_group) %>%
     summarize(stupendous = max(huge_value, na.rm = TRUE))
   ```

7. On a new line, **type** in the variable name you want to use for your data frame in your reproducible example, followed by an assignment arrow (`<-`). Then type one of the following commands, including the name of your URL variable inside the parentheses:

   If you already have `library(tidyverse)` in your reproducible example, use:
   - `read_csv(`_URL variable name_`)` for CSV data
   - `read_tsv(`_URL variable name_`)` for TSV data
   
   Otherwise, use:
   - `read.csv(`_URL variable name_`)` for CSV data
   - `read.delim(`_URL variable name_`)` for TSV data

   The result should look something like this:
   ```
   library(tidyverse)

   awesome_data_url <- "https://gist.githubusercontent.com/username/56fb7ecfbd4a6c563e0c87b18a1cbed4/raw/e9ab94c8c31320d1c2fedeaddda21279f875df1e/awesome_data.csv"

   awesome_data <- read_csv(awesome_data_url)
   
   awesome_data %>%
     group_by(super_group) %>%
     summarize(stupendous = max(huge_value, na.rm = TRUE))
   ```
	
   You're done! :tada:

<h2 id="heading--tweaks">Tweaks</h2>

<h3 id='heading--elsewhere'>Can I post my data somewhere other than GitHub?</h3>

- Don't make people download files and move them around! 
- Don't use FTP sites or anonymous paste sites!

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAxMzE2OTM3NSwtMTQyMjc5MjI3Miw1Mj
M0NDYwNzQsNDk4NzE3NDg1LDIwMDM3NzMzODgsLTI4NTYxMTA2
MiwxMDQ2OTA0NTAzLC0xNDE5MzkwMDI5LDE4NjMwOTQ1MDcsLT
ExNTM4ODczMDIsMTg2NzIxNjY5NiwtMTI5ODAxMjYxMSwxNTY3
OTc3MDE4LC04MTU4MTE2OTcsLTI0OTE0MjcxMF19
-->
