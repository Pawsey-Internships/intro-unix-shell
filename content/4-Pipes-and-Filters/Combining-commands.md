+++
title = "e. Combining Commands"
weight = 2
chapter = false
+++

Nothing prevents us from chaining pipes consecutively.
We can for example send the output of `wc` directly to `sort`,
and then the resulting output to `head`.
This removes the need for any intermediate files.

We'll start by using a pipe to send the output of `wc` to `sort`:

```Bash
$ wc -l *.pdb | sort -n
```

~~~
   9 methane.pdb
  12 ethane.pdb
  15 propane.pdb
  20 cubane.pdb
  21 pentane.pdb
  30 octane.pdb
 107 total
~~~

We can then send that output through another pipe, to `head`, so that the full pipeline becomes:

```Bash
$ wc -l *.pdb | sort -n | head -n 1
```

~~~
   9  methane.pdb
~~~

This is exactly like a mathematician nesting functions like *log(3x)*
and saying 'the log of three times *x*'. In our case,
the calculation is 'head of sort of line count of `*.pdb`'.


The redirection and pipes used in the last few commands are illustrated below:

![Redirects and Pipes of different commands: "wc -l *.pdb" will direct the
output to the shell. "wc -l *.pdb > lengths" will direct output to the file
"lengths". "wc -l *.pdb | sort -n | head -n 1" will build a pipeline where the
output of the "wc" command is the input to the "sort" command, the output of
the "sort" command is the input to the "head" command and the output of the
"head" command is directed to the shell](images/redirects-and-pipes.svg)

## Exercise: Piping Commands Together

In our current directory, we want to find the 3 files which have the least number of
lines. Which command listed below would work?

1. `wc -l * > sort -n > head -n 3`
2. `wc -l * | sort -n | head -n 1-3`
3. `wc -l * | head -n 3 | sort -n`
4. `wc -l * | sort -n | head -n 3`

{{% expand "Solution" %}}
Option 4 is the solution.
The pipe character `|` is used to connect the output from one command to
the input of another.
`>` is used to redirect standard output to a file.
Try it in the `shell-lesson-data/molecules` directory!
{{% /expand %}}