+++
title = "f. Command Syntax"
weight = 2
chapter = false
+++

We have now encountered commands, options, and arguments,
but it is perhaps useful to formalise some terminology.

Consider the command below as a general example of a command,
which we will dissect into its component parts:

```Bash
$ ls -F /
```

![General syntax of a shell command](images/shell_command_syntax.svg)

`ls` is the **command**, with an **option** `-F` and an
**argument** `/`.
We've already encountered options (also called **switches** or **flags**) which
either start with a single dash (`-`) or two dashes (`--`), 
and they change the behavior of a command.
[Arguments] tell the command what to operate on (e.g. files and directories).
Sometimes options and arguments are referred to as **parameters**.
A command can be called with more than one option and more than one argument, but a
command doesn't always require an argument or an option.

Each part is separated by spaces: if you omit the space
between `ls` and `-F` the shell will look for a command called `ls-F`, which
doesn't exist. Also, capitalization can be important.
For example, `ls -s` will display the size of files and directories alongside the names,
while `ls -S` will sort the files and directories by size, as shown below:

```Bash
$ ls -s Desktop/shell-lesson-data/data
total 116
 4 amino-acids.txt   4 animals.txt   4 morse.txt  12 planets.txt  76 sunspot.txt
 4 animal-counts     4 elements      4 pdb         4 salmon.txt
$ ls -S Desktop/shell-lesson-data/data
sunspot.txt  animal-counts  pdb        amino-acids.txt  salmon.txt
planets.txt  elements       morse.txt  animals.txt
```

Putting all that together, our command above gives us a listing
of files and directories in the root directory `/`.
An example of the output you might get from the above command is given below:

```Bash
$ ls -F /
```

~~~
Applications/         System/
Library/              Users/
Network/              Volumes/
~~~


