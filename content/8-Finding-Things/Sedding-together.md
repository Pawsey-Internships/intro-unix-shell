+++
title = "d. Sedding Together"
weight = 2
chapter = true
+++


## Introduction to the SED Command

`sed` is a command in UNIX that is short for stream editor. `sed` is a powerful tool
for perfoming actions like subsituting (replacing), inserting, and removing data
in files. SED uses pattern matching and also supports regular expressions.
{: .callout}

```Bash
$ man sed
```

Okay, let's try see what we can do with `sed`, first we will try substituting...:

```Bash
$ cd ..
$ sed 's/Horrible/Nicest Person Ever/' notes.txt
```

~~~
- finish experiments
- write thesis
- get post-doc position (pref. with Dr. Nicest Person Ever)
~~~

Let's try something else, how about deleting the third line 
(bottom line in the example) from notes.txt:

```Bash
$ sed "3d" notes.txt
```

~~~
- finish experiments
- write thesis
~~~

Where could you imagine this being useful in a data set?
