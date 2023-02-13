+++
title = "d. Exploring Directories"
weight = 2
chapter = true
+++

## Exploring other directories

Not only can we use `ls` on the current working directory, 
but we can use it to list the contents of a different directory.
Let's take a look at our `Desktop` directory by running `ls -F Desktop`,
i.e.,
the command `ls` with the `-F` **option** and the [**argument**][Arguments]  `Desktop`.
The argument `Desktop` tells `ls` that
we want a listing of something other than our current working directory:

```Bash
$ ls -F Desktop
```

~~~
shell-lesson-data/
~~~


Note that if a directory named `Desktop` does not exist in your current working directory,
this command will return an error. Typically, a `Desktop` directory exists in your
home directory, which we assume is the current working directory of your bash shell.

Your output should be a list of all the files and sub-directories in your
Desktop directory, including the `shell-lesson-data` directory you downloaded at
the [setup for this lesson]({{< ref "/0-setup" >}} "setup").
On many systems, the command line Desktop directory is the same as your GUI Desktop.
Take a look at your Desktop to confirm that your output is accurate.

As you may now see, using a bash shell is strongly dependent on the idea that
your files are organized in a hierarchical file system.
Organizing things hierarchically in this way helps us keep track of our work:
it's possible to put hundreds of files in our home directory,
just as it's possible to pile hundreds of printed papers on our desk,
but it's a self-defeating strategy.

Now that we know the `shell-lesson-data` directory is located in our Desktop directory, we
can do two things.

First, we can look at its contents, using the same strategy as before, passing
a directory name to `ls`:

```Bash
$ ls -F Desktop/shell-lesson-data
```

~~~
creatures/          molecules/          notes.txt           solar.pdf
data/               north-pacific-gyre/ pizza.cfg           writing/
~~~


Second, we can actually change our location to a different directory, so
we are no longer located in our home directory.

The command to change locations is `cd` followed by a directory name to 
change our working directory. `cd` stands for 'change directory',
which is a bit misleading: the command doesn't change the directory;
it changes the shell's idea of what directory we are in.
The `cd` command is akin to double clicking a folder in a graphical interface to get into a folder.

Let's say we want to move to the `data` directory we saw above. We can
use the following series of commands to get there:

```Bash
$ cd Desktop
$ cd shell-lesson-data
$ cd data
```

These commands will move us from our home directory into our Desktop directory, then into
the `shell-lesson-data` directory, then into the `data` directory. 
You will notice that `cd` doesn't print anything. This is normal. 
Many shell commands will not output anything to the screen when successfully executed. 
But if we run `pwd` after it, we can see that we are now
in `/Users/nelle/Desktop/shell-lesson-data/data`.
If we run `ls -F` without arguments now,
it lists the contents of `/Users/nelle/Desktop/shell-lesson-data/data`,
because that's where we now are:

```Bash
$ pwd
```

~~~
/Users/nelle/Desktop/shell-lesson-data/data
~~~


```Bash
$ ls -F
```

~~~
amino-acids.txt   elements/     pdb/	        salmon.txt
animals.txt       morse.txt     planets.txt     sunspot.txt
~~~

We now know how to go down the directory tree (i.e. how to go into a subdirectory),
but how do we go up (i.e. how do we leave a directory and go into its parent directory)?
We might try the following:

```Bash
$ cd shell-lesson-data
```

~~~
-bash: cd: shell-lesson-data: No such file or directory
~~~

But we get an error! Why is this?

With our methods so far,
`cd` can only see sub-directories inside your current directory. There are
different ways to see directories above your current location; we'll start
with the simplest.

There is a shortcut in the shell to move up one directory level
that looks like this:

```Bash
$ cd ..
```

`..` is a special directory name meaning
"the directory containing this one",
or more succinctly,
the **parent** of the current directory.
Sure enough,
if we run `pwd` after running `cd ..`, we're back in `/Users/nelle/Desktop/shell-lesson-data`:

```Bash
$ pwd
```

~~~
/Users/nelle/Desktop/shell-lesson-data
~~~


The special directory `..` doesn't usually show up when we run `ls`. If we want
to display it, we can add the `-a` option to `ls -F`:

```Bash
$ ls -F -a
```

~~~
./   .bash_profile  data/       north-pacific-gyre/  pizza.cfg  thesis/
../  creatures/     molecules/  notes.txt            solar.pdf  writing/
~~~


`-a` stands for 'show all';
it forces `ls` to show us file and directory names that begin with `.`,
such as `..` (which, if we're in `/Users/nelle`, refers to the `/Users` directory).
As you can see, it also displays another special directory that's just called `.`,
which means 'the current working directory'.
It may seem redundant to have a name for it, but we'll see some uses for it soon.

{{% notice note %}}
## Command Line Flags

In most command line tools, multiple options can be combined
with a single `-` and no spaces between the options: `ls -F -a` is
equivalent to `ls -Fa`.
This makes writing more complicated commands easy. For example `ls`
with long listing showing all hidden files in human readable format in
reverse order is just:

```Bash
$ ls -larh
```
{{% /notice %}}

{{% notice note %}}
## Other Hidden Files

In addition to the hidden directories `..` and `.`, you may also see a file
called `.bash_profile`. This file usually contains shell configuration
settings. You may also see other files and directories beginning
with `.`. These are usually files and directories that are used to configure
different programs on your computer and are commonly called **dotfiles**.
The prefix `.` is used to prevent these configuration
files from cluttering the terminal when a standard `ls` command
is used.
{{% /notice %}}

These three commands are the basic commands for navigating the filesystem on your computer:
`pwd`, `ls`, and `cd`. Let's explore some variations on those commands. What happens
if you type `cd` on its own, without giving
a directory?

```Bash
$ cd
```

How can you check what happened? `pwd` gives us the answer!

```Bash
$ pwd
```

~~~
/Users/nelle
~~~

It turns out that `cd` without an argument will return you to your home directory,
which is great if you've gotten lost in your own filesystem.

Let's try returning to the `data` directory from before. Last time, we used
three commands, but we can actually string together the list of directories
to move to `data` in one step:

```Bash
$ cd Desktop/shell-lesson-data/data
```

Check that we've moved to the right place by running `pwd` and `ls -F`.

If we want to move up one level from the data directory, we could use `cd ..`.  But
there is another way to move to any directory, regardless of your
current location.

So far, when specifying directory names, or even a directory path (as above),
we have been using **relative paths**.  When you use a relative path with a command
like `ls` or `cd`, it tries to find that location from where we are,
rather than from the root of the file system.

However, it is possible to specify the **absolute path** to a directory by
including its entire path from the root directory, which is indicated by a
leading slash. The leading `/` tells the computer to follow the path from
the root of the file system, so it always refers to exactly one directory,
no matter where we are when we run the command.

This allows us to move to our `shell-lesson-data` directory from anywhere on
the filesystem (including from inside `data`). To find the absolute path
we're looking for, we can use `pwd` and then extract the piece we need
to move to `shell-lesson-data`.

```Bash
$ pwd
```

~~~
/Users/nelle/Desktop/shell-lesson-data/data
~~~

```Bash
$ cd /Users/nelle/Desktop/shell-lesson-data
```

Run `pwd` and `ls -F` to ensure that we're in the directory we expect.

{{% notice note %}}
## Two More Shortcuts

The shell interprets a tilde (`~`) character at the start of a path to
mean "the current user's home directory". For example, if Nelle's home
directory is `/Users/nelle`, then `~/data` is equivalent to
`/Users/nelle/data`. This only works if it is the first character in the
path: `here/there/~/elsewhere` is *not* `here/there/Users/nelle/elsewhere`.

Another shortcut is the `-` (dash) character. `cd` will translate `-` into
*the previous directory I was in*, which is faster than having to remember,
then type, the full path.  This is a *very* efficient way of moving
*back and forth between two directories* -- i.e. if you execute `cd -` twice,
you end up back in the starting directory.

The difference between `cd ..` and `cd -` is
that the former brings you *up*, while the latter brings you *back*.

----
Try it!
First navigate to `~/Desktop/shell-lesson-data` (you should already be there).
```Bash
$ cd ~/Desktop/shell-lesson-data
```

Then `cd` into the `creatures` directory
```Bash
$ cd creatures
```

Now if you run
```Bash
$ cd -
```
you'll see you're back in `~/Desktop/shell-lesson-data`.
Run `cd -` again and you're back in `~/Desktop/shell-lesson-data/creatures`
{{% /notice %}}