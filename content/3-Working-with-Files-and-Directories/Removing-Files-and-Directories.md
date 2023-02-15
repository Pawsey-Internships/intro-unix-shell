+++
title = "e. Removing Files and Directories"
weight = 2
chapter = true
+++

## Removing files and directories

Returning to the `shell-lesson-data` directory,
let's tidy up this directory by removing the `quotes.txt` file we created.
The Unix command we'll use for this is `rm` (short for 'remove'):

```Bash
$ rm quotes.txt
```

We can confirm the file has gone using `ls`:

```Bash
$ ls quotes.txt
```

```
ls: cannot access 'quotes.txt': No such file or directory
```

{{% notice note %}}
## Deleting Is Forever
The Unix shell doesn't have a trash bin that we can recover deleted
files from (though most graphical interfaces to Unix do).  Instead,
when we delete files, they are unlinked from the file system so that
their storage space on disk can be recycled. Tools for finding and
recovering deleted files do exist, but there's no guarantee they'll
work in any particular situation, since the computer may recycle the
file's disk space right away.
{{% /notice %}}

## Exercise: Using `rm` Safely
What happens when we execute `rm -i thesis_backup/quotations.txt`?
Why would we want this protection when using `rm`?

{{%expand "Solution" %}}
```Bash
$ rm: remove regular file 'thesis_backup/quotations.txt'? y
```

The `-i` option will prompt before (every) removal (use <kbd>Y</kbd> to confirm deletion
or <kbd>N</kbd> to keep the file).
The Unix shell doesn't have a trash bin, so all the files removed will disappear forever.
By using the `-i` option, we have the chance to check that we are deleting only the files
that we want to remove.
{{% /expand %}}


If we try to remove the `thesis` directory using `rm thesis`,
we get an error message:

```Bash
$ rm thesis
```

~~~
rm: cannot remove `thesis': Is a directory
~~~


This happens because `rm` by default only works on files, not directories.

`rm` can remove a directory *and all its contents* if we use the
recursive option `-r`, and it will do so *without any confirmation prompts*:

```Bash
$ rm -r thesis
```

Given that there is no way to retrieve files deleted using the shell,
`rm -r` *should be used with great caution*
(you might consider adding the interactive option `rm -r -i` or just `rm -ri`).