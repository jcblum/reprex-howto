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

# Beginner's guide to making a reproducible example

- [What's a reproducible example and why does it matter?](#heading--background)
  - :thinking: [Reprex? `reprex`?](#heading--jargon)
  - :confounded: [I have no idea what I'm doing, and now people are demanding a "reprex". Can't anybody just help?](#heading--why)

- [How to make a reproducible example](#heading--howto)
  1. [Compose your reproducible example](#heading--compose)
     - [Make it complete](#heading--complete)
     - [Make it self-contained](#heading--self-contained)
     - [Try to make it smaller](#heading--smaller)

  2. [Use the `reprex` package to check your work and format it for sharing](#heading--reprex-pkg)

- :fire::fire_engine: [Reprex disaster? A last resort fallback](#heading--fallback)

---

<h2 id="heading--background">What's a reproducible example and why does it matter?</h2>

The gold standard for communicating about code problems is to compose a **small, self-contained reproducible example**. A reproducible example is a chunk of code that will run on anybody's computer and demonstrates the problem you are having. When you're asking a code question here, people will expect you to try to create a reproducible example to go with it.

A reproducible example needs to be both *easy to read* and *easy to run*. This means your reproducible example should be:

- **Complete**: it can be copied and pasted in a single action and it will run as-is, with no modifications
- **Self-contained**: it does not make references to anything that won't exist on somebody else's computer (e.g., locations of files on your computer or R objects that were created outside of the reproducible example code)
- **As small as possible**: it is focused on demonstrating a single problem, without distractions from unrelated bits of code
- **Well-formatted**: it uses proper code formatting and a consistent, readable style

Composing good reproducible examples is a skill that takes time and practice to learn. But honing this skill makes you better at thinking about code, and makes it much more likely that you will find the help you need quickly.

<h3 id="heading-jargon">🤔 Reprex? <code>reprex</code>?</h3>

In the R community, "reprex" has become a popular shorthand for "**repr**oducible **ex**ample" (credit for this portmanteau goes to [Romain François](https://twitter.com/romain_francois/status/530011023743655936)). Other programming communities use different terms, but the reproducible example concept is widely shared and appreciated. On [Stack Overflow](https://stackoverflow.com/), the preferred jargon for years was ["Minimal, Complete, and Verifiable Example" (MCVE)](https://stackoverflow.com/help/minimal-reproducible-example), so you may encounter people using that term, too.

[`reprex`](https://reprex.tidyverse.org) is also the name of a [tidyverse](https://www.tidyverse.org) package that helps you prepare reproducible examples to be shared with others. This overlapping terminology can occasionally be confusing! To some people, "make a reprex" simply means "compose a reproducible example", while to others it can mean "compose a reproducible example _and then process it using the `reprex` package_".

<h3 id="heading--why">😖 I have no idea what I'm doing, and now people are demanding a "reprex". Can't anybody just help?</h3>

When you're just starting out, being asked to make a reproducible example might feel daunting. That's understandable! So please know that people here aren't trying to put obstacles in front of you by asking for a reproducible example. Debugging code problems when you can't see and interact with the code yourself is difficult even for experts, and helpers truly need the specific information that a reproducible example provides. Without one, many questions are simply impossible for anyone here to answer.

So give it a try and do your best. A question with an imperfect reproducible example is almost always a better starting point for discussion than a question without one, and people here are happy to help you learn how to make your reprex better :grinning:.

<h2 id="heading--howto">How to make a reproducible example</h2>

The process described here is meant to be a starting point, and certainly is not the only way to go about composing a reproducible example. As you gain more experience, you will hopefully find yourself developing your own variations on these steps.

### What's going to happen

You'll compose your reproducible example in stages, first focusing on making it **complete**, then on making it **self-contained**, and finally on making it **as small as possible**. 

Once you've got a solid draft, you'll use the `reprex` package to check your work and format the reproducible example in a way that will make it both *easy to read* and *easy to run* for your helpers.

<h3 id="heading--compose">Step 1: Compose your reproducible example</h3>

#### Before you begin

Your goal in making a reproducible example is to demonstrate a problem you're having. So you'll need to start with an idea of what your example is trying to show people. Here are some common things people use reproducible examples to demonstrate:

- Your code is producing an error message
- Your code does not give you the result you expected
- You figured out one way to do something, but you want to know if there's a better way

In these cases, your reproducible example code should focus on showing people a clear example of what you're seeing. If your problem is an error message, then the reproducible example should produce that same error message! 

But there is one more case where a reproducible example is helpful, but a bit trickier to think about:

- You know what you want to do, but you don't know the way to do it with code

In this case, the goal of your reproducible example should be to include any necessary setup steps to get others right up to the place where you got stumped. It's also helpful if it can show any solutions you tried, even if those attempts didn't work.

Once you've decided on what you want to demonstrate with your reproducible example, then you're ready to start writing it! 😀

#### Make it complete

For your first pass at composing your reproducible example, focus on making it **complete**: that is, including **all** of the code necessary to demonstrate your problem.

1. Make a new script file to hold your reproducible example.
2. Copy all the code you think you need to reconstruct your problem into your reproducible example script.
   - The trickiest part is often figuring out how much setup you need to include, or where the problem starts. It's OK to err on the side of copying too much right now — we'll work on streamlining your example later. 
   - Did you remember to include all your `library()` statements? If not, go copy those over as well! :books:
3. Restart R (in the RStudio IDE, go to the **Session** menu and choose **Restart R**).
   - :fearful:Are you afraid to restart R because you'll lose important stuff? Stop right now and read [Chapter 1 of _What They Forgot to Teach You About R_](https://rstats.wtf/save-source.html).
4. Run the code in your reproducible example script.
   - You might get unexpected error messages, because you forgot to copy over something important :sweat_smile:. If so, add what you think is missing, then restart R and try running the reproducible example script again.
   - You're done when the script shows exactly what you had in mind, and runs without any *extra* error messages (error messages that you're trying to demonstrate are fine!). :relieved:

#### Make it self-contained

The next step is to make sure your reproducible example is  **self-contained**, so that it will run on anybody's computer, not just yours.

If you followed the process described above for making your reproducible example complete, then hopefully you've already tackled these important criteria for self-containedness:

- Your reproducible example script includes all necessary `library()` statements :heavy_check_mark:
- Your reproducible example script only refers to R objects (variables, data frames, etc) that were created by code included in the reproducible example script :heavy_check_mark:

The last self-contained criterion to check for is:

- Your reproducible example does **not** include references to files or folders that only exist on your computer :heavy_check_mark:
  
  This last criterion most commonly bites you when you're trying to include some data in your reproducible example. You don't have anything like this in your reproducible example script, _right_? :sweat_smile:

   :x: `awesome_data <- read.csv("C:\Documents\Awesome Project\data.csv")`

:anguished: **So how do I include my data?**

Don't worry, there are plenty of self-contained ways to get data into a reproducible example. Here are instructions for the most common cases:

- **You already have code that loads data from a file**

  You'll need to replace the code that loads your data with a special, self-contained code recipe that recreates the resulting data frame. Start by reading about [**the `dput()` method**][dput] for generating self-contained data.

- **You have example data in a spreadsheet**

   If the data you want to use in your reproducible example are currently living in a spreadsheet, then you should first try [**the `datapasta` method**][datapasta] for generating self-contained data.

> :stop_sign: Neither of these are good ways to load data into R for general use! If your main problem is figuring out how to load your data, check out the [RStudio Data Import Wizard](https://support.rstudio.com/hc/en-us/articles/218611977-Importing-Data-with-RStudio)
 and this helpful [Data Import Cheatsheet](https://resources.rstudio.com/rstudio-developed/data-import).

#### Make it smaller

By now you should have a reproducible example script that includes **all** the code and data necessary to demonstrate your problem, and does so in a **self-contained** way that will run on anybody's computer. The last step is to take a critical look at your reproducible example script and see if it can be **made simpler**.

This might seem like an optional step, but it's pretty important! The hardest part about finding help online is getting to the point where others understand your problem. Everybody has plenty of their own work to do, and limited time to help others. To get the best help possible, your reproducible example needs to be as **easy to understand** as possible, and that means removing distracting details and extraneous steps.

You may feel that extra details or steps in your reproducible example more faithfully describe how you encountered your problem. But people helping you don't usually need to know the particular twisty path you took to getting stuck :dizzy_face:. They just need to clearly see where you're stuck now.

**Ways to streamline your reproducible example:**

- Does the code in your reproducible example script actually use all the packages you're loading at the top?
  - Remove any `library()` statements for packages that aren't being used
- Is all of the code in your reproducible example script related to your problem?
  - Try [commenting out](https://en.wikipedia.org/wiki/Comment_(computer_programming)#Debugging) code that you suspect might not be necessary, then restart R and run your reproducible example script. If it still runs as you expect, remove the commented-out code: you don't need it!
- Can you show your problem with less data?
- Do you even need to use your own idiosyncratic data, or would it be clearer to use a familiar built-in dataset or a small artificial dataset constructed specifically to make a good example?
  - For tips on how to use built-in data sets or how to generate example data, see our [full guide to self-contained data][data].

Crafting the smallest, simplest possible reproducible example is itself a skill that takes practice. You don't have to be completely perfect at this step when you're starting out! Keep an eye on experienced people's reproducible examples to see how code problems can be simplified. You'll get better with practice! :grinning:

<h3 id="heading--reprex-pkg">Step 2: Use the <code>reprex</code> package to check your work and format it for sharing</h3>

[`reprex`](https://reprex.tidyverse.org/) is a tidyverse package that contains tools for preparing reproducible examples to be posted on sites like this one. Using it has two major benefits:

- It automatically **formats** both **your code _and the code's output_** in a way that is easy to read when posted here, and also easy for your helpers to copy, paste, and run themselves.
- It helps you **verify** that your reproducible example really is **complete and self-contained** by running the code in a separate, self-contained R session while generating the formatted output.

#### How to use the `reprex` package

You don't *have* to use `reprex` to prepare your reproducible examples, but we **strongly recommend** that you give it a try.

If you're planning to post your reproducible example on this site, start with these instructions:
- [Use the `reprex` package to prepare your reproducible example for posting][package] 

   **Exception:** you can't use `reprex` to prepare Shiny reproducible examples. For guidance on Shiny reproducible examples, start here: [SHINY GUIDANCE]()

#### If you're not using the `reprex` package

If you choose not to use the `reprex` package on your reproducible example, then it's still up to you to **make sure that the code you post is [properly formatted](https://community.rstudio.com/t/6246)**. Screenshots are [**not** an acceptable substitute](https://community.rstudio.com/t/6824#heading--screenshot) for properly formatted code!

<h2 id="heading--fallback">🔥🚒 Reprex disaster? A last resort fallback</h2>

Did you make an honest attempt at composing a reproducible example and wind up [even more stuck](https://xkcd.com/1739/) than before? :confounded: That's a frustrating situation, and it's very tempting to give up completely. But don't lose heart! There are still things you can do to help your helpers and increase your chances of finding the answers you need.

If you're struggling to make a proper reproducible example, focus on providing as much of **the information that your helpers need** as you can. Make sure your question includes these **key items**:

1. The **complete script** that you were working on when you got stuck, **[properly formatted](https://community.rstudio.com/t/6246)**
   - Even experts usually can't tell what's wrong with your code from only an error message or a verbal description of the problem (this often surprises people who are new to writing code!). Symptoms of code problems can have many possible causes, and problems can start several lines away from where they reveal themselves, so people need to see the full context of what you were doing. 
2. The **result of running `str()`** on any data frames you were working with, **[properly formatted](https://community.rstudio.com/t/6246)**
   - `str()` (for "structure") is a function that reveals how R understands your data frame internally. Many common problems can be diagnosed by examining `str()` output.

Remember, screenshots are [**not** an acceptable substitute](https://community.rstudio.com/t/6824#heading--screenshot) for properly formatted code and console output!

### Have realistic expectations

Even if you've done your best to give your helpers useful information, it may still be difficult (or impossible :disappointed:) to answer your question without a reproducible example. Your question may take longer to attract answers, and helpers may only be able to offer limited help. Be patient, and do what you can to answer any follow-up questions. In the end, your best bet may be to give the reproducible example another try.

### If you need help making a reproducible example, ask about that in a separate topic

We welcome questions about how to make reproducible examples! :grinning: But it gets confusing when questions about a code problem are mixed up with questions about other problems you encountered while trying to make a reproducible example to illustrate your code problem :dizzy_face:.

- Start a new topic explaining where you got stuck when working on your reproducible example, and **include a link** to the topic that contains your original question
- Back in the original question topic, **include a link** to your reprex-problem topic

All this cross-linking will help people see what you've tried, while keeping the individual topics easy to digest.

<!--stackedit_data:
eyJoaXN0b3J5IjpbNzYxOTI3MjA1LDEwMjM4MDAzMTYsLTE3Nz
A5NTMyMjQsODE4NTA3ODczLC02NDA1MTU0OThdfQ==
-->
