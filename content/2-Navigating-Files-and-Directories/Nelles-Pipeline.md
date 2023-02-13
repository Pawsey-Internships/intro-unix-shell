+++
title = "g. Nelle's Pipeline"
weight = 2
chapter = true
+++


## Nelle's Pipeline: Organizing Files

Knowing this much about files and directories,
Nelle is ready to organize the files that the protein assay machine will create.
First,
she creates a directory called `north-pacific-gyre`
(to remind herself where the data came from).
Inside that,
she creates a directory called `2012-07-03`,
which is the date she started processing the samples.
She used to use names like `conference-paper` and `revised-results`,
but she found them hard to understand after a couple of years.
(The final straw was when she found herself creating
a directory called `revised-revised-results-3`.)

#### Sorting Output

Nelle names her directories 'year-month-day',
with leading zeroes for months and days,
because the shell displays file and directory names in alphabetical order.
If she used month names, December would come before July;
if she didn't use leading zeroes, November ('11') would come before July 
('7'). Similarly, putting the year first means that June 2012 will come before June 2013.

Each of her physical samples is labelled according to her lab's convention
with a unique ten-character ID,
such as 'NENE01729A'.
This ID is what she used in her collection log
to record the location, time, depth, and other characteristics of the sample,
so she decides to use it as part of each data file's name.
Since the assay machine's output is plain text,
she will call her files `NENE01729A.txt`, `NENE01812A.txt`, and so on.
All 1520 files will go into the same directory.

Now in her current directory `shell-lesson-data`,
Nelle can see what files she has using the command:

```Bash
$ ls north-pacific-gyre/2012-07-03/
```

This command is a lot to type,
but she can let the shell do most of the work through what is called **tab completion**.
If she types:

```Bash
$ ls nor
```

and then presses <kbd>Tab</kbd> (the tab key on her keyboard),
the shell automatically completes the directory name for her:

```Bash
$ ls north-pacific-gyre/
```

If she presses <kbd>Tab</kbd> again,
Bash will add `2012-07-03/` to the command,
since it's the only possible completion.
Pressing <kbd>Tab</kbd> again does nothing,
since there are 19 possibilities;
pressing <kbd>Tab</kbd> twice brings up a list of all the files,
and so on.
This is called **tab completion**,
and we will see it in many other tools as we go on.


#### The most common `ls` command

We have already seen that `-a` makes ls show hidden files.
Another very useful flag is `-l` which tells `ls` to use a long listing format.
This includes very useful information like file permissions, file sizes, ownership and modification
times. As such the following command is one of the most used:

```Bash
$ ls -la
```

~~~
total 36
drwxr-xr-x 1 nelle nelle   188 Nov  3 08:40 .
drwxr-xr-x 1 nelle nelle    34 Nov  3 08:40 ..
-rw-r--r-- 1 nelle nelle   199 Nov  3 08:40 .bash_profile
drwxr-xr-x 1 nelle nelle    46 Nov  3 08:40 creatures
drwxr-xr-x 1 nelle nelle   156 Nov  3 08:40 data
drwxr-xr-x 1 nelle nelle    16 Nov  3 08:40 Desktop
drwxr-xr-x 1 nelle nelle   126 Nov  3 08:40 molecules
drwxr-xr-x 1 nelle nelle    20 Nov  3 08:40 north-pacific-gyre
-rw-r--r-- 1 nelle nelle    86 Nov  3 08:40 notes.txt
-rw-r--r-- 1 nelle nelle    32 Nov  3 08:40 pizza.cfg
-rw-r--r-- 1 nelle nelle 21583 Nov  3 08:40 solar.pdf
drwxr-xr-x 1 nelle nelle    54 Nov  3 08:40 writing
~~~

We will cover the specifics of file permissions and ownership later so don't worry
if you don't understand what each collumn means just yet.

