+++
title = "b. Creating Files"
weight = 2
chapter = false
+++

### Create a text file
Let's change our working directory to `thesis` using `cd`,
then run a text editor called Nano to create a file called `draft.txt`:

```Bash
$ cd thesis
$ nano draft.txt
```

{{% notice note %}}
## Which Editor?

When we say, '`nano` is a text editor' we really do mean 'text': it can
only work with plain character data, not tables, images, or any other
human-friendly media. We use it in examples because it is one of the
least complex text editors. However, because of this trait, it may
not be powerful enough or flexible enough for the work you need to do
after this workshop. On Unix systems (such as Linux and macOS),
many programmers use [Emacs](http://www.gnu.org/software/emacs/) or
[Vim](http://www.vim.org/) (both of which require more time to learn),
or a graphical editor such as
[Gedit](http://projects.gnome.org/gedit/). On Windows, you may wish to
use [Notepad++](http://notepad-plus-plus.org/).  Windows also has a built-in
editor called `notepad` that can be run from the command line in the same
way as `nano` for the purposes of this lesson.

No matter what editor you use, you will need to know where it searches
for and saves files. If you start it from the shell, it will (probably)
use your current working directory as its default location. If you use
your computer's start menu, it may want to save files in your desktop or
documents directory instead. You can change this by navigating to
another directory the first time you 'Save As...'
{{% /notice %}}

Let's type in a few lines of text.
Once we're happy with our text, we can press <kbd>Ctrl</kbd>+<kbd>O</kbd>
(press the <kbd>Ctrl</kbd> or <kbd>Control</kbd> key and, while
holding it down, press the <kbd>O</kbd> key) to write our data to disk
(we'll be asked what file we want to save this to:
press <kbd>Return</kbd> to accept the suggested default of `draft.txt`).

![screenshot of nano text editor in action"](images/nano-screenshot.png)


Once our file is saved, we can use <kbd>Ctrl</kbd>+<kbd>X</kbd> to quit the editor and
return to the shell.

`nano` doesn't leave any output on the screen after it exits,
but `ls` now shows that we have created a file called `draft.txt`:

```Bash
$ ls
```

~~~
draft.txt
~~~

## Exercise: Creating Files a Different Way

We have seen how to create text files using the `nano` editor.
Now, try the following command:

```Bash
$ touch my_file.txt
```

1.  What did the `touch` command do?
    When you look at your current directory using the GUI file explorer,
    does the file show up?
2.  Use `ls -l` to inspect the files.  How large is `my_file.txt`?
3.  When might you want to create a file this way?

{{%expand "Solution" %}}
1.  The `touch` command generates a new file called `my_file.txt` in
    your current directory.  You
    can observe this newly generated file by typing `ls` at the
    command line prompt.  `my_file.txt` can also be viewed in your
    GUI file explorer.
>
2.  When you inspect the file with `ls -l`, note that the size of
    `my_file.txt` is 0 bytes.  In other words, it contains no data.
    If you open `my_file.txt` using your text editor it is blank.
>
3.  Some programs do not generate output files themselves, but
    instead require that empty files have already been generated.
    When the program is run, it searches for an existing file to
    populate with its output.  The touch command allows you to
    efficiently generate a blank text file to be used by such
    programs.
{{% /expand%}}

{{% notice note %}}
## What's In A Name?

You may have noticed that all of Nelle's files are named 'something dot
something', and in this part of the lesson, we always used the extension
`.txt`.  This is just a convention: we can call a file `mythesis` or
almost anything else we want. However, most people use two-part names
most of the time to help them (and their programs) tell different kinds
of files apart. The second part of such a name is called the
**filename extension** and indicates
what type of data the file holds: `.txt` signals a plain text file, `.pdf`
indicates a PDF document, `.cfg` is a configuration file full of parameters
for some program or other, `.png` is a PNG image, and so on.

This is just a convention, albeit an important one. Files contain
bytes: it's up to us and our programs to interpret those bytes
according to the rules for plain text files, PDF documents, configuration
files, images, and so on.

Naming a PNG image of a whale as `whale.mp3` doesn't somehow
magically turn it into a recording of whale song, though it *might*
cause the operating system to try to open it with a music player
when someone double-clicks it.
{{% /notice %}}