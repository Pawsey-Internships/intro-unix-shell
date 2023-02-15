+++
title = "a. Background"
weight = 2
chapter = true
+++

## Background

**Loops** are a programming construct which allow us to repeat a command or set of commands
for each item in a list.
As such they are key to productivity improvements through automation.
Similar to wildcards and tab completion, using loops also reduces the
amount of typing required (and hence reduces the number of typing mistakes).

Suppose we have several hundred genome data files named `basilisk.dat`, `minotaur.dat`, and
`unicorn.dat`. For this example, we'll use the `creatures` directory which only has three example files,
but the principles can be applied to many many more files at once.

The structure of these files is the same: the common name, classification, and updated date are
presented on the first three lines, with DNA sequences on the following lines.
Let's look at the files:

```Bash
$ head -n 5 basilisk.dat minotaur.dat unicorn.dat
```

We would like to print out the classification for each species, which is given on the second
line of each file. For each file, we would need to execute the command `head -n 2` and pipe 
this to `tail -n 1`. We’ll use a loop to solve this problem, but first let’s look at the general
form of a loop:

```Bash
for thing in list_of_things
do
    operation_using $thing    # Indentation within the loop is not required, but aids legibility
done
```

and we can apply this to our example like this:

```Bash
$ for filename in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $filename | tail -n 1
> done
```

```
CLASSIFICATION: basiliscus vulgaris
CLASSIFICATION: bos hominus
CLASSIFICATION: equus monoceros
```


