+++
title = "b. Getting Help"
weight = 2
chapter = false
+++


`ls` has lots of other **options**. There are two common ways to find out how
to use a command and what options it accepts:

1. We can pass a `--help` option to the command, such as:
    ```Bash
    $ ls --help
    ```

2. We can read its manual with `man`, such as:
    ```Bash
    $ man ls
    ```

**Depending on your environment, you might find that only one of these commands works
(either `man` or `--help`, e.g., `man` works for macOS and `--help` typically works for Git Bash).**

We'll describe both ways below.

## The `--help` option

Many bash commands, and programs that people have written that can be
run from within bash, support a `--help` option to display more
information on how to use the command or program.

```Bash
$ ls --help
```

~~~
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if neither -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options, too.
  -a, --all                  do not ignore entries starting with .
  -A, --almost-all           do not list implied . and ..
      --author               with -l, print the author of each file
  -b, --escape               print C-style escapes for nongraphic characters
      --block-size=SIZE      scale sizes by SIZE before printing them; e.g.,
                               '--block-size=M' prints sizes in units of
                               1,048,576 bytes; see SIZE format below
  -B, --ignore-backups       do not list implied entries ending with ~
  -c                         with -lt: sort by, and show, ctime (time of last
                               modification of file status information);
                               with -l: show ctime and sort by name;
                               otherwise: sort by ctime, newest first
  -C                         list entries by columns
      --color[=WHEN]         colorize the output; WHEN can be 'always' (default
                               if omitted), 'auto', or 'never'; more info below
  -d, --directory            list directories themselves, not their contents
  -D, --dired                generate output designed for Emacs' dired mode
  -f                         do not sort, enable -aU, disable -ls --color
  -F, --classify             append indicator (one of */=>@|) to entries
...        ...        ...
~~~


{{% notice note %}}
#### Unsupported command-line options
If you try to use an option (flag) that is not supported, `ls` and other commands
will usually print an error message similar to:

```Bash
$ ls -j
```
~~~
ls: invalid option -- 'j'
Try 'ls --help' for more information.
~~~

{{% /notice %}}

#### The `man` command

The other way to learn about `ls` is to type
```Bash
$ man ls
```

This command will turn your terminal into a page with a description
of the `ls` command and its options.

To navigate through the `man` pages, you may use <kbd>↑</kbd> and <kbd>↓</kbd> 
to move line-by-line, or try <kbd>B</kbd> and <kbd>Spacebar</kbd> to skip up 
and down by a full page. To search for a character or word in the `man` pages,
use <kbd>/</kbd> followed by the character or word you are searching for.
Sometimes a search will result in multiple hits. 
If so, you can move between hits using <kbd>N</kbd> (for moving forward) and 
<kbd>Shift</kbd>+<kbd>N</kbd> (for moving backward).

To **quit** the `man` pages, press <kbd>Q</kbd>.

{{% notice note %}}
#### Manual pages on the web
Of course, there is a third way to access help for commands:
searching the internet via your web browser.
When using internet search, including the phrase `unix man page` in your search
query will help to find relevant results.

GNU provides links to its
[manuals](http://www.gnu.org/manual/manual.html) including the
[core GNU utilities](http://www.gnu.org/software/coreutils/manual/coreutils.html),
which covers many commands introduced within this lesson.
{{% /notice %}}