# Newbie

The gold standard for communicating about code problems is to compose a **small, self-contained reproducible example**. A reproducible example is a chunk of code that will run on anybody's computer and demonstrates the problem you are having. When you're asking a code question here, people will expect you to at least _try_ to create a reproducible example to go with it.

A reproducible example needs to be both *easy to read* and *easy to run*. This means your reproducible example should be:

- **Complete**: it can be copied and pasted in a single action and it will run as-is, with no modifications
- **Self-contained**: it does not make references to anything that won't exist on somebody else's computer (e.g., locations on a hard drive or R objects that were created outside of the reproducible example code)
- **As small as possible**: it is focused on demonstrating a single problem, without distractions from unrelated bits of code
- **Well-formatted**: it uses proper code formatting and a consistent, readable style

Composing good reproducible examples is a skill that takes time and practice to learn, but it is worth the effort. Honing this skill makes you better at thinking about code, and makes it much more likely that you will find the help you need quickly.

### I have no idea what I'm doing, and now people are demanding a reprex. Can't anybody just help?

When you're just starting out, being asked to make a reproducible example might feel daunting. That's understandable! But people here aren't trying to put obstacles in front of you by asking for a reproducible example. Debugging code problems when you can't see and interact with the code yourself is challenging, and helpers truly need the specific information that a reproducible example provides. Without one, many questions are simply impossible for anyone here to answer.

So give it a try and do your best. A question with an imperfect reproducible example is almost always a better starting point for discussion than a question without one, and people here are happy to help you learn how to make your reprex better :grinning:.

## Overview

1. Compose your reproducible example
   - Make sure it's complete
   - Make sure it's self-contained
   - Try to make it smaller
2. Check your work and prepare for posting using the `reprex` package

## Step by step

0. Install the `reprex` package
1. Install the `datapasta` package (Optional)

### Make it complete

1. Make a new script file to hold your reproducible example.
2. Copy the code that's giving you trouble into your reproducible example script.
3. Did you include all your `library()` statements? If not, go copy those over as well.

### Make it self-contained

(Relying on R objects created outside the reprex: link to https://rstats.wtf/save-source.html)

Are you trying to use data? Here are some things that **will not work**:

- (reference to data with a local path)
- (screenshot of a spreadsheet)
- (reference to an object that isn't created by the code)

#### My data is already loaded in R!

If you want to use a data frame from your R workspace in your reproducible example, then you should first try [**the `dput()` method**]() for generating self-contained data.

#### My data is in a spreadsheet!

If the data you want to use in your reproducible example are currently living in a spreadsheet, then you should first try [**the `datapasta` method**]() for generating self-contained data.

:stop_sign: This is _not_ a good way to load data into R for general use! If your problem is figuring out how to load your data, check out the [RStudio Data Import Wizard](https://support.rstudio.com/hc/en-us/articles/218611977-Importing-Data-with-RStudio)
 and this helpful [Data Import Cheatsheet](https://resources.rstudio.com/rstudio-developed/data-import).

### Make it smaller

- Does the code in your reproducible example script actually use all the packages you're loading at the top?
- Is all of the code in your reproducible example script related to your problem? (test by commenting out?)
- Can you show your problem with less data? Do you even need to use your own data?

### Use the `reprex` package to check your work and format it for sharing

[`reprex`](https://reprex.tidyverse.org/) is a tidyverse package that contains tools for preparing reproducible examples to be posted on sites like this one. Using it has two major benefits:

- It automatically **formats** both **your code _and the code's output_** in a way that is easy to read when posted here, and also easy for your helpers to copy, paste, and run themselves.
- It helps you **verify** that your reproducible example really is **complete and self-contained** by running the code in a separate, self-contained R session while generating the formatted output.

You don't *have* to use `reprex` to prepare your reproducible examples, but we **strongly recommend** that you try to do so. There is one major exception to this recommendation: you can't use `reprex` to prepare Shiny reproducible examples. [LINK TO GUIDANCE ON HOW TO MAKE SHINY REPREXES]()

(simplest possible instructions for running `reprex` on the reproducible example script)
(don't forget to *examine the output*: `reprex` keeps you honest!

### Fallback

- Complete code
- `str()` on your data frame
- Format correctly (link)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzYxOTI3MjA1LDEwMjM4MDAzMTYsLTE3Nz
A5NTMyMjQsODE4NTA3ODczLC02NDA1MTU0OThdfQ==
-->