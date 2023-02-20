+++
title = "a. Getting Started"
weight = 2
chapter = true
+++

## Getting Started with scripts

We are finally ready to see what makes the shell such a powerful programming environment.
We are going to take the commands we repeat frequently and save them in files
so that we can re-run all those operations again later by typing a single command.
For historical reasons,
a bunch of commands saved in a file is usually called a **shell script**,
but make no mistake:
these are actually small programs.

Not only will writing shell scripts make your work faster ---
you won't have to retype the same commands over and over again ---
it will also make it more accurate (fewer chances for typos) and more reproducible.
If you come back to your work later (or if someone else finds your work and wants to build on it)
you will be able to reproduce the same results simply by running your script,
rather than having to remember or retype a long list of commands.

Let's start by going back to `molecules/` and creating a new file, `middle.sh` which will
become our shell script:

```Bash
$ cd molecules
$ nano middle.sh
```

The command `nano middle.sh` opens the file `middle.sh` within the text editor 'nano'
(which runs within the shell).
If the file does not exist, it will be created.
We can use the text editor to directly edit the file -- we'll simply insert the following line:

```Bash
head -n 15 octane.pdb | tail -n 5
```

This is a variation on the pipe we constructed earlier:
it selects lines 11-15 of the file `octane.pdb`.
Remember, we are *not* running it as a command just yet:
we are putting the commands in a file.

Then we save the file (`Ctrl-O` in nano),
 and exit the text editor (`Ctrl-X` in nano).
Check that the directory `molecules` now contains a file called `middle.sh`.

Once we have saved the file,
we can ask the shell to execute the commands it contains.
Our shell is called `bash`, so we run the following command:

```Bash
$ bash middle.sh
```

~~~
ATOM      9  H           1      -4.502   0.681   0.785  1.00  0.00
ATOM     10  H           1      -5.254  -0.243  -0.537  1.00  0.00
ATOM     11  H           1      -4.357   1.252  -0.895  1.00  0.00
ATOM     12  H           1      -3.009  -0.741  -1.467  1.00  0.00
ATOM     13  H           1      -3.172  -1.337   0.206  1.00  0.00
~~~

Sure enough, our script's output is exactly what we would get if we ran that pipeline directly.

