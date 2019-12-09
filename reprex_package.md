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

# Use the `reprex` package to prepare your reproducible example for posting

Including data in a self-contained way is a common stumbling block for people who are new to creating reproducible examples. Here's how the built-in R function `dput()` can help.

- [Are these instructions for me?](#heading--rightchoice)   
- [How to use `reprex`](#heading--howto)
- [A Worked Example](#heading--example)
- [Tweaks](#heading--tweaks)

<h2 id="heading--rightchoice">🛑 Are these instructions for me?</h2>

If you can answer **YES** to **ALL** of these questions, then skip right on down to "How to"! :grinning:

1. I have written a reproducible example script :heavy_check_mark:
2. I am **NOT** trying to make a reproducible example for a [Shiny](https://shiny.rstudio.com) app :heavy_check_mark:
3. I am using the RStudio IDE (Desktop, Server, or Cloud) :heavy_check_mark:
4. I am planning to post my reproducible example here on Community :heavy_check_mark:

:frowning: Answered **no**? All is not lost!

<details>
<summary>Click here for more help</summary>

1. :sweat_smile: I haven't written my reproducible example yet!
   - Unfortunately, `reprex` can't write your reproducible example for you (that would _really_ be magic! :woman_mage:). If you're looking for guidance on what goes into a good reproducible example, start here: [Beginner's guide to reproducible examples][newbie]

2. :sparkles: I'm making a [Shiny](https://shiny.rstudio.com) reproducible example!
   - The `reprex` package functions don't work on Shiny apps. For guidance on how to prepare a Shiny reproducible example, start here: [SHINY GUIDANCE]().

3. :thinking: I'm not using the RStudio IDE.
   - These instructions show you how to use an [RStudio Addin](https://rstudio.github.io/rstudioaddins/) to process a reproducible example using the `reprex` package. But that's certainly not the only way to use `reprex`! If you're working in another code editor, try the [clipboard-based instructions from the `reprex` package documentation](https://reprex.tidyverse.org/index.html#usage).

4. :nerd_face: I'm planning to post my reproducible example somewhere else.
   - If you're posting in a [GitHub](https://github.com) issue or on [StackOverflow](https://stackoverflow.com), then you're in luck! :grinning: The instructions here will work just fine for you, because all these sites use the same [CommonMark](https://commonmark.org/) formatting conventions.
   - If you want some other type of output, take a look at the `reprex` package's different ["venue" options](https://reprex.tidyverse.org/reference/reprex.html#arguments). You can then adapt these instructions by choosing the "Render reprex…" RStudio Addin (instead of the "Render selection" Addin), which lets you change the venue before rendering begins.

</details>

<h2 id='heading--howto'>How to use <code>reprex</code></h2>

### What's going to happen

You will start by making sure you're set up to use the `reprex` package. You'll need to have the package installed, and you'll need your reproducible example script open in the RStudio Source pane. 

You'll **select** all the lines of code in your reproducible example. Then you'll use an **[RStudio Addin](http://rstudio.github.io/rstudioaddins/)** to tell `reprex` to process the lines of code you just selected. The `reprex` package will begin transforming your reproducible example into formatted output :sparkles:.

When it's done, a **preview** of your formatted reproducible example will appear in the RStudio Viewer pane, and you'll be supplied with a **special chunk of text**, all ready for pasting into a post here! :grinning:

- **Note:** the details of the process differ a bit depending on whether you're using [RStudio Desktop](https://rstudio.com/products/rstudio/#rstudio-desktop) or a version of the IDE that you access through a web browser such as [RStudio Server](https://rstudio.com/products/rstudio/#rstudio-server) or [RStudio Cloud](https://rstudio.cloud/). Don't worry, everything is explained below! :relieved:

### Step by step

1. You should have your reproducible example open in a script file. Check that you are set up correctly to use the `reprex` package:
	- Make sure you have installed  `reprex` with `install.packages("reprex")`, and that you see a <span style="font-size:smaller">"REPREX"</span> section somewhere in your RStudio Addins menu.
	- That's it! You are using `reprex` to _process_ your reproducible example script, but you are not using `reprex` as part of the script itself, so there is no need to include it in your script's `library()` statements.

   ![Script open in RStudio Source pane, REPREX section visible in Addins menu]()

2. Use your cursor to **select all the lines** of your reproducible example.

3. Click on the **Addins menu**, find the <small>REPREX</small> section, and choose **Reprex selection**.

   ![Script lines selected, choosing "Reprex selection" from Addins menu]()

4. The message `Rendering reprex...` will appear in the console as `reprex` does its work. What happens next depends on what version of the RStudio IDE you're using, so now it's time to choose your own adventure…

   <details>
   <summary>🖥 <strong><a href = "https://rstudio.com/products/rstudio/#rstudio-desktop">RStudio Desktop</a>:</strong> RStudio is an app  installed on my computer!</summary>
 
    - A lovely **preview** of the formatted output `reprex` has prepared  will appear in the Viewer pane :nail_care:. (This is just for looking  at! Don't try to copy and paste the preview)
    - A second message will appear in the console: `Rendered reprex is on  the clipboard.` :astonished:
         
       This means that an invisible, **special chunk of text** that  `reprex` produced *has already been copied* to your computer's clipboard behind the scenes  :woman_mage:. If you put your cursor just about anywhere (in any app!) and choose **Paste**, the special chunk of text will be inserted right there :sparkles:. 
       
       If you paste the special chunk of text into a post on this site, then it will produce formatted code that looks just like the preview :grinning:! 
   </details>

   <details>
   <summary>🌐 <strong><a href="https://rstudio.com/products/rstudio/#rstudio-server">RStudio Server</a> or <a href="https://rstudio.cloud/">RStudio Cloud</a>:</strong> I access RStudio from a web browser!</summary>

    - A lovely **preview** of the formatted output `reprex` has prepared  will appear in the Viewer pane :nail_care:. (This is just for looking  at! Don't try to copy and paste the preview)
    - A new message will appear in the console that looks something like:
      
       ```
       Unable to put result on the clipboard. How to get it:
         * Capture what `reprex()` returns.
         * Consult the output file. Control via `outfile` argument.
       Path to `outfile`:
         * /tmp/RtmpAPrrX7/reprexf7309e7776/reprex_reprex.md
       Open the output file for manual copy?
       1: yes
       2: no

       Selection:
       ```
      
      Huh!? :dizzy_face: What's happening is that `reprex` would like to magically copy a **special chunk of text** that it has produced onto your computer's clipboard. But since RStudio is running on a remote server and not on your computer, `reprex` doesn't have any way of accessing your computer's clipboard :worried:. But `reprex` is pretty smart, so (among other things) it's offering to open a window and let you do the copying yourself :relieved:.

    - **Type** `1` next to `Selection:` and press <kbd>Return</kbd> (or <kbd>Enter</kbd>).
      
      A window will appear, containing something that looks like your reproducible example, but with some extra stuff at the top and bottom (and probably some extra lines in the middle). This is the **special chunk of text** that `reprex` produced!

      ![Output window, with all lines selected]()

    - **Select** **ALL** of the text in the window and **copy** it. Make sure you don't miss the very top or very bottom lines!
    - Click the <kbd><strong>Cancel</strong></kbd> button at the bottom of the window (this might seem odd, but clicking <kbd>Save</kbd> doesn't really do anything here).
       
       If you now paste the special chunk of text you just copied into a post on this site, it will produce formatted code that looks just like the preview :grinning:!
   </details>

5. **Almost done!** Before you run off to paste your special chunk of text into your post :sweat_smile:, take a moment to **check the preview** in the Viewer pane. Does everything look the way you expect? If not, go back and edit your reproducible example script, then repeat this process all over again.

6. Finally, **paste** the special chunk of text that `reprex` generated into your post.

   You're done! :tada:

<h2 id='heading--example'>A Worked Example</h2>

<h2 id='heading--tweaks'>Tweaks</h2>