+++
title = "c. Wildcards"
weight = 2
chapter = true
+++

## Wildcards

`grep`'s real power doesn't come from its options, though; it comes from
the fact that patterns can include wildcards. (The technical name for
these is **regular expressions**, which
is what the 're' in 'grep' stands for.) Regular expressions are both complex
and powerful. As a taster, we can
find lines that have an 'o' in the second position like this:

```Bash
$ grep -E "^.o" haiku.txt
```

~~~
You bring fresh toner.
Today it is not working
Software is like that.
~~~

We use the `-E` option and put the pattern in quotes to prevent the shell
from trying to interpret it. (If the pattern contained a `*`, for
example, the shell would try to expand it before running `grep`.) The
`^` in the pattern anchors the match to the start of the line. The `.`
matches a single character (just like `?` in the shell), while the `o`
matches an actual 'o'.