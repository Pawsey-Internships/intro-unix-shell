+++
title = "c. Filtering Output"
weight = 2
chapter = false
+++

Next we'll use the `sort` command to sort the contents of the `lengths.txt` file.
But first we'll use an exercise to learn a little about the sort command:

## Exercise: What Does `sort -n` Do?

The file [`shell-lesson-data/numbers.txt`](../shell-lesson-data/numbers.txt)
contains the following lines:

~~~
10
2
19
22
6
~~~

If we run `sort` on this file, the output is:

~~~
10
19
2
22
6
~~~


If we run `sort -n` on the same file, we get this instead:

~~~
2
6
10
19
22
~~~


Explain why `-n` has this effect.

{{% expand "Solution" %}}
 The `-n` option specifies a numerical rather than an alphanumerical sort.
{{% /expand %}}

We will also use the `-n` option to specify that the sort is
numerical instead of alphanumerical.
This does *not* change the file;
instead, it sends the sorted result to the screen:

```Bash
$ sort -n lengths.txt
```

~~~
  9  methane.pdb
 12  ethane.pdb
 15  propane.pdb
 20  cubane.pdb
 21  pentane.pdb
 30  octane.pdb
107  total
~~~


We can put the sorted list of lines in another temporary file called `sorted-lengths.txt`
by putting `> sorted-lengths.txt` after the command,
just as we used `> lengths.txt` to put the output of `wc` into `lengths.txt`.
Once we've done that,
we can run another command called `head` to get the first few lines in `sorted-lengths.txt`:

```Bash
$ sort -n lengths.txt > sorted-lengths.txt
$ head -n 1 sorted-lengths.txt
```

~~~
  9  methane.pdb
~~~

Using `-n 1` with `head` tells it that we only want the first line of the file;
`-n 20` would get the first 20,and so on. Since `sorted-lengths.txt` contains the
lengths of our files ordered from least to greatest, the output of `head` must be 
the file with the fewest lines.

{{% notice note %}}
#### Redirecting to the same file = Bad

It's a very bad idea to try redirecting
the output of a command that operates on a file
to the same file. For example:

```Bash
$ sort -n lengths.txt > lengths.txt
```

Doing something like this may give you incorrect results and/or delete the contents
 of `lengths.txt`.
{{% /notice %}}

## Exercise: What Does `>>` Mean? (Hint: It means "append")

We have seen the use of `>`, but there is a similar operator `>>` 
which works slightly differently.
We'll learn about the differences between these two operators by printing some strings.
We can use the `echo` command to print strings e.g.

```Bash
$ echo The echo command prints text
```

~~~
The echo command prints text
~~~

Now test the commands below to reveal the difference between the two operators:

```Bash
$ echo hello > testfile01.txt
```

and:

```Bash
$ echo hello >> testfile02.txt
```

Hint: Try executing each command twice in a row and then examining the output files.

{{% expand "Solution" %}}
In the first example with `>`, the string 'hello' is written to `testfile01.txt`,
but the file gets overwritten each time we run the command.

We see from the second example that the `>>` operator also writes 'hello' to a file
(in this case`testfile02.txt`),
but appends the string to the file if it already exists 
(i.e. when we run it for the second time).
{{% /expand %}}

## Exercise: Appending Data

We have already met the `head` command, which prints lines from the start of a file.
`tail` is similar, but prints lines from the end of a file instead.

Consider the file `shell-lesson-data/data/animals.txt`.
After these commands, select the answer that
corresponds to the file `animals-subset.txt`:

```Bash
$ head -n 3 animals.txt > animals-subset.txt
$ tail -n 2 animals.txt >> animals-subset.txt
```

1. The first three lines of `animals.txt`
2. The last two lines of `animals.txt`
3. The first three lines and the last two lines of `animals.txt`
4. The second and third lines of `animals.txt`

{{% expand "Solution" %}}
**Option 3 is correct.**
For option 1 to be correct we would only run the `head` command.
For option 2 to be correct we would only run the `tail` command.
For option 4 to be correct we would have to pipe the output of `head` into `tail -n 2`
by doing `head -n 3 animals.txt | tail -n 2> animals-subset.txt`
{{% /expand %}}