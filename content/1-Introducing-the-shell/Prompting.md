+++
title = "b. Prompting"
weight = 2
chapter = true
+++

## Prompting

Let’s get started.

When the shell is first opened, you are presented with a **prompt**, indicating that the shell is waiting for input.

```Bash
$
```

The shell typically uses `$ ` as the prompt, but may use a different symbol.
In the examples for this lesson, we'll show the prompt as `$ `.
Most importantly:
when typing commands, either from these lessons or from other sources,
*do not type the prompt*, only the commands that follow it.
Also note that after you type a command, you have to press the <kbd>Enter</kbd> key to execute it.

{{% notice note Note%}}
### Other Prompts
Depending on your linux installation you may have a different prompt
For example

```
[user@machine directory]$ _
```
{{% /notice %}}

The prompt is followed by a **text cursor**, a character that indicates the position where your
typing will appear.
The cursor is usually a flashing or solid block, but it can also be an underscore or a pipe.
You may have seen it in a text editor program, for example.

So let's try our first command, `ls` which is short for listing.
This command will list the contents of the current directory:

```Bash
$ ls
```

~~~
Desktop     Downloads   Movies      Pictures
Documents   Library     Music       Public
~~~

{{% notice note Note%}}
### Command not found
If the shell can't find a program whose name is the command you typed, it
will print an error message such as:

```Bash
$ ks
```

~~~
ks: command not found
~~~

This might happen if the command was mis-typed or if the program corresponding to that command
is not installed.
{{% /notice %}}