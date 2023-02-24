+++
title = "c. Exercises I"
weight = 2
chapter = false
+++

## Variables in Loops

This exercise refers to the `shell-lesson-data/molecules` directory.
`ls` gives the following output:

~~~
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
~~~

What is the output of the following code?

```Bash
$ for datafile in *.pdb
do
	ls *.pdb
done
```

Now, what is the output of the following code?

```Bash
$ for datafile in *.pdb
do
ls $datafile
done
```

Why do these two loops give different outputs?

{{% expand "Solution" %}}
The first code block gives the same output on each iteration through
the loop. Bash expands the wildcard `*.pdb` within the loop body (as well as
before the loop starts) to match all files ending in `.pdb`
and then lists them using `ls`. The expanded loop would look like this:

```Bash
$ for datafile in cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
do
	ls cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
done
```


```
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
```


The second code block lists a different file on each loop iteration.
The value of the `datafile` variable is evaluated using `$datafile`,
and then listed using `ls`.

```
cubane.pdb
ethane.pdb
methane.pdb
octane.pdb
pentane.pdb
propane.pdb
```
{{% /expand %}}

## Limiting Sets of Files

What would be the output of running the following loop in the
`shell-lesson-data/molecules` directory?

```Bash
$ for filename in c*
do
	ls $filename
done
```

1.  No files are listed.
2.  All files are listed.
3.  Only `cubane.pdb`, `octane.pdb` and `pentane.pdb` are listed.
4.  Only `cubane.pdb` is listed.

{{% expand "Solution" %}}
4 is the correct answer. `*` matches zero or more characters, so any file name starting with
the letter c, followed by zero or more other characters will be matched.
{{% /expand %}}

How would the output differ from using this command instead?

```Bash
$ for filename in *c*
do
	ls $filename
done
```

1.  The same files would be listed.
2.  All the files are listed this time.
3.  No files are listed this time.
4.  The files `cubane.pdb` and `octane.pdb` will be listed.
5.  Only the file `octane.pdb` will be listed.

{{% expand "Solution" %}}
4 is the correct answer. `*` matches zero or more characters, so a file name with zero or more
characters before a letter c and zero or more characters after the letter c will be matched.
{{% /expand %}}