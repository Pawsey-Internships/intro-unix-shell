+++
title = "b. Grep Flags"
weight = 2
chapter = true
+++

## Grep Flags

To restrict matches to lines containing the word 'The' on its own,
we can give `grep` with the `-w` option. This will limit matches to word boundaries.

Later in this lesson, we will also see how we can change the search behavior of grep
with respect to its case sensitivity.

```Bash
$ grep -w The haiku.txt
```

~~~
The Tao that is seen
~~~

Note that a 'word boundary' includes the start and end of a line, so not
just letters surrounded by spaces. Sometimes we don't want to search for 
a single word, but a phrase. This is also easy to do with `grep` by putting
the phrase in quotes.

```Bash
$ grep -w "is not" haiku.txt
```

~~~
Today it is not working
~~~

We've now seen that you don't have to have quotes around single words,
but it is useful to use quotes when searching for multiple words.
It also helps to make it easier to distinguish between the search term or phrase
and the file being searched. We will use quotes in the remaining examples.

Another useful option is `-n`, which numbers the lines that match:

```Bash
$ grep -n "it" haiku.txt
```

~~~
5:With searching comes loss
9:Yesterday it worked
10:Today it is not working
~~~

Here, we can see that lines 5, 9, and 10 contain the letters 'it'.

We can combine options (i.e. flags) as we do with other Unix commands.
For example, let's find the lines that contain the word 'the'.
We can combine the option `-w` to find the lines that contain the word 'the'
and `-n` to number the lines that match:

```Bash
$ grep -n -w "the" haiku.txt
```

~~~
2:Is not the true Tao, until
6:and the presence of absence:
~~~

{{% notice note %}}
## Using multiple flags

Remember that flags for most commands can be concatenated together:

```Bash
grep -nw "the" haiku.txt
```

We will use this going forward
{{% /notice %}}

Now we want to use the option `-i` to make our search case-insensitive:

```Bash
$ grep -nwi "the" haiku.txt
```

~~~
1:The Tao that is seen
2:Is not the true Tao, until
6:and the presence of absence:
~~~

Now, we want to use the option `-v` to invert our search, i.e., we want to output
the lines that do not contain the word 'the'.

```Bash
$ grep -nwv "the" haiku.txt
```

~~~
1:The Tao that is seen
3:You bring fresh toner.
4:
5:With searching comes loss
7:"My Thesis" not found.
8:
9:Yesterday it worked
10:Today it is not working
11:Software is like that.
~~~


If we use the `-r` (recursive) option,
`grep` can search for a pattern recursively through a set of files in subdirectories.

Let's search recursively for `Yesterday` in the `shell-lesson-data/writing` directory:

```Bash
$ grep -r Yesterday .
```


```
data/LittleWomen.txt:"Yesterday, when Aunt was asleep and I was trying to be as still as a
data/LittleWomen.txt:Yesterday at dinner, when an Austrian officer stared at us and then
data/LittleWomen.txt:Yesterday was a quiet day spent in teaching, sewing, and writing in my
haiku.txt:Yesterday it worked
```

`grep` has lots of other options. To find out what they are, we can try either `--help` or `man`:

```Bash
$ grep --help

$ man grep
```
~~~
Usage: grep [OPTION]... PATTERN [FILE]...
Search for PATTERN in each FILE or standard input.
PATTERN is, by default, a basic regular expression (BRE).
Example: grep -i 'hello world' menu.h main.c

Regexp selection and interpretation:
  -E, --extended-regexp     PATTERN is an extended regular expression (ERE)
  -F, --fixed-strings       PATTERN is a set of newline-separated fixed strings
  -G, --basic-regexp        PATTERN is a basic regular expression (BRE)
  -P, --perl-regexp         PATTERN is a Perl regular expression
  -e, --regexp=PATTERN      use PATTERN for matching
  -f, --file=FILE           obtain PATTERN from FILE
  -i, --ignore-case         ignore case distinctions
  -w, --word-regexp         force PATTERN to match only whole words
  -x, --line-regexp         force PATTERN to match only whole lines
  -z, --null-data           a data line ends in 0 byte, not newline

Miscellaneous:
...        ...        ...
~~~

## Exercise: Using `grep`

Which command would result in the following output:

~~~
and the presence of absence:
~~~
{: .output}

1. `grep "of" haiku.txt`
2. `grep -E "of" haiku.txt`
3. `grep -w "of" haiku.txt`
4. `grep -i "of" haiku.txt`

{{% expand "Solution" %}}
The correct answer is 3, because the `-w` option looks only for whole-word matches.
The other options will also match 'of' when part of another word.
{{% /expand %}}