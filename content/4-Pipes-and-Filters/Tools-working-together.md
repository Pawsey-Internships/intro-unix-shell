+++
title = "f. Tools Working Together"
weight = 2
chapter = false
+++

This idea of linking programs together is why Unix has been so successful.
Instead of creating enormous programs that try to do many different things,
Unix programmers focus on creating lots of simple tools that each do one job well,
and that work well with each other. This programming model is called 'pipes and filters'. 

We've already seen pipes; a **filter** is a program like `wc` or `sort`
that transforms a stream of input into a stream of output. Almost all of the standard 
Unix tools can work this way: unless told to do otherwise,they read from standard input,
do something with what they've read, and write to standard output.

The key is that any program that reads lines of text from standard input and writes lines 
of text to standard output can be combined with every other program that behaves this way 
as well. You can *and should* write your programs this way so that you and other people can
put those programs into pipes to multiply their power.


## Exercise: Pipe Reading Comprehension

A file called `animals.txt` (in the `shell-lesson-data/data` folder) contains the following data:

```Bash
2012-11-05,deer
2012-11-05,rabbit
2012-11-05,raccoon
2012-11-06,rabbit
2012-11-06,deer
2012-11-06,fox
2012-11-07,rabbit
2012-11-07,bear
```


What text passes through each of the pipes and the final redirect in the pipeline below?

```Bash
$ cat animals.txt | head -n 5 | tail -n 3 | sort -r > final.txt
```

**Hint**: build the pipeline up one command at a time to test your understanding

{{% expand "Solution" %}}
The `head` command extracts the first 5 lines from `animals.txt`.
Then, the last 3 lines are extracted from the previous 5 by using the `tail` command.
With the `sort -r` command those 3 lines are sorted in reverse order and finally,
the output is redirected to a file `final.txt`. The content of this file can be checked 
by executing `cat final.txt`. The file should contain the following lines:
```Bash
2012-11-06,rabbit
2012-11-06,deer
2012-11-05,raccoon
```
{{% /expand %}}

## Exercise: Pipe Construction

For the file `animals.txt` from the previous exercise, consider the following command:

```Bash
$ cut -d , -f 2 animals.txt
```

The `cut` command is used to remove or 'cut out' certain sections of each line in the file,
and `cut` expects the lines to be separated into columns by a <kbd>Tab</kbdcharacter.
A character used in this way is a called a **delimiter**.
In the example above we use the `-d` option to specify the comma as our delimiter character.
We have also used the `-f` option to specify that we want to extract the second field (column).
This gives the following output:

~~~
deer
rabbit
raccoon
rabbit
deer
fox
rabbit
bear
~~~


The `uniq` command filters out adjacent matching lines in a file.
How could you extend this pipeline (using `uniq` and another command) to find
out what animals the file contains (without any duplicates in their
names)?

{{% expand "Solution" %}}
```Bash
$ cut -d , -f 2 animals.txt | sort | uniq
```
{{% /expand %}}

## Exercise: Which Pipe?

The file `animals.txt` contains 8 lines of data formatted as follows:

~~~
2012-11-05,deer
2012-11-05,rabbit
2012-11-05,raccoon
2012-11-06,rabbit
...
~~~

The `uniq` command has a `-c` option which gives a count of the
number of times a line occurs in its input.  Assuming your current
directory is `shell-lesson-data/data/`, what command would you use to produce
a table that shows the total count of each type of animal in the file?

1.  `sort animals.txt | uniq -c`
2.  `sort -t, -k2,2 animals.txt | uniq -c`
3.  `cut -d, -f 2 animals.txt | uniq -c`
4.  `cut -d, -f 2 animals.txt | sort | uniq -c`
5.  `cut -d, -f 2 animals.txt | sort | uniq -c | wc -l`

{{% expand "Solution" %}}
Option 4. is the correct answer.
If you have difficulty understanding why, try running the commands, or sub-sections of
the pipelines (make sure you are in the `shell-lesson-data/data` directory).
{{% /expand %}}

## Exercise: Removing Unneeded Files

Suppose you want to delete your processed data files, and only keep
your raw files and processing script to save storage.
The raw files end in `.dat` and the processed files end in `.txt`.
Which of the following would remove all the processed data files,
and *only* the processed data files?

1. `rm ?.txt`
2. `rm *.txt`
3. `rm * .txt`
4. `rm *.*`

{{% expand "Solution" %}}
1. This would remove `.txt` files with one-character names
2. This is correct answer
3. The shell would expand `*` to match everything in the current directory,
so the command would try to remove all matched files and an additional
file called `.txt`
4. The shell would expand `*.*` to match all files with any extension,
so this command would delete all files
{{% /expand %}}

