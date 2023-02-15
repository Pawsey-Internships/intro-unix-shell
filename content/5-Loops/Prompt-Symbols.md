+++
title = "b. Prompt Symbols"
weight = 2
chapter = true
+++


## Follow the Prompt

The shell prompt changes from `$` to `>` and back again as we were
typing in our loop. The second prompt, `>`, is different to remind
us that we haven't finished typing a complete command yet. A semicolon, `;`,
can be used to separate two commands written on a single line.

When the shell sees the keyword `for`,
it knows to repeat a command (or group of commands) once for each item in a list.
Each time the loop runs (called an iteration), an item in the list is assigned in sequence to
the **variable**, and the commands inside the loop are executed, before moving on to
the next item in the list. Inside the loop, we call for the variable's value by putting `$` 
in front of it. The `$` tells the shell interpreter to treat the variable as a variable 
name and substitute its value in its place, rather than treat it as text or an external command.

In this example, the list is three filenames: `basilisk.dat`, `minotaur.dat`, and `unicorn.dat`.
Each time the loop iterates, it will assign a file name to the variable `filename`
and run the `head` command. The first time through the loop, `$filename` is `basilisk.dat`.
The interpreter runs the command `head` on `basilisk.dat` and pipes the first two lines to 
the `tail` command, which then prints the second line of `basilisk.dat`. For the second iteration, `$filename` becomes `minotaur.dat`. This time, the shell runs `head` on `minotaur.dat`
and pipes the first two lines to the `tail` command, which then prints the second line of `minotaur.dat`.
For the third iteration, `$filename` becomes `unicorn.dat`, so the shell runs the `head` command 
on that file, and `tail` on the output of that. Since the list was only three items, the shell exits the `for` loop.

{{% notice note %}}
## Same Symbols, Different Meanings

Here we see `>` being used as a shell prompt, whereas `>` is also
used to redirect output.
Similarly, `$` is used as a shell prompt, but, as we saw earlier,
it is also used to ask the shell to get the value of a variable.

If the *shell* prints `>` or `$` then it expects you to type something,
and the symbol is a prompt.

If *you* type `>` or `$` yourself, it is an instruction from you that
the shell should redirect output or get the value of a variable.
{{% /notice %}}

When using variables it is also possible to put the names into curly braces to clearly
delimit the variable name: `$filename` is equivalent to `${filename}`, but is different from
`${file}name`. You may find this notation in other people's programs.

We have called the variable in this loop `filename` in order to make its purpose clearer
to human readers. The shell itself doesn't care what the variable is called;
if we wrote this loop as:

```Bash
$ for x in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $x | tail -n 1
> done
```

or:

```Bash
$ for temperature in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $temperature | tail -n 1
> done
```

it would work exactly the same way.

**Don't do this!**
Programs are only useful if people can understand them,
so meaningless names (like `x`) or misleading names (like `temperature`)
increase the odds that the program won't do what its readers think it does.
