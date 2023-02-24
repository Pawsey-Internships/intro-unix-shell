+++
title = "c. Making Scripts Versatile"
weight = 2
chapter = false
+++

What if we want to select lines from an arbitrary file?
We could edit `middle.sh` each time to change the filename,
but that would probably take longer than typing the command out again
in the shell and executing it with a new file name.
Instead, let's edit `middle.sh` and make it more versatile:

```Bash
$ nano middle.sh
```

Now, within "nano", replace the text `octane.pdb` with the special variable called `$1`:

```Bash
head -n 15 "$1" | tail -n 5
```

Inside a shell script,
`$1` means 'the first filename (or other argument) on the command line'.
We can now run our script like this:

```Bash
$ bash middle.sh octane.pdb
```

~~~
ATOM      9  H           1      -4.502   0.681   0.785  1.00  0.00
ATOM     10  H           1      -5.254  -0.243  -0.537  1.00  0.00
ATOM     11  H           1      -4.357   1.252  -0.895  1.00  0.00
ATOM     12  H           1      -3.009  -0.741  -1.467  1.00  0.00
ATOM     13  H           1      -3.172  -1.337   0.206  1.00  0.00
~~~

or on a different file like this:

```Bash
$ bash middle.sh pentane.pdb
```

~~~
ATOM      9  H           1       1.324   0.350  -1.332  1.00  0.00
ATOM     10  H           1       1.271   1.378   0.122  1.00  0.00
ATOM     11  H           1      -0.074  -0.384   1.288  1.00  0.00
ATOM     12  H           1      -0.048  -1.362  -0.205  1.00  0.00
ATOM     13  H           1      -1.183   0.500  -1.412  1.00  0.00
~~~

 ## Double-Quotes Around Arguments

{{% notice note %}}
For the same reason that we put the loop variable inside double-quotes,
in case the filename happens to contain any spaces,
we surround `$1` with double-quotes.
{{% /notice %}}

Currently, we need to edit `middle.sh` each time we want to adjust the range of
lines that is returned.
Let's fix that by configuring our script to instead use three command-line arguments.
After the first command-line argument (`$1`), each additional argument that we
provide will be accessible via the special variables `$1`, `$2`, `$3`,
which refer to the first, second, third command-line arguments, respectively.

Knowing this, we can use additional arguments to define the range of lines to
be passed to `head` and `tail` respectively:

```Bash
$ nano middle.sh
```

~~~
head -n "$2" "$1" | tail -n "$3"
~~~
