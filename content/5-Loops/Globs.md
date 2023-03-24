+++
title = "d. Globs"
weight = 2
chapter = false
+++


## The advantages of globs
Glob expansion with characters like `*` is fast and efficient. Do not be tempted to use `ls`
to work out what file paths to loop over. It is slow and inefficient.

```Bash
for file in $(ls input_files/*.txt); do
   ...
done
```

## Exercise: Saving to a File in a Loop - Part One

In the `shell-lesson-data/molecules` directory, what is the effect of this loop?

```Bash
for alkanes in *.pdb
do
    echo $alkanes
    cat $alkanes > alkanes.pdb
done
```

1.  Prints `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb` and
   `propane.pdb`, and the text from `propane.pdb` will be saved to a file called `alkanes.pdb`.
2.  Prints `cubane.pdb`, `ethane.pdb`, and `methane.pdb`, and the text from all three files
    would be concatenated and saved to a file called `alkanes.pdb`.
3.  Prints `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, and `pentane.pdb`,
    and the text from `propane.pdb` will be saved to a file called `alkanes.pdb`.
4.  None of the above.

{{% expand "Solution" %}}
1. The text from each file in turn gets written to the `alkanes.pdb` file.
However, the file gets overwritten on each loop iteration, so the final content of `alkanes.pdb`
is the text from the `propane.pdb` file.
{{% /expand %}}

## Exercise: Saving to a File in a Loop - Part Two

Also in the `shell-lesson-data/molecules` directory,
what would be the output of the following loop?

```Bash
for datafile in *.pdb
do
    cat $datafile >> all.pdb
done
```

1.  All of the text from `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, and
    `pentane.pdb` would be concatenated and saved to a file called `all.pdb`.
2.  The text from `ethane.pdb` will be saved to a file called `all.pdb`.
3.  All of the text from `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb`
    and `propane.pdb` would be concatenated and saved to a file called `all.pdb`.
4.  All of the text from `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb`
    and `propane.pdb` would be printed to the screen and saved to a file called `all.pdb`.

{{% expand "Solution" %}}
3 is the correct answer. `>>` appends to a file, rather than overwriting it with the redirected
output from a command.
Given the output from the `cat` command has been redirected, nothing is printed to the screen.
{{% /expand %}}

Let's continue with our example in the `shell-lesson-data/creatures` directory.
Here's a slightly more complicated loop:

```Bash
$ for filename in *.dat
do
    echo $filename
    head -n 100 $filename | tail -n 20
done
```

The shell starts by expanding `*.dat` to create the list of files it will process.
The **loop body** then executes two commands for each of those files.
The first command, `echo`, prints its command-line arguments to standard output.
For example:

```Bash
$ echo hello there
```

prints:

~~~
hello there
~~~

In this case,
since the shell expands `$filename` to be the name of a file,
`echo $filename` prints the name of the file.
Note that we can't write this as:

```Bash
$ for filename in *.dat
do
    $filename
    head -n 100 $filename | tail -n 20
done
```

because then the first time through the loop, when `$filename` expanded to
`basilisk.dat`, the shell would try to run `basilisk.dat` as a program.
Finally, the `head` and `tail` combination selects lines 81-100 from whatever 
file is being processed (assuming the file has at least 100 lines).