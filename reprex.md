[tips-code]: https://github.com/jcblum/community-faqs/blob/master/code-formatting_6246.md
[reprex]: reprex.md
[newbie]: reprex_newbie.md
[install]: reprex_install-packages.md
[shiny-cloud]: reprex_shiny_cloud.md
[data]: reprexdata_advanced.md
[dput]: reprexdata_dput.md
[datapasta]: reprexdata_datapasta.md
[readr]: reprexdata_readr.md
[remote]: reprexdata_remote.md

# All About Reproducible Examples

The gold standard for communicating about code problems is to compose a **small, self-contained reproducible example** ("reprex" for short). A reproducible example is a chunk of code that both demonstrates the problem you are having _and_ will run on anybody's computer. When you're asking a code question here, people will expect you to try to create a reproducible example to go with it.

<!--
A reproducible example needs to be both *easy to read* and *easy to run*, because helpers will need to both read your code and **run it themselves** in order to figure out what's wrong and suggest solutions.

Composing good reproducible examples is a skill that takes time and practice to learn, but experienced coders agree that it is the best thing you can do to  increase your chances of getting the help you need.
-->

<!--
### What's in a Reproducible Example?

Parts of a reproducible example:

1. **background information** - Describe what you are trying to do. What have you already done?
1.  **complete set up** - include any `library()` calls and data to reproduce your issue.
**data for a reprex**: [Here's a discussion on setting up data for a reprex](https://community.rstudio.com/t/best-practices-how-to-prepare-your-own-data-for-use-in-a-reprex-if-you-can-t-or-don-t-know-how-to-reproduce-a-problem-with-a-built-in-dataset/5346)
2. **make it run** - include the minimal code required to reproduce your error on the data provided.
People should be able to copy and paste your `code chunk` and get the same error.
[How do I format my text so it has nice `code chunks`?](https://community.rstudio.com/t/faq-how-to-make-your-code-look-nice-markdown-formatting/6246)
3. **minimal** - strip away everything that is not directly related to your problem.  This usually involves creating a much smaller and simpler set of code and data compared to that which created your issue.
-->
### The `reprex` package helps prepare reproducible examples

When creating a reprex by hand, it’s easy to accidentally miss something that means your code can’t be run on someone else’s computer. Avoid this problem by using the [`reprex`-package](https://www.tidyverse.org/help/).
The `reprex` package will save effort for you and others who want to help.

## Why are reproducible examples so important?

A reproducible example needs to be both *easy to read* and *easy to run*, because helpers will need to both read your code and **run it themselves** in order to figure out what's wrong and suggest solutions.

Most people here are helping others for free, on their own time. Every extra step that it takes for helpers to work on your problem is a reason for them to move on to a different question.

<!--
- Helpers need to both **read and run** your code in order to figure out what's wrong.
- Many helpers don't want to suggest solutions they haven't been able to test for themselves by running code.
- Even experts usually can't tell what caused an error message without seeing all of the code that produced the message, not just the line where the error occurred.
- Understanding a piece of code you didn't write is challenging, even for experts. Extraneous bits of code that aren't related to the core problem only make this harder.
-->

## New to reproducible examples?

### Start here!

[Beginner's guide to creating a reproducible example][newbie]

### :confused: Sorry, I read that and I'm still confused

Different explanations work better for different people. Maybe one of these resources will click with you, instead?

#### General reproducible example advice
- :page_with_curl: https://community.rstudio.com/t/faq-how-to-do-a-minimal-reproducible-example-reprex-for-beginners/23061 (contributed Community guide)
- :link: [Get help!](https://www.tidyverse.org/help/) (Tidyverse guide to getting help)
- :book: [How to Write a Reproducible Example](http://adv-r.had.co.nz/Reproducibility.html) (chapter from Advanced R, 1st edition, by Hadley Wickham)
- :book: [Reprex Dos and Don'ts](https://reprex.tidyverse.org/articles/reprex-dos-and-donts.html) (article from `reprex` package documentation)


#### Using the `reprex` package to prepare reproducible examples
- :link: [So You've Been Asked to Make a Reprex](https://www.jessemaegan.com/post/so-you-ve-been-asked-to-make-a-reprex) (blog post by Jesse Mostipak)
- :movie_camera: [Reproducible examples and the `reprex` package](https://community.rstudio.com/t/video-reproducible-examples-and-the-reprex-package/14732) (video by `reprex` package developer Jenny Bryan)
- :book: [How to Use `reprex`](https://reprex.tidyverse.org/articles/articles/learn-reprex.html) (article from `reprex` package documentation)
- :book: [Magic `reprex`](https://reprex.tidyverse.org/articles/articles/magic-reprex.html) (article from `reprex` package documentation)

## Looking to up your reprex game?

- :page_with_curl: [How to get data into your reproducible example][data] (Community guide)
- :link: [How to make a great R reproducible example? aka MCVE](https://stackoverflow.com/questions/5963269/how-to-make-a-great-r-reproducible-example-aka-mcve-minimal-complete-and-ver) (StackOverflow question)
- :link: [Three tips for posting good questions to R-help and Stack Overflow](https://www.r-bloggers.com/three-tips-for-posting-good-questions-to-r-help-and-stack-overflow/) (R-Bloggers post)
- :book: [The R Inferno, Circle 9: Unhelpfully Seeking Help](http://www.burns-stat.com/pages/Tutor/R_inferno.pdf), by Patrick Burns (classic reference to the tricky bits of R, written as a parody of [Dante's _Inferno_](https://en.wikipedia.org/wiki/Inferno_(Dante)))

### Background on the `reprex` package

- :link: [`reprex` package on GitHub](https://github.com/tidyverse/reprex): read the source, check out known issues, and pitch in to help!
- :movie_camera: [How to ask questions so they get answered! Possibly by yourself! rOpenSci Community Call v13](https://vimeo.com/208749032): Jenny Bryan introduces the `reprex` package (`reprex` material begins ~10:40)

## Special circumstances

There are a few cases where specific methods are necessary for composing a good reproducible example. If one of these situations applies to you, make sure you've read the instructions linked below so you don't get tripped up!

### Shiny reproducible examples

### Package installation problems

### Personal, Private, and Protected Information

You should not share private data or personal or protected information in your posts here. A non-exhaustive list of things that **must not** appear in your reproducible examples:

- Mailing addresses
- Email addresses
- IP addresses
- Protected or personally identifiable health data
- Private or proprietary data

To learn more about acceptable ways to ask questions relating to protected data or share contact information, and to find out what to do if you see a violation of these rules, check out this Community guide: https://community.rstudio.com/t/personally-identifiable-protected-information/9993.

It's also a good idea to be familiar with this site's [Privacy Policy](https://community.rstudio.com/privacy).
