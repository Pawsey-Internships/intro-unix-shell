+++
title = "f. Multiple Files and Directories"
weight = 2
chapter = true
+++

## Operations with multiple files and directories

Oftentimes one needs to copy or move several files at once.
This can be done by providing a list of individual filenames,
or specifying a naming pattern using wildcards.

## Exercise: Copy with Multiple Filenames

For this exercise, you can test the commands in the `shell-lesson-data/data` directory.

In the example below, what does `cp` do when given several filenames and a directory name?

```Bash
$ mkdir backup
$ cp amino-acids.txt animals.txt backup/
```

In the example below, what does `cp` do when given three or more file names?

```Bash
$ ls -F
```

~~~
amino-acids.txt  animals.txt  backup/  elements/  morse.txt  pdb/
planets.txt  salmon.txt  sunspot.txt
~~~


```Bash
$ cp amino-acids.txt animals.txt morse.txt
```

{{% expand "Solution" %}}
If given more than one file name followed by a directory name
(i.e. the destination directory must be the last argument),
`cp` copies the files to the named directory.

If given three file names, `cp` throws an error such as the one below,
because it is expecting a directory name as the last argument.

```
cp: target ‘morse.txt’ is not a directory
```
{{% /expand %}}

## Using wildcards for accessing multiple files at once

#### Wildcards

`*` is a **wildcard**, which matches zero or more  characters.
Let's consider the `shell-lesson-data/molecules` directory:
`*.pdb` matches `ethane.pdb`, `propane.pdb`, and every
file that ends with '.pdb'. On the other hand, `p*.pdb` only matches
`pentane.pdb` and `propane.pdb`, because the 'p' at the front only
matches filenames that begin with the letter 'p'.

`?` is also a wildcard, but it matches exactly one character.
So `?ethane.pdb` would match `methane.pdb` whereas
`*ethane.pdb` matches both `ethane.pdb`, and `methane.pdb`.

Wildcards can be used in combination with each other
e.g. `???ane.pdb` matches three characters followed by `ane.pdb`,
giving `cubane.pdb  ethane.pdb  octane.pdb`.

When the shell sees a wildcard, it expands the wildcard to create a
list of matching filenames *before* running the command that was
asked for. As an exception, if a wildcard expression does not match
any file, Bash will pass the expression as an argument to the command
as it is.
{: .callout}

## Exercise: List filenames matching a pattern

When run in the `molecules` directory, which `ls` command(s) will
produce this output?

`ethane.pdb   methane.pdb`

1. `ls *t*ane.pdb`
2. `ls *t?ne.*`
3. `ls *t??ne.pdb`
4. `ls ethane.*`

{{% expand "Solution" %}}
 The solution is **3.**

1. shows all files whose names contain zero or more characters (`*`)
followed by the letter `t`,
then zero or more characters (`*`) followed by `ane.pdb`.
This gives `ethane.pdb  methane.pdb  octane.pdb  pentane.pdb`.
>
2. shows all files whose names start with zero or more characters (`*`) followed by
the letter `t`,
then a single character (`?`), then `ne.` followed by zero or more characters (`*`).
This will give us `octane.pdb` and `pentane.pdb` but doesn't match anything
which ends in `thane.pdb`.
>
3. fixes the problems of option 2 by matching two characters (`??`) between `t` and `ne`.
This is the solution.
>
4. only shows files starting with `ethane.`.
{{%/expand %}}

## Exercise: Organizing Directories and Files

Jamie is working on a project and she sees that her files aren't very well
organized:

```Bash
$ ls -F
```

~~~
analyzed/  fructose.dat    raw/   sucrose.dat
~~~


The `fructose.dat` and `sucrose.dat` files contain output from her data
analysis. What command(s) covered in this lesson does she need to run
so that the commands below will produce the output shown?

```Bash
$ ls -F
```

~~~
analyzed/   raw/
~~~

```Bash
$ ls analyzed
```

~~~
fructose.dat    sucrose.dat
~~~


{{% expand "Solution" %}}
```
mv *.dat analyzed
```
{: .language-bash}
Jamie needs to move her files `fructose.dat` and `sucrose.dat` to the `analyzed` directory.
The shell will expand *.dat to match all .dat files in the current directory.
The `mv` command then moves the list of .dat files to the 'analyzed' directory.
{{% /expand %}}

## Exercise: Reproduce a folder structure

You're starting a new experiment and would like to duplicate the directory
structure from your previous experiment so you can add new data.

Assume that the previous experiment is in a folder called '2016-05-18',
which contains a `data` folder that in turn contains folders named `raw` and
`processed` that contain data files.  The goal is to copy the folder structure
of the `2016-05-18-data` folder into a folder called `2016-05-20`
so that your final directory structure looks like this:

~~~
2016-05-20/
└── data
   ├── processed
   └── raw
~~~

Which of the following set of commands would achieve this objective?
What would the other commands do?

```Bash
$ mkdir 2016-05-20
$ mkdir 2016-05-20/data
$ mkdir 2016-05-20/data/processed
$ mkdir 2016-05-20/data/raw
```

```Bash
$ mkdir 2016-05-20
$ cd 2016-05-20
$ mkdir data
$ cd data
$ mkdir raw processed
```

```Bash
$ mkdir 2016-05-20/data/raw
$ mkdir 2016-05-20/data/processed
```

```Bash
$ mkdir -p 2016-05-20/data/raw
$ mkdir -p 2016-05-20/data/processed
```

```Bash
$ mkdir 2016-05-20
$ cd 2016-05-20
$ mkdir data
$ mkdir raw processed
```

{{% expand "Solution" %}}
The first two sets of commands achieve this objective.
The first set uses relative paths to create the top-level directory before
the subdirectories.

The third set of commands will give an error because the default behavior of `mkdir`
won't create a subdirectory of a non-existent directory:
the intermediate level folders must be created first.

The fourth set of commands achieve this objective. Remember, the `-p` option,
followed by a path of one or more
directories, will cause `mkdir` to create any intermediate subdirectories as required.

The final set of commands generates the 'raw' and 'processed' directories at the same level
as the 'data' directory.
{{% /expand %}}

{{% notice note%}}
## Creating Multiple Directories at once
Bash also supports brace expansion whereby multiple paths can be
created with a single expression.
For example to reproduce the folder structure only a single command is needed:
```Bash
$ mkdir -p 2016-05-20/data/{raw, processed}
```

As bash expands it to:
```Bash
$ mkdir -p 2016-05-20/data/raw 2016-05-20/data/processed
```

This can be useful when creating nested file structures or when creating multiple
directories quickly.
{{%/notice %}}

