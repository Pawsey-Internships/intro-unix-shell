+++
title = "a. Background"
weight = 2
chapter = false
+++


Now that we know a few basic commands,
we can finally look at the shell's most powerful feature:
the ease with which it lets us combine existing programs in new ways.
We'll start with the directory called `shell-lesson-data/molecules`
that contains six files describing some simple organic molecules.
The `.pdb` extension indicates that these files are in Protein Data Bank format,
a simple text format that specifies the type and position of each atom in the molecule.

```Bash
$ cd ~/shell-lesson-data
$ ls molecules
```

~~~
cubane.pdb    ethane.pdb    methane.pdb
octane.pdb    pentane.pdb   propane.pdb
~~~


Let's go into that directory with `cd` and run an example  command  `wc -l` instead of just `wc`,
the output shows only the number of lines per file:

```Bash
$ cd molecules
$ wc -l *.pdb
```

~~~
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
~~~


The `-m` and `-w` options can also be used with the `wc` command, to show
only the number of characters or the number of words in the files.

{{% notice note %}}
#### Why Is My Code Hanging?

What happens if a command is supposed to process a file, but we
don't give it a filename? For example, what if we type:

```Bash
$ wc -l
```

but don't type `*.pdb` (or anything else) after the command?
Since it doesn't have any filenames, `wc` assumes it is supposed to
process input given at the command prompt, so it just sits there and waits for us to give
it some data interactively. From the outside, though, all we see is it
sitting there: the command doesn't appear to do anything.

Hint: Press <kbd>Ctrl</kbd>+<kbd>C</kbd> to cancel the executable when the code hangs...
If you make this kind of mistake, you can escape out of this state by holding down
the control key (<kbd>Ctrl</kbd>) and typing the letter <kbd>C</kbd> once and 
letting go of the <kbd>Ctrl</kbd> key.
<kbd>Ctrl</kbd>+<kbd>C</kbd>
{{% /notice %}}

