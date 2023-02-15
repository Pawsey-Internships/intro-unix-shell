+++
title = "g. Nelle's Pipeline: Processing Files"
weight = 2
chapter = true
+++

## Nelle's Pipeline: Processing Files

Nelle is now ready to process her data files using `goostats.sh` ---
a shell script written by her supervisor.
This calculates some statistics from a protein sample file, and takes two arguments:

1. an input file (containing the raw data)
2. an output file (to store the calculated statistics)

Since she's still learning how to use the shell, she decides to build up the required
commands in stages. Her first step is to make sure that she can select the right input
files --- remember, these are ones whose names end in 'A' or 'B', rather than 'Z'.
Starting from her home directory, Nelle types:

```Bash
$ cd north-pacific-gyre/2012-07-03
$ for datafile in NENE*A.txt NENE*B.txt
> do
>     echo $datafile
> done
```

~~~
NENE01729A.txt
NENE01729B.txt
NENE01736A.txt
...
NENE02043A.txt
NENE02043B.txt
~~~

Her next step is to decide what to call the files that the `goostats.sh` 
analysis program will create. Prefixing each input file's name with 'stats' 
seems simple, so she modifies her loop to do that:

```Bash
$ for datafile in NENE*A.txt NENE*B.txt
> do
>     echo $datafile stats-$datafile
> done
```

~~~
NENE01729A.txt stats-NENE01729A.txt
NENE01729B.txt stats-NENE01729B.txt
NENE01736A.txt stats-NENE01736A.txt
...
NENE02043A.txt stats-NENE02043A.txt
NENE02043B.txt stats-NENE02043B.txt
~~~

She hasn't actually run `goostats.sh` yet, but now she's sure she can select
the right files and generate the right output filenames.

Typing in commands over and over again is becoming tedious, though,
and Nelle is worried about making mistakes, so instead of re-entering her loop,
she presses <kbd>↑</kbd>. In response, the shell redisplays the whole loop on one line
(using semi-colons to separate the pieces):

```Bash
$ for datafile in NENE*A.txt NENE*B.txt; do echo $datafile stats-$datafile; done
```

Using the left arrow key, Nelle backs up and changes the command `echo` to
`bash goostats.sh`:

```Bash
$ for datafile in NENE*A.txt NENE*B.txt; do bash goostats.sh $datafile stats-$datafile; done
```

When she presses <kbd>Enter</kbd>, the shell runs the modified command.
However, nothing appears to happen --- there is no output.
After a moment, Nelle realizes that since her script doesn't print anything to the screen
any longer, she has no idea whether it is running, much less how quickly.
She kills the running command by typing <kbd>Ctrl</kbd>+<kbd>C</kbd>,
uses <kbd>↑</kbd> to repeat the command, and edits it to read:

```Bash
$ for datafile in NENE*A.txt NENE*B.txt; do echo $datafile;
bash goostats.sh $datafile stats-$datafile; done
```