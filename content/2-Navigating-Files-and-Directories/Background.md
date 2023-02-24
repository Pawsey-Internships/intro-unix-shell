+++
title = "a. Background"
weight = 2
chapter = false
+++

The part of the operating system responsible for managing files and directories
is called the **file system**. It organizes our data into files,
which hold information, and directories (also called 'folders'),
which hold files or other directories.

Several commands are frequently used to create, inspect, rename, and delete files and directories.
To start exploring them, we'll go to our open shell window.

First, let's find out where we are by running a command called `pwd`
(which stands for 'print working directory'). Directories are like *places* — at any time
while we are using the shell, we are in exactly one place called
our **current working directory**. Commands mostly read and write files in the
current working directory, i.e. 'here', so knowing where you are before running
a command is important. `pwd` shows you where you are:

```Bash
$ pwd
```

~~~
/Users/nelle
~~~


Here,the computer's response is `/Users/nelle`,
which is Nelle's **home directory**:

{{% notice note %}}
## Home Directory Variation

The home directory path will look different on different operating systems.
On Linux, it may look like `/home/nelle`,
and on Windows, it will be similar to `C:\Documents and Settings\nelle` or
`C:\Users\nelle`.
(Note that it may look slightly different for different versions of Windows.)
In future examples, we've used Mac output as the default - Linux and Windows
output may differ slightly but should be generally similar.

We will also assume that your `pwd` command returns your user's home directory.
If `pwd` returns something different, you may need to navigate there using `cd`
or some commands in this lesson will not work as written.
See [Exploring Other Directories CHECK LINK](#exploring-other-directories) for more details
on the `cd` command.
{{% /notice %}}

To understand what a 'home directory' is,
let's have a look at how the file system as a whole is organized.  For the
sake of this example, we'll be
illustrating the filesystem on our scientist Nelle's computer.  After this
illustration, you'll be learning commands to explore your own filesystem,
which will be constructed in a similar way, but not be exactly identical.

On Nelle's computer, the filesystem looks like this:

![The file system is made up of a root directory that contains sub-directories
titled bin, data, users, and tmp](images/filesystem.svg "The file system is made 
up of a root directory that contains sub-directories titled bin, data, users, and tmp")

At the top is the **root directory** that holds everything else.
We refer to it using a slash character, `/`, on its own;
this character is the leading slash in `/Users/nelle`.

Inside that directory are several other directories:
- `bin` (which is where some built-in programs are stored),
- `data` (for miscellaneous data files),
- `Users` (where users' personal directories are located),
- `tmp` (for temporary files that don't need to be stored long-term),
and so on.

We know that our current working directory `/Users/nelle` is stored inside `/Users`
because `/Users` is the first part of its name.
Similarly,
we know that `/Users` is stored inside the root directory `/`
because its name begins with `/`.

{{% notice note %}}
## Slashes

Notice that there are two meanings for the `/` character.
When it appears at the front of a file or directory name,
it refers to the root directory. When it appears *inside* a path,
it's just a separator.
{{% /notice %}}

Typically, when you open a new command prompt, you will be in
your home directory to start. Because Nelle is the user in our
examples here, therefore we get `/Users/nelle` as our home directory.

{{% notice note %}}
## Clearing your terminal

If your screen gets too cluttered, you can clear your terminal using the
`clear` command. You can still access previous commands using <kbd>↑</kbd>
and <kbd>↓</kbd> to move line-by-line, or by scrolling in your terminal.
{{% /notice %}}