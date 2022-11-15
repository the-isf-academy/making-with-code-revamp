---
title: 00. Turtle
slug: lab0_turtle
type: lab
resources:
- name: GitHub
  src: images/courses/cs9/unit00/00_git_github.png
numberHeaders: true
repo_url: https://github.com/cproctor/mwc-pedprog-unit00-lab00.git
init_action: clone
draft: false
---


# Welcome to Making with Code! 

We're glad you're here! yay 😄

If you have not yet completed the [initial setup]({{< ref "../../initial_setup.md" >}}), 
please do that before you start. 


{{< aside "FYI" >}}
*Hello! I'm the For Your Information Space Invader. I'll be stopping by
every once in a while to give you some extra information about labs or the content you're
learning.*

**Here's my first FYI:** Sometimes you'll see 💻 in a lab. This means that you
need do something that involves writing code or using your Terminal (MacOS) or Ubunutu (Windows). You can use these like little action items during labs.

The {{< look-action >}} symbol is another helpful symbol to indicate that you need to do
something. This one means that there's something important for you to read or watch.
{{< /aside >}}

---

## [0] Into the Terminal
{{< look-action " Take a peek at your Desktop." >}} **You should see a new folder called `making_with_code`** created by the configuration
script. (If you told `mwc setup` you wanted to install somewhere else, you'll need to adapt the following instructions 
to your situation.) We are going to navigate to that folder using the Terminal interface.


### [Terminal: a new user interface]

You're probably used to interacting with the files in your computer through a *Graphical User Interface
(GUI)* like Finder. Terminal allows us to interact with the files in our computer through a *Text-based
User Interface (TUI)*. The files in our computers are organized in nested folders known as
*directories*.

{{< figure src="https://help.apple.com/assets/6152754A4192845C4361C49A/6152754B4192845C4361C4A1/en_GB/d94aa1c4979b25e9ffbda97fcbae219a.png" width="25%"  >}}

{{< code-action >}} **Open a new Terminal window.** Terminal opens in your `home` directory (also known as `~`), but we will be working in the `making_with_code` directory. Since the home directory holds all your stuff, the `making_with_code` directory
must be somewhere inside the `home` directory.

{{< code-action >}} **Type** `ls` **into the command line and press** `return`. This will list all the files and subdirectories in the current directory. You should see that `Desktop` is one of the subdirectories listed. Let's move into that
subdirectory. 

```shell
~$ ls
Applications  Desktop  Documents  Downloads	 Library  Movies  Music	 Pictures
```


{{< code-action >}} **Type** `cd Desktop` **into the command line and press**
`return`. `cd` stands for "change directory". Now, list all the items in your `Desktop`
directory using `ls`.

```shell
~$ cd Desktop
~/Desktop$ ls
Screen Shot 2019-08-15 at 12.34.48 AM.png  dobby.gif			  warsaw-boarding-pass.pdf
making_with_code						                   lentil loaf gravy.pdf
```
---

### [Compare the output in the Terminal window with the Desktop shown by the GUI.]

{{< code-action >}} **Type** `open .` **to open Finder.** All of the files and folders are the same!
The Terminal really does show us the same files and directories as our GUI!

{{< figure src="images/courses/cs9/unit00/00_setup_compare_terminal_finder.png" width="100%" title="Comparing Finder and Terminal files" >}}

Going back to the Terminal, we can also see that the `making_with_code` subdirectory is inside the
`Desktop` directory. 

{{< code-action >}} **Change into the** `making_with_code` **directory and list what
it contains.** There is a subdirectory called `pedprog` and another subdirectory that 
named `unit00`, which holds everything related to Unit 0. Inside `unit00` is yet another
subdirectory, `lab00`, which is where we want to be today.

```shell
~/Desktop$ cd making_with_code
~/Desktop/making_with_code$ ls
pedprog
~/Desktop/making_with_code$ cd pedprog
~/Desktop/making_with_code/pedprog$ ls
unit00
~/Desktop/making_with_code/pedprog$ cd unit00
~/Desktop/making_with_code/pedprog/unit00$ ls
lab00
~/Desktop/making_with_code/pedprog/unit00$ cd lab00
~/Desktop/making_with_code/pedprog/unit00/lab00$
```

---

### [Terminal Commands]

Here a summary of the commands you just learned and few extra helpful ones:


| Command                 | Description |
| :---------------------- | :-----------|
| `cd Desktop/making_with_code/pedprog/unit00`|to change to the directory "unit00" |
| `atom .`                |  to open Atom.   |
| `atom newfilename.py`   |  to make a new file. You can also choose to make a new file by right-clicking on the folder in atom. |
| `python newfilename.py` |  to run the program. |
| `↑`                     |  to get to the previous command you typed in terminal |
| `tab`                   |  autocompletes the command or path as much as possible |
| `tab` `tab`             |  shows possible autocompletions |


---

## [1] Introduction to writing code
Now that you can navigate in the Terminal, let's write some code! Throughout the class, we
will be using the Python programming language to help us perform computational tasks. In
this unit, we'll be using a software library called turtle to draw things with code.

Every time you start working on a project, you need to enter a shell which is configured properly
for that project using a tool called [Poetry](https://python-poetry.org/). 
([Developers often have several versions of Python installed and many versions of Python packages](https://xkcd.com/1987/). 
Poetry makes sure you don't have to worry about it.)

{{< code-action "Enter a poetry shell:" >}}

```shell
poetry shell
```

### [Writing programs]
Python programs start out as simple text files. To write a Python program, we start out
by writing a text file. During the setup, we downloaded a special text editor made for
the purpose of writing code. 

{{< figure src="https://w7.pngwing.com/pngs/975/30/png-transparent-atom-source-code-editor-text-editor-logo-visual-studio-code-design-text-logo-mac.png" width="25%"  >}}


**Before you start, make sure you are still in `~/Desktop/making_with_code/<your username>/unit00/lab00`.**

{{< code-action "Use the Terminal commands below to open a new file in Atom." >}} 

```shell
atom first_program.py
```

This should open a new Atom window with a tab that says `first_program.py`.
Python programs consist of lines of code that tell your computer what you want it to do.

{{< code-action >}} **Paste the following lines of code into the** `first_program.py` **file in Atom:**

```python
from turtle import *

forward(50)
right(90)
forward(50)
right(90)
forward(50)
right(90)
forward(50)
right(90)

input()
```

Can you guess what these lines of code are telling the computer to draw?

---

### [Running programs]
Now that you've written a program, let's run it to see what it does!

To run Python code, we need to give our programs to a python interpretor. Fortunately,
we installed a Python interpretor in your Terminal during the setup. To use it,
you can use the command `python file-name.py`. This will read in the text file you
pass it, interpret it as a Python program, translate it into a format that your computer
can understand, and then give those instructions to your computer.

Let's try it with the program you just wrote in Atom.  

{{< code-action "Save" >}} `first_program.py` file in Atom.

{{< code-action "Run the program in Terminal using the command," >}}  `python3 first_program.py`.
What happend? Did your computer draw what you expected?

{{< code-action "End the program" >}} and close the turtle window by pressing `return`.

{{< aside >}}
Most files in your computer have a file type that tells your computer how to interpret them.
The file type is determined by the letters after the dot in the file name.

Notice that even though python programs are just text files, we're saving it with the `.py`
file extension. This tells our computer that this file should be interpreted as a python
file.

<br>

{{< /aside >}}

{{< expand "Video Tutorial" >}}

{{< youtube id="7bnoG9Hzihg" >}}

{{< /expand >}}


#### You just ran your first Python program! Congrats!! 🎉


---



## [2] Let's draw!
Now that you've got the basics, try to make it more interesting.


{{< figure src="https://freshgadgets.nl/wp-content/uploads/2014/12/inspirograph2.jpg" width="75%" title="Python Turtle Examples" >}}

{{< code-action "Experiment with turtle commands below by editing your" >}} `first_program.py` file. 

| Function |       Input      |   Example Use  | Explanation                                                                                                                      |
|:--------:|:----------------:|:--------------:|----------------------------------------------------------------------------------------------------------------------------------|
|  forward |      amount      |  forward(100)  | Moves the turtle forward by the specified amount                                                                                 |
| backward |      amount      |  backward(100) | Moves the turtle backward by the specified amount                                                                                |
|   right  | angle in degrees |    right(45)   | Turns the turtle clockwise by the specified angle                                                                                |
|   left   | angle in degress |    left(45)    | Turns the turtle counter clockwise by the specified angle                                                                        |
|   color  |     colorname    |  color("red")  | Sets the color for drawing. Use "red", "black", etc.  [Here's a list of all the colors](https://trinket.io/docs/colors).                                           |
|   shape  |     shapename    | shape("arrow") | Should be "arrow", "classic", "turtle", or "circle"                                                                              |
|   speed  | number from 0-10 |    speed(0)    | Determines the speed at which the turtle moves around the window. 1 for slowest, 3 for normal speed, 10 for fast, 0 for fastest. |
|  pendown |       None       |    pendown()   | Puts down the turtle/pen so that it draws when it moves                                                                          |
|   penup  |       None       |     penup()    | Picks up the turtle/pen so that it doesn’t draw when it moves                                                                    |
| pensize  |       width      |   pensize(4)   | Sets the width of the pen for drawing                                                                                            |

---

### [Error and bugs]
While trying this out, you may come across errors or bugs, do not fear!
Write the issue down, and we can talk about it during class. Try to
figure out whether your bug is a:
{{< columns >}}
**Programmatic error** (which happens when the program does something different than what
you wanted. Remember that this happened when we set the angle to the wrong number)

<--->

**Syntax error** (which happens when the program crashes because the program cannot be
understood by the computer. Remember that this happened when we forgot a parentheses).

{{< /columns >}}
