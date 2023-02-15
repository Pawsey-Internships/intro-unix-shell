+++
title = "d. Copying Files and Directories"
weight = 2
chapter = true
+++

## Copying files and directories

The `cp` command works very much like `mv`, except it copies 
a file instead of moving it. We can check that it did the right
thing using `ls` with two paths as arguments --- like most Unix
commands, `ls` can be given multiple paths at once:

```Bash
$ cp quotes.txt thesis/quotations.txt
$ ls quotes.txt thesis/quotations.txt
```

~~~
quotes.txt   thesis/quotations.txt
~~~


We can also copy a directory and all its contents by using the
[recursive](https://en.wikipedia.org/wiki/Recursion) option `-r`,
e.g. to back up a directory:

```Bash
$ cp -r thesis thesis_backup
```

We can check the result by listing the contents of both the `thesis` and `thesis_backup` directory:

```Bash
$ ls thesis thesis_backup
```

```
thesis:
quotations.txt

thesis_backup:
quotations.txt
```
