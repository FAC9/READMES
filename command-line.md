# Tutorial

In this tutorial, we're going to find out how to navigate around your computer using the command line.

When you're used to using a graphical file browser to navigate between your folders (aka directories), the command line can feel dry at best. But once you get used to it, the advantage is that typing is just much faster than using your mouse.

So with that in mind, let's dive in.


## Where am I?

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

## Moving around

### Where can I go from here?

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


### Changing directory

So now that you know where you are, and you know which directories you can move into, you can use the `cd` command to 'change directory'.

To be specific, type the directory that you want to move into directly after `cd`. For example, I'm going to go into `notes`, so I would type `cd notes`.

Choose one of the directories that you saw when you typed `ls` and use `cd` to move into it.

If you type `ls` again, you can now see what is inside here.

If you want to go back to the previous directory, type `cd ..`. This would take me back to `FAC9`.

#### I just want to go home :cry:

Don't cry! If you just want to head back home, `cd` by itself will take you straight there.
