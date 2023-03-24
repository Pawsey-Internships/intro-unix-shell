+++
title = "e. Exercises II"
weight = 2
chapter = false
+++

#### Absolute vs. Relative Paths

Starting from `/Users/amanda/data`,
which of the following commands could Amanda use to navigate to her home directory,
which is `/Users/amanda`?

1. `cd .`
2. `cd /`
3. `cd /home/amanda`
4. `cd ../..`
5. `cd ~`
6. `cd home`
7. `cd ~/data/..`
8. `cd`
9. `cd ..`

{{%expand "Solution" %}}
1. No: `.` stands for the current directory.
2. No: `/` stands for the root directory.
3. No: Amanda's home directory is `/Users/amanda`.
4. No: this command goes up two levels, i.e. ends in `/Users`.
5. Yes: `~` stands for the user's home directory, in this case `/Users/amanda`.
6. No: this command would navigate into a directory `home` in the current directory 
    if it exists.
7. Yes: unnecessarily complicated, but correct.
8. Yes: shortcut to go back to the user's home directory.
9. Yes: goes up one level.
{{% /expand%}}

#### Relative Path Resolution

Using the filesystem diagram below, if `pwd` displays `/Users/thing`,
what will `ls -F ../backup` display?

1.  `../backup: No such file or directory`
2.  `2012-12-01 2013-01-08 2013-01-27`
3.  `2012-12-01/ 2013-01-08/ 2013-01-27/`
4.  `original/ pnas_final/ pnas_sub/`

![A directory tree below the Users directory where "/Users" contains the
directories "backup" and "thing"; "/Users/backup" contains "original",
"pnas_final" and "pnas_sub"; "/Users/thing" contains "backup"; and
"/Users/thing/backup" contains "2012-12-01", "2013-01-08" and
"2013-01-27"](images/filesystem-challenge.svg)

{{%expand "Solution" %}}
1. No: there *is* a directory `backup` in `/Users`.
2. No: this is the content of `Users/thing/backup`,
   but with `..`, we asked for one level further up.
3. No: see previous explanation.
4. Yes: `../backup/` refers to `/Users/backup/`.
{{% /expand%}}

#### `ls` Reading Comprehension

Using the filesystem diagram below,
if `pwd` displays `/Users/backup`,
and `-r` tells `ls` to display things in reverse order,
what command(s) will result in the following output:

~~~
pnas_sub/ pnas_final/ original/
~~~

![A directory tree below the Users directory where "/Users" contains the
directories "backup" and "thing"; "/Users/backup" contains "original",
"pnas_final" and "pnas_sub"; "/Users/thing" contains "backup"; and
"/Users/thing/backup" contains "2012-12-01", "2013-01-08" and
"2013-01-27"](images/filesystem-challenge.svg)

1.  `ls pwd`
2.  `ls -r -F`
3.  `ls -r -F /Users/backup`

{{%expand "Solution" %}}
 1. No: `pwd` is not the name of a directory.
 2. Yes: `ls` without directory argument lists files and directories
    in the current directory.
 3. Yes: uses the absolute path explicitly.
{{% /expand%}}