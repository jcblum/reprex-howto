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

# Shiny reprex using RStudio Cloud

- [:stop_sign: Is RStudio Cloud the right choice for sharing your Shiny reproducible example?](#heading--rightchoice)
- [How to share a Shiny reproducible example using RStudio Cloud](#heading--howto)
- [Tweaks](#heading--tweaks)
	 - [Skip steps by creating a new Cloud Project from a GitHub repo](#heading--github)
	 - [Ensure that package versions match exactly](#heading--pkgversion)

<h2 id="heading--rightchoice">🛑 Is RStudio Cloud the right choice for sharing your Shiny reproducible example?</h2>

- You've already tried boiling your problem down to example code inside a [standard Shiny reprex skeleton](), and got stuck
- The app behavior you need to demonstrate involves… _(?? what's necessarily complex? modules? multiple interacting scripts? lots of customization?)_
- Your Shiny reproducible example can run within RStudio Cloud's resource limits:
	- Necessary packages must be able to install within the 1GB memory limit. But thanks to RSPM's support for Linux binaries, very few packages should need to compile.
	- Data processing, model fitting, or other computations performed by app code must be able to operate within the 1GB memory limit.
	- Apps that rely on unusual system dependencies external to R may not be able to run on RStudio Cloud.

<h2 id="heading--howto">How to share a Shiny reproducible example using RStudio Cloud</h2>

### What's going to happen

- Develop your reprex app in your normal dev environment, making sure all the script files and resources you need are inside a single Shiny app folder
- Make an RStudio Cloud account (if necessary) and then make a new RStudio Cloud Project inside your account's main workspace.
- A new Cloud Project is like a separate computer with a fresh installation of RStudio and R, so you will need to do some setup to get it ready to run your reprex app. Choose a matching version of R and install all the R packages your reprex app requires.
- Upload the compressed reprex app folder and do a test run.
- Change the sharing settings so that others can access your app. They will be able to view and interact with a temporary copy of your Cloud Project, or make a copy of it to edit in their own account, but they will **not** be able to make edits to your original copy. If someone wants to show you changes they made that solved your problem, they'll need to share their copy of the Cloud Project back with you.
- Keep discussing the problem in the Community topic. Please make sure to describe and share whatever solutions you and your helpers discover directly in the replies to the topic, so that the discussion will be helpful to others in the future.

### Step by step

1. Make a new Shiny app to contain your reproducible example, using your normal development tools. At minimum, this app should consist of **a single app folder** containing:
	- One `app.R` file, or a pair of `ui.R` and `server.R` files
	- Any other resources your app needs (additional script files, example data files, etc.)

	   One approach to composing a Shiny reproducible example is to start with a blank default app (for instance, by using the RStudio New Shiny Web App wizard), then copy over _just enough_ code and resources from your real app to demonstrate your problem. 

	   By removing distractions and keeping your reproducible example focused on your specific problem, others will be better able to quickly understand your problem and suggest solutions.

2. Do a test run of your Shiny reproducible example to make sure you don't have any missing `library()` statements or other typos unrelated to the problem you're seeking help for.

3. Compress the reproducible example app folder into a ZIP archive.

4. Make an RStudio Cloud account.

5. Make a new project in "Your Workspace".
	- New Project button
	- "Deploying Project" spinner, wait until RStudio interface appears
	- Click on Untitled Project (upper left) to change name

6. Choose a version of R to use in your Cloud project that matches (as closely as possible) the version you are using on the system where you developed your reproducible example app.

7. Install all the packages your reproducible example app needs, and their dependencies. Don't forget to install `shiny`!

8. From the Files pane, click **Upload**, and choose the ZIP archive of your Shiny reprex app folder. The archive will be uploaded to the root level of your Cloud Project and automatically expanded.

9. Try running your reproducible example app from within RStudio Cloud to make sure that there aren't any missing packages or other unanticipated problems.

10. Make your reproducible example app public:
	- Click on the gear icon (upper right). In the panel that opens, click on the "Access" tab (padlock icon).
	- Under "Who can view this project", select "Everyone".

11. Share a link to your project in your topic on Community. To get the project link, just copy the web address from the browser tab where the project is open. It should look like: `https://rstudio.cloud/project/123456`.

<h2 id="heading--tweaks">Tweaks</h2>

<h3 id="heading--github">Skip steps by creating a new Cloud Project from a GitHub repo</h3>

- Assume comfort with git/GitHub

<h3 id="heading--pkgversion">Ensure that package versions match exactly</h3>

- `packrat`/`renv`

<!--stackedit_data:
eyJkaXNjdXNzaW9ucyI6eyI1Zm5RUk9MRGZKc1hiT0ZNIjp7In
N0YXJ0Ijo0Njk4LCJlbmQiOjQ3NzAsInRleHQiOiIjIyMgRW5z
dXJlIHRoYXQgcGFja2FnZSB2ZXJzaW9ucyBtYXRjaCBleGFjdG
x5IGJ5IHVzaW5nIGBwYWNrcmF0YC9gcmVudmAifSwia3ZDdERa
THFNUHVENlNRSCI6eyJzdGFydCI6MTI4NSwiZW5kIjoxMzMyLC
J0ZXh0IjoiQSBuZXcgQ2xvdWQgUHJvamVjdCBpcyBsaWtlIGEg
c2VwYXJhdGUgY29tcHV0ZXIifSwiODc5MWlHTTFJWlNRTW9uUC
I6eyJzdGFydCI6MzAyLCJlbmQiOjM5NiwidGV4dCI6Iig/PyB3
aGF0J3MgbmVjZXNzYXJpbHkgY29tcGxleD8gbW9kdWxlcz8gbX
VsdGlwbGUgaW50ZXJhY3Rpbmcgc2NyaXB0cz8gbG90cyBvZuKA
piJ9LCJ3dEpDalRVWmhlTXV5RTRiIjp7InN0YXJ0Ijo1OTksIm
VuZCI6NjI1LCJ0ZXh0IjoidGhpcyBvZnRlbiBpc24ndCBhIHBy
b2JsZW0ifSwiNkRCUnVyVER5RkdUUUM4aSI6eyJzdGFydCI6OD
E5LCJlbmQiOjg1NCwidGV4dCI6InJlbHkgb24gdW51c3VhbCBz
eXN0ZW0gZGVwZW5kZW5jaWVzIn0sIkdUbHpXQTBBdWdWdGZXNG
wiOnsic3RhcnQiOjY3NywiZW5kIjo3MzAsInRleHQiOiJEYXRh
IHByb2Nlc3NpbmcsIG1vZGVsIGZpdHRpbmcsIG9yIG90aGVyIG
NvbXB1dGF0aW9ucyJ9LCIzZjlCTUx4QjQ0SGZ4bWplIjp7InN0
YXJ0Ijo5ODEsImVuZCI6MTAwMywidGV4dCI6IldoYXQncyBnb2
luZyB0byBoYXBwZW4ifSwiaUlGZmVRdElWU3BCNUY4SiI6eyJz
dGFydCI6MzU4MCwiZW5kIjozNjEyLCJ0ZXh0IjoibWF0Y2hlcy
AoYXMgY2xvc2VseSBhcyBwb3NzaWJsZSkifX0sImNvbW1lbnRz
Ijp7InZhWVgwUGljMHFVQVFsV1YiOnsiZGlzY3Vzc2lvbklkIj
oiNWZuUVJPTERmSnNYYk9GTSIsInN1YiI6ImdvOjExODIyOTkw
Mjk0NzI0NTM4MTg3MyIsInRleHQiOiJUaGlzIGlzIHBvdGVudG
lhbGx5IGEgbWFqb3IgZ290Y2hhICh0aGF0IHlvdSBoYXZlIHRv
IGluc3RhbGwgcGFja2FnZXMgaW50byBDbG91ZCB5b3Vyc2VsZi
wgc28gaXQncyB1cCB0byB5b3UgdG8gbWFrZSBzdXJlIHRoZXkg
YWxsIG1hdGNoIHlvdXIgbG9jYWwgZGV2IGVudmlyb25tZW50KS
wgYnV0IGl0IGFsc28gc2VlbXMgbGlrZSB0aGUga2luZCBvZiB0
aGluZyB0aGF0J3Mgbm90IHJlYWxseSBiZWdpbm5lci1mcmllbm
RseSBpbiBhbnkgd2F5IiwiY3JlYXRlZCI6MTU3MjIxODc3NTk4
N30sIkwzWFFCWGhGM09wQ01KVWEiOnsiZGlzY3Vzc2lvbklkIj
oia3ZDdERaTHFNUHVENlNRSCIsInN1YiI6ImdvOjExODIyOTkw
Mjk0NzI0NTM4MTg3MyIsInRleHQiOiJNZW50aW9uIHRoYXQgQ2
xvdWQgaXMgcnVubmluZyBvbiAodmlydHVhbCkgTGludXg/IE1p
Z2h0IG5vdCBiZSBvYnZpb3VzIHRvIHNvbWVvbmUgd2hvJ3Mgbm
V2ZXIgdXNlZCBSU3R1ZGlvIFNlcnZlciBiZWZvcmUuIiwiY3Jl
YXRlZCI6MTU3MjIxODg2MjEyM30sImJvTU9xWFd6N0N5ZGhBam
MiOnsiZGlzY3Vzc2lvbklkIjoiODc5MWlHTTFJWlNRTW9uUCIs
InN1YiI6ImdvOjExODIyOTkwMjk0NzI0NTM4MTg3MyIsInRleH
QiOiJOb3Qgc3VyZSB3aGF0IHRoZSBiZXN0IGNyaXRlcmlhIHRv
IHF1b3RlIGhlcmUgd2lsbCBiZSIsImNyZWF0ZWQiOjE1NzIyMT
g4ODg1Mjl9LCJjejdqU0NpSWZTdlhWVkRpIjp7ImRpc2N1c3Np
b25JZCI6Ind0SkNqVFVaaGVNdXlFNGIiLCJzdWIiOiJnbzoxMT
gyMjk5MDI5NDcyNDUzODE4NzMiLCJ0ZXh0IjoiU29tZSBwYWNr
YWdlcyBkbyBzdGlsbCBpbnN0YWxsIGZyb20gc291cmNlLCBhbm
QgSSBkb24ndCBrbm93IGhvdyB0byBwcmVkaWN0IHdoaWNoIG9u
ZXMuLi4iLCJjcmVhdGVkIjoxNTcyMjE4OTE0MTM4fSwieWpWcG
pnQm5NQVk5TTFheSI6eyJkaXNjdXNzaW9uSWQiOiI2REJSdXJU
RHlGR1RRQzhpIiwic3ViIjoiZ286MTE4MjI5OTAyOTQ3MjQ1Mz
gxODczIiwidGV4dCI6IkNpdGUgb25lIG9yIHR3byBleGFtcGxl
cyB0aGF0IGhhdmUgY29tZSB1cCBpbiBDb21tdW5pdHkgcXVlc3
Rpb25zIGFib3V0IENsb3VkPyBOb3Qgc3VyZSB3aGF0J3MgYmVl
biBhZGRlZCB0byB0aGUgQ2xvdWQgaW1hZ2VzIGF0IHRoaXMgcG
9pbnQsIGJ1dCBJIHRoaW5rIGByZ2RhbGAgdXNlZCB0byBiZSBh
IHByb2JsZW0/IiwiY3JlYXRlZCI6MTU3MjIxODk2MDEzM30sIl
oySXlTOVU0NTVYRkRwMHIiOnsiZGlzY3Vzc2lvbklkIjoiR1Rs
eldBMEF1Z1Z0Zlc0bCIsInN1YiI6ImdvOjExODIyOTkwMjk0Nz
I0NTM4MTg3MyIsInRleHQiOiJDaXRlIHNvbWUga25vd24gZXhh
bXBsZXMgdGhhdCB3aWxsIG5vdCB3b3JrPyBFLmcuLCB5b3UgY2
FuJ3QgZXZlbiBydW4gYW55IGByc3RhbmAgb3IgYHJzdGFuYXJt
YCBleGFtcGxlIGNvZGUgc3VjY2Vzc2Z1bGx5LCBsYXN0IHRpbW
UgSSBjaGVja2VkLiIsImNyZWF0ZWQiOjE1NzIyMTkwMTQ1NjZ9
LCJ2Qno3bmgwdjFHT0NxZmdMIjp7ImRpc2N1c3Npb25JZCI6Ij
NmOUJNTHhCNDRIZnhtamUiLCJzdWIiOiJnbzoxMTgyMjk5MDI5
NDcyNDUzODE4NzMiLCJ0ZXh0IjoiTmVlZHMgdG8gYmUgZGUtYn
VsbGV0aXplZCIsImNyZWF0ZWQiOjE1NzIyMTkwNDIzNTh9LCJB
ZVVEaUVTWHl2UjM2SHBtIjp7ImRpc2N1c3Npb25JZCI6IjVmbl
FST0xEZkpzWGJPRk0iLCJzdWIiOiJnbzoxMTgyMjk5MDI5NDcy
NDUzODE4NzMiLCJ0ZXh0IjoiQWxzbywgd2lsbCBgcGFja3JhdG
AvYHJlbnZgIGV2ZW4gd29yayBvbiBDbG91ZD8iLCJjcmVhdGVk
IjoxNTcyMjE5MTM4ODMyfSwiZDZjN3FZempZQjlIeGpaciI6ey
JkaXNjdXNzaW9uSWQiOiJpSUZmZVF0SVZTcEI1RjhKIiwic3Vi
IjoiZ286MTE4MjI5OTAyOTQ3MjQ1MzgxODczIiwidGV4dCI6Ik
1lbnRpb24gdGhhdCBpdCBvbmx5IG5lZWRzIHRvIG1hdGNoIG1h
am9yLm1pbm9yLCBub3QgbWFqb3IubWlub3IucGF0Y2g/IiwiY3
JlYXRlZCI6MTU3NDE5OTUyMDk1Nn19LCJoaXN0b3J5IjpbMTM2
NDkzNTc5MCwtMTI5ODQxOTEwOSwtMTI2ODU3MzE4M119
-->