+++
title = "a. Creating Directories"
weight = 2
chapter = true
+++

## Creating directories
We now know how to explore files and directories,
but how do we create them in the first place?

### Step one: see where we are and what we already have
Let's go back to our `shell-lesson-data` directory on the Desktop
and use `ls -F` to see what it contains:

```Bash
$ pwd
```

~~~
/Users/nelle/Desktop/shell-lesson-data
~~~

```Bash
$ ls -F
```

~~~
creatures/  data/  molecules/  north-pacific-gyre/  notes.txt  pizza.cfg  solar.pdf  writing/
~~~

### Create a directory

Let's create a new directory called `thesis` using the command `mkdir thesis`
(which has no output):

```Bash
$ mkdir thesis
```

As you might guess from its name, `mkdir` means 'make directory'.
Since `thesis` is a relative path (i.e., does not have a leading 
slash, like `/what/ever/thesis`), the new directory is created in 
the current working directory:

```Bash
$ ls -F
```

~~~
creatures/  data/  molecules/  north-pacific-gyre/  notes.txt  pizza.cfg
solar.pdf  thesis/  writing/
~~~

Since we've just created the `thesis` directory, there's nothing in it yet:

```Bash
$ ls -F thesis
```

Note that `mkdir` is not limited to creating single directories one at a time.
The `-p` option allows `mkdir` to create a directory with nested subdirectories
in a single operation:

```Bash
$ mkdir -p project/data project/results
```
{{% notice note %}}
## Two ways of doing the same thing
Using the shell to create a directory is no different than using a file explorer.
If you open the current directory using your operating system's graphical file explorer,
the `thesis` directory will appear there too.
While the shell and the file explorer are two different ways of interacting with the files,
the files and directories themselves are the same.

{{% /notice %}}

{{% notice note %}}
## Good names for files and directories

Complicated names of files and directories can make your life painful
when working on the command line. Here we provide a few useful
tips for the names of your files and directories.

1. Don't use spaces.
	Spaces can make a name more meaningful,
	but since spaces are used to separate arguments on the command line
	it is better to avoid them in names of files and directories.
	You can use `-` or `_` instead (e.g. `north-pacific-gyre/` rather than `north pacific gyre/`).
	To test this out, try typing `mkdir north pacific gyre`and see what directory (or directories!)
	are made when you check with `ls -F`.

2. Don't begin the name with `-` (dash).
	Commands treat names starting with `-` as options.

3. Stick with letters, numbers, `.` (period or 'full stop'), `-` (dash) and `_` (underscore).

 If you need to refer to names of files or directories that have spaces
 or other special characters, you should surround the name in quotes (`""`).

{{% /notice %}}