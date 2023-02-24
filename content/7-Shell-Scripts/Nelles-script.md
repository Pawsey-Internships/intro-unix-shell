+++
title = "f. Nelle's Pipeline - Scripting"
weight = 2
chapter = false
+++

## Nelle's Pipeline: Creating a Script

Nelle's supervisor insisted that all her analytics must be reproducible.
The easiest way to capture all the steps is in a script.

First we return to Nelle's data directory:
```Bash
$ cd ../north-pacific-gyre/2012-07-03/
```

She runs the editor and writes the following:

```Bash
# Calculate stats for data files.
for datafile in "$@"
do
    echo $datafile
    bash goostats.sh $datafile stats-$datafile
done
```

She saves this in a file called `do-stats.sh`
so that she can now re-do the first stage of her analysis by typing:

```Bash
$ bash do-stats.sh NENE*A.txt NENE*B.txt
```

She can also do this:

```Bash
$ bash do-stats.sh NENE*A.txt NENE*B.txt | wc -l
```

so that the output is just the number of files processed
rather than the names of the files that were processed.

One thing to note about Nelle's script is that
it lets the person running it decide what files to process.
She could have written it as:

```Bash
# Calculate stats for Site A and Site B data files.
for datafile in NENE*A.txt NENE*B.txt
do
    echo $datafile
    bash goostats.sh $datafile stats-$datafile
done
```

The advantage is that this always selects the right files:
she doesn't have to remember to exclude the 'Z' files.
The disadvantage is that it *always* selects just those files --- she can't run it on all files
(including the 'Z' files),
or on the 'G' or 'H' files her colleagues in Antarctica are producing,
without editing the script.
If she wanted to be more adventurous,
she could modify her script to check for command-line arguments,
and use `NENE*A.txt NENE*B.txt` if none were provided.
Of course, this introduces another tradeoff between flexibility and complexity.