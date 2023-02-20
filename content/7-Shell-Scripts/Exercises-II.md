+++
title = "g. Exercises II"
weight = 2
chapter = true
+++

## Exercises II

#### Variables in Shell Scripts

In the `molecules` directory, imagine you have a shell script called `script.sh` containing the
following commands:

```Bash
head -n $2 $1
tail -n $3 $1
```

While you are in the `molecules` directory, you type the following command:

```Bash
bash script.sh '*.pdb' 1 1
```

Which of the following outputs would you expect to see?

1. All of the lines between the first and the last lines of each file ending in `.pdb`
in the `molecules` directory
2. The first and the last line of each file ending in `.pdb` in the `molecules` directory
3. The first and the last line of each file in the `molecules` directory
4. An error because of the quotes around `*.pdb`

{{% expand "Solution" %}}
The correct answer is 2.

The special variables $1, $2 and $3 represent the command line arguments given to the
script, such that the commands run are:

```Bash
$ head -n 1 cubane.pdb ethane.pdb octane.pdb pentane.pdb propane.pdb
$ tail -n 1 cubane.pdb ethane.pdb octane.pdb pentane.pdb propane.pdb
```

The shell does not expand `'*.pdb'` because it is enclosed by quote marks.
As such, the first argument to the script is `'*.pdb'` which gets expanded within the
script by `head` and `tail`.
{{% /expand %}}

#### Find the Longest File With a Given Extension

Write a shell script called `longest.sh` that takes the name of a
directory and a filename extension as its arguments, and prints
out the name of the file with the most lines in that directory
with that extension. For example:

```Bash
$ bash longest.sh shell-lesson-data/exercise-data/proteins pdb
```

would print the name of the `.pdb` file in `shell-lesson-data/exercise-data/proteins` that has
the most lines.

Feel free to test your script on another directory e.g.
```Bash
$ bash longest.sh shell-lesson-data/exercise-data/writing txt
```

{{% expand "Solution" %}}

```Bash
# Shell script which takes two arguments:
#    1. a directory name
#    2. a file extension
# and prints the name of the file in that directory
# with the most lines which matches the file extension.

wc -l $1/*.$2 | sort -n | tail -n 2 | head -n 1
```

The first part of the pipeline, `wc -l $1/*.$2 | sort -n`, counts
the lines in each file and sorts them numerically (largest last). When
there's more than one file, `wc` also outputs a final summary line,
giving the total number of lines across _all_ files.  We use `tail
-n 2 | head -n 1` to throw away this last line.

With `wc -l $1/*.$2 | sort -n | tail -n 1` we'll see the final summary
line: we can build our pipeline up in pieces to be sure we understand
the output.

{{% /expand %}}

#### Script Reading Comprehension

For this question, consider the `shell-lesson-data/molecules` directory once again.
This contains a number of `.pdb` files in addition to any other files you
may have created.
Explain what each of the following three scripts would do when run as
`bash script1.sh *.pdb`, `bash script2.sh *.pdb`, and `bash script3.sh *.pdb` respectively.

```Bash
# Script 1
echo *.*
```

```Bash
# Script 2
for filename in $1 $2 $3
do
	cat $filename
done
```

```Bash
# Script 3
echo $@.pdb
```

{{% expand "Solution" %}}
In each case, the shell expands the wildcard in `*.pdb` before passing the resulting
list of file names as arguments to the script.

Script 1 would print out a list of all files containing a dot in their name.
The arguments passed to the script are not actually used anywhere in the script.

Script 2 would print the contents of the first 3 files with a `.pdb` file extension.
`$1`, `$2`, and `$3` refer to the first, second, and third argument respectively.

Script 3 would print all the arguments to the script (i.e. all the `.pdb` files),
followed by `.pdb`.
`$@` refers to *all* the arguments given to a shell script.
```
cubane.pdb ethane.pdb methane.pdb octane.pdb pentane.pdb propane.pdb.pdb
```
{{% /expand %}}

#### Debugging Scripts

Suppose you have saved the following script in a file called `do-errors.sh`
in Nelle's `north-pacific-gyre/2012-07-03` directory:

```Bash
# Calculate stats for data files.
for datafile in "$@"
do
	echo $datfile
	bash goostats.sh $datafile stats-$datafile
done
```

When you run it:

```Bash
$ bash do-errors.sh NENE*A.txt NENE*B.txt
```

the output is blank.
To figure out why, re-run the script using the `-x` option:

```Bash
bash -x do-errors.sh NENE*A.txt NENE*B.txt
```

What is the output showing you?
Which line is responsible for the error?

{{% expand "Solution" %}}
The `-x` option causes `bash` to run in debug mode.
This prints out each command as it is run, which will help you to locate errors.
In this example, we can see that `echo` isn't printing anything. We have made a typo
in the loop variable name, and the variable `datfile` doesn't exist, hence returning
an empty string.
{{% /expand %}}

