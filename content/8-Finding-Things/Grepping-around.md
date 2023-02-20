+++
title = "a. Grepping Around"
weight = 2
chapter = true
+++

## Grepping Around

In the same way that many of us now use 'Google' as a
verb meaning 'to find', Unix programmers often use the word 'grep'.
'grep' is a contraction of 'global/regular expression/print',
a common sequence of operations in early Unix text editors.
It is also the name of a very useful command-line program.

`grep` finds and prints lines in files that match a pattern. It works like a filter search.
For our examples, we will use a file that contains three haiku taken from a
1998 competition in *Salon* magazine. For this set of examples,
we're going to be working in the writing subdirectory:

```Bash
$ cd ~/shell-lesson-data/writing
$ cat haiku.txt
```

~~~
The Tao that is seen
Is not the true Tao, until
You bring fresh toner.

With searching comes loss
and the presence of absence:
"My Thesis" not found.

Yesterday it worked
Today it is not working
Software is like that.
~~~

{{% notice note %}}
## Forever, or Five Years

We haven't linked to the original haiku because
they don't appear to be on *Salon*'s site any longer.
As [Jeff Rothenberg said](https://www.clir.org/wp-content/uploads/sites/6/ensuring.pdf),
'Digital information lasts forever --- or five years, whichever comes first.'
Luckily, popular content often [has backups](http://wiki.c2.com/?ComputerErrorHaiku).
{{% /notice %}}

Let's find lines that contain the word 'not':

```Bash
$ grep not haiku.txt
```

~~~
Is not the true Tao, until
"My Thesis" not found
Today it is not working
~~~

Here, `not` is the pattern we're searching for.
The grep command searches through the file, looking for matches to the pattern specified.
To use it type `grep`, then the pattern we're searching for and finally
the name of the file (or files) we're searching in.

The output is the three lines in the file that contain the letters 'not'.

By default, grep searches for a pattern in a case-sensitive way.
In addition, the search pattern we have selected does not have to form a complete word,
as we will see in the next example.

Let's search for the pattern: 'The'.

```Bash
$ grep The haiku.txt
```

~~~
The Tao that is seen
"My Thesis" not found.
~~~

This time, two lines that include the letters 'The' are outputted,
one of which contained our search pattern within a larger word, 'Thesis'.