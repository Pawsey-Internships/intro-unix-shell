+++
title = "d. Piping Output"
weight = 2
chapter = false
+++

## Piping: Passing output to another command
In our example of finding the file with the fewest lines,
we are using two intermediate files `lengths.txt` and `sorted-lengths.txt` to store output.
This is a confusing way to work because
even once you understand what `wc`, `sort`, and `head` do,
those intermediate files make it hard to follow what's going on.
We can make it easier to understand by running `sort` and `head` together:

```Bash
$ sort -n lengths.txt | head -n 1
```

~~~
  9  methane.pdb
~~~

The vertical bar, `|`, between the two commands is called a **pipe**.
It tells the shell that we want to use
the output of the command on the left
as the input to the command on the right.

This has removed the need for the `sorted-lengths.txt` file.