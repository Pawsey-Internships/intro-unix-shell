+++
title = "h. History"
weight = 2
chapter = true
+++

## Beginning and End

We can move to the beginning of a line in the shell by typing <kbd>Ctrl</kbd>+<kbd>A</kbd>
and to the end using <kbd>Ctrl</kbd>+<kbd>E</kbd>.

When Nelle runs her program now, it produces one line of output every five seconds or so:

~~~
NENE01729A.txt
NENE01729B.txt
NENE01736A.txt
...
~~~

1518 times 5 seconds divided by 60 tells her that her script will take about two hours to run.
As a final check, she opens another terminal window, goes into `north-pacific-gyre/2012-07-03`,
and uses `cat stats-NENE01729B.txt` to examine one of the output files. It looks good,
so she decides to get some coffee and catch up on her reading.

## Those Who Know History Can Choose to Repeat It

Another way to repeat previous work is to use the `history` command to
get a list of the last few hundred commands that have been executed, and
then to use `!123` (where '123' is replaced by the command number) to
repeat one of those commands. For example, if Nelle types this:

```Bash
$ history | tail -n 5
```

~~~
  456  ls -l NENE0*.txt
  457  rm stats-NENE01729B.txt.txt
  458  bash goostats.sh NENE01729B.txt stats-NENE01729B.txt
  459  ls -l NENE0*.txt
  460  history
~~~

then she can re-run `goostats.sh` on `NENE01729B.txt` simply by typing `!458`.


## Other History Commands

There are a number of other shortcut commands for getting at the history.

- <kbd>Ctrl</kbd>+<kbd>R</kbd> enters a history search mode 'reverse-i-search' and finds the
most recent command in your history that matches the text you enter next.
Press <kbd>Ctrl</kbd>+<kbd>R</kbd> one or more additional times to search for earlier matches.
You can then use the left and right arrow keys to choose that line and edit
it then hit <kbd>Return</kbd> to run the command.
- `!!` retrieves the immediately preceding command
(you may or may not find this more convenient than using <kbd>↑</kbd>)
- `!$` retrieves the last word of the last command.
That's useful more often than you might expect: after
`bash goostats.sh NENE01729B.txt stats-NENE01729B.txt`, you can type
`less !$` to look at the file `stats-NENE01729B.txt`, which is
quicker than doing <kbd>↑</kbd> and editing the command-line.

