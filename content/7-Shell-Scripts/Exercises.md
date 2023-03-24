+++
title = "e. Exercises I"
weight = 2
chapter = false
+++


What if we want to process many files in a single pipeline?
For example, if we want to sort our `.pdb` files by length, we would type:

```Bash
$ wc -l *.pdb | sort -n
```

because `wc -l` lists the number of lines in the files
(recall that `wc` stands for 'word count', adding the `-l` option means 'count lines' instead)
and `sort -n` sorts things numerically. We could put this in a file,
but then it would only ever sort a list of `.pdb` files in the current directory.
If we want to be able to get a sorted list of other kinds of files,
we need a way to get all those names into the script. We can't use `$1`, `$2`, and so on
because we don't know how many files there are.Instead, we use the special variable `$@`,
which means, 'All of the command-line arguments to the shell script'.
We also should put `$@` inside double-quotes to handle the case of arguments containing spaces
(`"$@"` is special syntax and is equivalent to `"$1"` `"$2"` ...).

Here's an example:

```Bash
$ nano sorted.sh
```

```
# Sort files by their length.
# Usage: bash sorted.sh one_or_more_filenames
wc -l "$@" | sort -n
```

```Bash
$ bash sorted.sh *.pdb ../creatures/*.dat
```

~~~
9 methane.pdb
12 ethane.pdb
15 propane.pdb
20 cubane.pdb
21 pentane.pdb
30 octane.pdb
163 ../creatures/basilisk.dat
163 ../creatures/minotaur.dat
163 ../creatures/unicorn.dat
596 total
~~~

#### List Unique Species

Leah has several hundred data files, each of which is formatted like this:

~~~
2013-11-05,deer,5
2013-11-05,rabbit,22
2013-11-05,raccoon,7
2013-11-06,rabbit,19
2013-11-06,deer,2
2013-11-06,fox,1
2013-11-07,rabbit,18
2013-11-07,bear,1
~~~

An example of this type of file is given in `shell-lesson-data/data/animal-counts/animals.txt`.

We can use the command `cut -d , -f 2 animals.txt | sort | uniq` to produce
the unique species in `animals.txt`.
In order to avoid having to type out this series of commands every time,
a scientist may choose to write a shell script instead.

Write a shell script called `species.sh` that takes any number of
filenames as command-line arguments, and uses a variation of the above command
to print a list of the unique species appearing in each of those files separately.

{{% expand "Solution" %}}

```Bash
# Script to find unique species in csv files where species is the second data field
# This script accepts any number of file names as command line arguments

# Loop over all files
for file in $@
do
echo "Unique species in $file:"
# Extract species names
cut -d , -f 2 $file | sort | uniq
done
```
{{% /expand %}}


Suppose we have just run a series of commands that did something useful --- for example,
that created a graph we'd like to use in a paper. We'd like to be able to re-create the graph later if we need to, so we want to save the commands in a file. Instead of typing them in again
(and potentially getting them wrong) we can do this:

```Bash
$ history | tail -n 5  redo-figure-3.sh
```

The file `redo-figure-3.sh` now contains:

~~~
297 bash goostats.sh NENE01729B.txt stats-NENE01729B.txt
298 bash goodiff.sh stats-NENE01729B.txt /data/validated/01729.txt > 01729-differences.txt
299 cut -d ',' -f 2-3 01729-differences.txt > 01729-time-series.txt
300 ygraph --format scatter --color bw --borders none 01729-time-series.txt figure-3.png
301 history | tail -n 5 > redo-figure-3.sh
~~~

After a moment's work in an editor to remove the serial numbers on the commands,
and to remove the final line where we called the `history` command,
we have a completely accurate record of how we created that figure.

#### Why Record Commands in the History Before Running Them?

If you run the command:

```Bash
$ history | tail -n 5 > recent.sh
```

the last command in the file is the `history` command itself, i.e.,
the shell has added `history` to the command log before actually
running it. In fact, the shell *always* adds commands to the log
before running them. Why do you think it does this?

{{% expand "Solution" %}}
If a command causes something to crash or hang, it might be useful
to know what that command was, in order to investigate the problem.
Were the command only be recorded after running it, we would not
have a record of the last command run in the event of a crash.
{{% /expand %}}

In practice, most people develop shell scripts by running commands at the shell prompt a few times
to make sure they're doing the right thing, then saving them in a file for re-use. This style of work allows people to recycle what they discover about their data and their workflow with one call to `history` and a bit of editing to clean up the output and save it as a shell script.