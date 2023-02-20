+++
title = "e. Finding Things"
weight = 2
chapter = true
+++


## Finding files and combining with grep

While `grep` finds lines in files and `sed` can replace lines,
the `find` command finds files themselves. Again, it has a lot of 
options; to show how the simplest ones work, we'll use the directory tree shown below.

![A file tree under the directory "writing" contians several sub-directories and
files such that "writing" contains directories "data", "thesis", "tools" and a
file "haiku.txt"; "writing/data" contains the files "Little Women.txt",
"one.txt" and "two.txt"; "writing/thesis" contains the file "empty-draft.md";
"writing/tools" contains the directory "old" and the files "format" and "stats";
and "writing/tools/old" contains a file "oldtool"](images/find-file-tree.svg)

Nelle's `writing` directory contains one file called `haiku.txt` and three subdirectories:
`thesis` (which contains a sadly empty file, `empty-draft.md`);
`data` (which contains three files `LittleWomen.txt`, `one.txt` and `two.txt`);
and a `tools` directory that contains the programs `format` and `stats`,
and a subdirectory called `old`, with a file `oldtool`.

For our first command,
let's run `find .` (remember to run this command from the `shell-lesson-data/writing` folder).

```Bash
$ find .
```

~~~
.
./data
./data/one.txt
./data/LittleWomen.txt
./data/two.txt
./tools
./tools/format
./tools/old
./tools/old/oldtool
./tools/stats
./haiku.txt
./thesis
./thesis/empty-draft.md
~~~

As always, the `.` on its own means the current working directory,
which is where we want our search to start. `find`'s output is the 
names of every file **and** directory under the current working directory.
This can seem useless at first but `find` has many options to filter the output
and in this lesson we will discover some of them.

The first option in our list is `-type d` that means 'things that are directories'.
Sure enough, `find`'s output is the names of the five directories in our little tree
(including `.`):

```Bash
$ find . -type d
```

~~~
./
./data
./thesis
./tools
./tools/old
~~~

Notice that the objects `find` finds are not listed in any particular order.
If we change `-type d` to `-type f`,
we get a listing of all the files instead:

```Bash
$ find . -type f
```

~~~
./haiku.txt
./tools/stats
./tools/old/oldtool
./tools/format
./thesis/empty-draft.md
./data/one.txt
./data/LittleWomen.txt
./data/two.txt
~~~

Now let's try matching by name:

```Bash
$ find . -name *.txt
```

~~~
./haiku.txt
~~~

We expected it to find all the text files, but it only prints out `./haiku.txt`.
The problem is that the shell expands wildcard characters like `*` *before* commands run.
Since `*.txt` in the current directory expands to `haiku.txt`,
the command we actually ran was:

```Bash
$ find . -name haiku.txt
```

`find` did what we asked; we just asked for the wrong thing.

To get what we want,
let's do what we did with `grep`:
put `*.txt` in quotes to prevent the shell from expanding the `*` wildcard.
This way,
`find` actually gets the pattern `*.txt`, not the expanded filename `haiku.txt`:

```Bash
$ find . -name "*.txt"
```

~~~
./data/one.txt
./data/LittleWomen.txt
./data/two.txt
./haiku.txt
~~~

## Listing vs. Finding

`ls` and `find` can be made to do similar things given the right options,
but under normal circumstances, `ls` lists everything it can,
while `find` searches for things with certain properties and shows them.

As we said earlier, the command line's power lies in combining tools.
We've seen how to do that with pipes; let's look at another technique.
As we just saw, `find . -name "*.txt"` gives us a list of all text files 
in or below the current directory. How can we combine that with `wc -l` to 
count the lines in all those files?

The simplest way is to put the `find` command inside `$()`:

```Bash
$ wc -l $(find . -name "*.txt")
```

~~~
11 ./haiku.txt
300 ./data/two.txt
21022 ./data/LittleWomen.txt
70 ./data/one.txt
21403 total
~~~

When the shell executes this command,
the first thing it does is run whatever is inside the `$()`.
It then replaces the `$()` expression with that command's output.
Since the output of `find` is the four filenames `./data/one.txt`, `./data/LittleWomen.txt`,
`./data/two.txt`, and `./haiku.txt`, the shell constructs the command:

```Bash
$ wc -l ./data/one.txt ./data/LittleWomen.txt ./data/two.txt ./haiku.txt
```

which is what we wanted.
This expansion is exactly what the shell does when it expands wildcards like `*` and `?`,
but lets us use any command we want as our own 'wildcard'.

It's very common to use `find` and `grep` together.
The first finds files that match a pattern;
the second looks for lines inside those files that match another pattern.
Here, for example, we can find PDB files that contain iron atoms
by looking for the string 'FE' in all the `.pdb` files above the current directory:

```Bash
$ grep "FE" $(find .. -name "*.pdb")
```

~~~
../data/pdb/heme.pdb:ATOM     25 FE           1      -0.924   0.535  -0.518
~~~

## Exercise: Matching and Subtracting

The `-v` option to `grep` inverts pattern matching, so that only lines
which do *not* match the pattern are printed. Given that, which of
the following commands will find all files in `/data` whose names
end in `s.txt` but whose names also do *not* contain the string `net`?
(For example, `animals.txt` or `amino-acids.txt` but not `planets.txt`.)
Once you have thought about your answer, you can test the commands in the `shell-lesson-data`
directory.

1.  `find data -name "*s.txt" | grep -v net`
2.  `find data -name *s.txt | grep -v net`
3.  `grep -v "net" $(find data -name "*s.txt")`
4.  None of the above.

{{% expand "Solution" %}}
The correct answer is 1. Putting the match expression in quotes prevents the shell
expanding it, so it gets passed to the `find` command.

Option 2 is incorrect because the shell expands `*s.txt` instead of passing the wildcard
expression to `find`.

Option 3 is incorrect because it searches the contents of the files for lines which
do not match 'net', rather than searching the file names.
{{% /expand %}}

## Binary Files

We have focused exclusively on finding patterns in text files. What if
your data is stored as images, in databases, or in some other format?

A handful of tools extend `grep` to handle a few non text formats. But a
more generalizable approach is to convert the data to text, or
extract the text-like elements from the data. On the one hand, it makes simple
things easy to do. On the other hand, complex things are usually impossible. For
example, it's easy enough to write a program that will extract X and Y
dimensions from image files for `grep` to play with, but how would you
write something to find values in a spreadsheet whose cells contained
formulas?

A last option is to recognize that the shell and text processing have
their limits, and to use another programming language.
When the time comes to do this, don't be too hard on the shell: many
modern programming languages have borrowed a lot of
ideas from it, and imitation is also the sincerest form of praise.
{: .callout}

The Unix shell is older than most of the people who use it. It has
survived so long because it is one of the most productive programming
environments ever created --- maybe even *the* most productive. Its syntax
may be cryptic, but people who have mastered it can experiment with
different commands interactively, then use what they have learned to
automate their work. Graphical user interfaces may be easier to use at
first, but once learned, the productivity in the shell is unbeatable.
And as Alfred North Whitehead wrote in 1911, 'Civilization advances by
extending the number of important operations which we can perform
without thinking about them.'
