+++
title = "e. Spaces in Names"
weight = 2
chapter = true
+++

## Spaces in Names

Spaces are used to separate the elements of the list that we are going to loop over.
If one of those elements contains a space character, we need to surround it with
quotes, and do the same thing to our loop variable. Suppose our data files are named:

~~~
red dragon.dat
purple unicorn.dat
~~~

To loop over these files, we would need to add double quotes like so:

```Bash
$ for filename in "red dragon.dat" "purple unicorn.dat"
do
	head -n 100 "$filename" | tail -n 20
done
```

It is simpler to avoid using spaces (or other special characters) in filenames.

The files above don't exist, so if we run the above code, the `head` command will be unable
to find them, however the error message returned will show the name of the files it is
expecting:

~~~
head: cannot open ‘red dragon.dat’ for reading: No such file or directory
head: cannot open ‘purple unicorn.dat’ for reading: No such file or directory
~~~

Try removing the quotes around `$filename` in the loop above to see the effect of the quote
marks on spaces. Note that we get a result from the loop command for unicorn.dat
when we run this code in the `creatures` directory:

~~~
head: cannot open ‘red’ for reading: No such file or directory
head: cannot open ‘dragon.dat’ for reading: No such file or directory
head: cannot open ‘purple’ for reading: No such file or directory
CGGTACCGAA
AAGGGTCGCG
CAAGTGTTCC
...
~~~