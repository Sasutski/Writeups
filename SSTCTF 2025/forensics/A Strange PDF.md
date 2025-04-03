# A Strange PDF

## Difficulty: Easy

We are given ```dist_mydocment.pdf``` and the context:
> Isn't this just an empty pdf..?

After opening it, we see that there is indeed nothing, just three blank pages.

Since I'm on Mac, I used Preview's built in info button to look deeper into what was really in the pdf.
![](images/info.png)

Nothing much in general info
![](generalinfo.png)
However, things get interest when you go to the **Annotations** page.
![](annotation.png)

We see a **Rectangle** that seems to be on page 2. Seeing this, I double click on it.
![](revealedwhite.png)

and it shows the completely white rectangle hiding the flag.

Modifying it reveals the flag
![](flagfoundwhite.png)


Answer: **sstctf{pdf3xpr7}**
