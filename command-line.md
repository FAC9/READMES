# Command Line

## Tutorial

In this tutorial, we're going to find out how to navigate around your computer using the command line.

When you're used to using a graphical file browser to navigate between your folders (aka directories), the command line can feel dry at best. But once you get used to it, the advantage is that typing is just much faster than using your mouse.

So with that in mind, let's dive in.


### Where am I?

At first, the comamnd line can feel less intuitive than the visual interfaces that we are used to.You may find it easy to forget what you have typed, and therefore get lost.

But when you use a GUI, how do you know which directory you are in? Well, you can see the path at the top of the window, right?

So in the command line, we can just type `pwd`. This stands for 'print working directory'. Type this into your command line now, and your terminal will print out the path to your current directory.

For example, mine looks like this:

```
$ pwd
/home/jsms90
$
```

Great, now you can always find out exactly where you are!

### Moving around

#### Where can I go from here?

Ok, that's useful. But what we really want to do is be able to move between directories.

In a traditional GUI, you see icons for each of the available files and directories. In the command line we can find out this information by printing a list. The basic command for this is `ls`.

Go ahead and type `ls` into your command line now for a list of your files and directories.

For example, I have:
```
$ ls
index.txt notes READMES semantic-html-workshop
```

So I have one file: `index.txt`. I can tell that it is a file, rather than a directory, because it has a file type after the dot.

I also have three directories: `notes`, `READMES` and `semantic-html-workshop`.


#### Changing directory

So now that you know where you are, and you know which directories you can move into, you can use the `cd` command to 'change directory'.

To be specific, type the directory that you want to move into directly after `cd`. For example, I'm going to go into `notes`, so I would type `cd notes`.

Choose one of the directories that you saw when you typed `ls` and use `cd` to move into it.

If you type `ls` again, you can now see what is inside here.

If you want to go back to the previous directory, type `cd ..`. This would take me back to `FAC9`.

#### I just want to go home :cry:

Don't cry! If you just want to head back home, `cd` by itself will take you straight there.


### What is Bash? ###

Short answer: **Bash is a Unix shell**.

 - A **shell** is a user interface for access to an operating system's services. It is an example of a command-line interface (CLI), as opposed to the graphical user interface (GUI). It is named a shell because it is a layer around the operating system kernel. Shells may be used interactively, with input typed from the keyboard in the text window, or non-interactively, reading commands from a file (a script).

- **Unix shell** is a shell that provides a traditional Unix-like command line user interface.

- **Unix** is a family of multitasking, multiuser computer operating systems. Unix-like operating systems include OS X and Linux (Ubuntu).

#### Key facts ####

- Bash was written by Brian Fox for the GNU project, and was first released in 1989
- GNU is an open-source operating system and an extensive collection of computer software
- Its features are based on Bourne shell, C shell and Korn shell
- Its name is an acronym for 'Bourne-again shell'

#### Supported features ####

Bash supports wildcard matching, process piping, here documents, command substitution, variables, and structures for condition testing and iteration.

#### Terminal ####

Bash is the default shell used in terminals on OS X and Ubuntu. It is what you have been using when you are creating or moving to a directory using the command line.

You may consider installing Z shell (zsh), an extended Bourne shell with a large number of improvements.

### How can you customise your terminal?
It's possible to customise your terminal in both appearance and functionality. Making changes to the appearance may be for aesthetic reasons, but it's also a helpful visual shorthand to assess what's going on in your terminal screen.

There are some differences between operating systems.

#### Prompt
Sometimes people like to change the prompt or add an icon to it to personalise it. Setting up a custom prompt involves a number of steps.
- [Linux tutorial](http://www.cyberciti.biz/tips/howto-linux-unix-bash-shell-setup-prompt.html)
- [OSX tutorial](http://osxdaily.com/2006/12/11/how-to-customize-your-terminal-prompt/)

#### Ubuntu colour
- Using the terminal menu click on 'Edit' and select 'Profile Preferences', which allows you to change the appearance of the cursor, colours, scrolling behaviour, and add an audible notification to the terminal if you like.
- Click on help in 'Profile Preferences' for a menu of specific changes you can make, complete with instructions.

#### OSX colour
- Open Profiles in the Preferences (Command + ,) to change the cursor shape, add a background image, change text size and colour.

Another [helpful link](http://mindthecode.com/customize-the-terminal/) on cutomisation

### What are the benefits of working with the command line rather than a GUI?

GUI stands for Graphic User Interface. In this context we are talking about
using GitHub on your browser to edit your files as opposed to using
the Command Line. This README focuses on the benefits of using the command line
rather than the GUI.

|   |  Command line | GUI |
|---|---|---|---|
| Control  | You have much greater control over your operating system and the files in GitHub with the command line.  | Not all tasks can be done with the GUI.|
|  Speed | The command line is much quicker than the GUI and lots of complex actions can be done completed with a single line of code. <br><br> An example of the increased speed of using the command line over the GUI is the ease with which you can view .dotfiles by simply typing the 'ls -a' command.|  Having to use a mouse to navigate files instead of just a keyboard can make simple tasks take a long time.|
| Multitasking  | The command line is at a disadvantage when it comes to multitasking because you can only type one command at a time. | The GUI enables you to work on many files at once by opening lots of different windows, programs and folders.|
| Ease  | Steep learning curve when first using the command line which can initially put people off using it. <br><br> When working in the command line it is easy to loose  "situational awareness" and errors can be made by editing the wrong files or adding/deleting things from the wrong directory. | Much more intuitive to use and learn when starting out. <br><br> As opposed to the command line it is easier to know in the GUI where you are in a system and which files you are editing.|
| Longevity  | The command line is not going to change too much in the future, with the exception that new commands may be added. | GUIs change all the time and you will need to learn how to use the new interface with each development.|   |

#### Resources / further reading:
- [GUI vs. Command line interface](http://www.softpanorama.org/OFM/gui_vs_command_line.shtml)
- [5 Reasons to Use CLI Over GUI](http://vivapinkfloyd.blogspot.co.uk/2008/07/5-reasons-to-use-cli-over-gui.html)
- [Graphical User Interface (GUI) vs Command Line Interface (CLI)](http://www.louiewong.com/archives/254)
- [Linux: GUI vs. Command Line](https://www.lifewire.com/linux-gui-vs-command-line-2200166)
- [Command line vs. GUI](http://www.computerhope.com/issues/ch000619.htm)

In case you were wondering, the first computer with a GUI was the Xerox 8010 Information System in 1981!
![Xerox 8010](http://www.digibarn.com/collections/systems/xerox-8010/xerox-star-8010-large.jpg "Xerox 8010")
