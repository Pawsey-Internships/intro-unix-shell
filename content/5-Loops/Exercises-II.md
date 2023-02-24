+++
title = "i. Exercises II"
weight = 2
chapter = false
+++


## Doing a Dry Run

A loop is a way to do many things at once --- or to make many mistakes at
once if it does the wrong thing. One way to check what a loop *would* do
is to `echo` the commands it would run instead of actually running them.

Suppose we want to preview the commands the following loop will execute
without actually running those commands:

```Bash
$ for datafile in *.pdb
do
    cat $datafile >> all.pdb
done
```

What is the difference between the two loops below, and which one would we
want to run?

```Bash
# Version 1
$ for datafile in *.pdb
do
    echo cat $datafile >> all.pdb
done
```

```Bash
# Version 2
$ for datafile in *.pdb
do
    echo "cat $datafile >> all.pdb"
done
```
{{% expand "Solution" %}}
The second version is the one we want to run.
This prints to screen everything enclosed in the quote marks, expanding the
loop variable name because we have prefixed it with a dollar sign.
It also *does not* modify nor create the file `all.pdb`, as the `>>`
is treated literally as part of a string rather than as a
redirection instruction.

The first version appends the output from the command `echo cat $datafile`
to the file, `all.pdb`. This file will just contain the list;
`cat cubane.pdb`, `cat ethane.pdb`, `cat methane.pdb` etc.

Try both versions for yourself to see the output! Be sure to open the
`all.pdb` file to view its contents.
{{% /expand %}}

## Nested Loops

Suppose we want to set up a directory structure to organize
some experiments measuring reaction rate constants with different compounds
*and* different temperatures.  What would be the
result of the following code:

```Bash
$ for species in cubane ethane methane
do
    for temperature in 25 30 37 40
    do
        mkdir $species-$temperature
    done
done
```

{{% expand "Solution" %}}
We have a nested loop, i.e. contained within another loop, so for each species
in the outer loop, the inner loop (the nested loop) iterates over the list of
temperatures, and creates a new directory for each combination.

Try running the code for yourself to see which directories are created!
{{% /expand %}}

