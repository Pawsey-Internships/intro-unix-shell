+++
title = "f. Copying with Glob"
weight = 2
chapter = true
+++

## Copying with Glob

We would like to modify each of the files in `shell-lesson-data/creatures`, but also save a version
of the original files, naming the copies `original-basilisk.dat` and `original-unicorn.dat`.
We can't use:

```Bash
$ cp *.dat original-*.dat
```

because that would expand to:

```Bash
$ cp basilisk.dat minotaur.dat unicorn.dat original-*.dat
```

This wouldn't back up our files, instead we get an error:

~~~
cp: target `original-*.dat' is not a directory
~~~

This problem arises when `cp` receives more than two inputs. When this happens, it
expects the last input to be a directory where it can copy all the files it was passed.
Since there is no directory named `original-*.dat` in the `creatures` directory we get an
error.

Instead, we can use a loop:
```Bash
$ for filename in *.dat
> do
>     cp $filename original-$filename
> done
```

This loop runs the `cp` command once for each filename.
The first time, when `$filename` expands to `basilisk.dat`,
the shell executes:

```Bash
cp basilisk.dat original-basilisk.dat
```

The second time, the command is:

```Bash
cp minotaur.dat original-minotaur.dat
```

The third and last time, the command is:

```Bash
cp unicorn.dat original-unicorn.dat
```

Since the `cp` command does not normally produce any output, it's hard to check
that the loop is doing the correct thing.
However, we learned earlier how to print strings using `echo`, and we can modify the loop
to use `echo` to print our commands without actually executing them.
As such we can check what commands *would be* run in the unmodified loop.

The following diagram
shows what happens when the modified loop is executed, and demonstrates how the
judicious use of `echo` is a good debugging technique.

![The for loop "for filename in *.dat; do echo cp $filename original-$filename;
done" will successively assign the names of all "*.dat" files in your current
directory to the variable "$filename" and then execute the command. With the
files "basilisk.dat", "minotaur.dat" and "unicorn.dat" in the current directory
the loop will successively call the echo command three times and print three
lines: "cp basislisk.dat original-basilisk.dat", then "cp minotaur.dat
original-minotaur.dat" and finally "cp unicorn.dat
original-unicorn.dat"](images/shell_script_for_loop_flow_chart.svg)