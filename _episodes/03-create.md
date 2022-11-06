---
title: "Working With Files and Directories"
teaching: 30
exercises: 20
questions:
- "How can I create, copy, and delete files and directories?"
- "How can I edit files?"
objectives:
- "Create a directory hierarchy that matches a given diagram."
- "Create files in that hierarchy using an editor or by copying and renaming existing files."
- "Delete, copy and move specified files and/or directories."
keypoints:
- "`cp [old] [new]` copies a file."
- "`mkdir [path]` creates a new directory."
- "`mv [old] [new]` moves (renames) a file or directory."
- "`rm [path]` removes (deletes) a file."
- "`*` matches zero or more characters in a filename, so `*.txt` matches all files ending in `.txt`."
- "`?` matches any single character in a filename, so `?.txt` matches `a.txt` but not `any.txt`."
- "The shell does not have a trash bin: once something is deleted, it's really gone."
- "Most files' names are `something.extension`. The extension isn't required, and doesn't guarantee anything, but is normally used to indicate the type of data in the file."
- "Depending on the type of work you do, you may need a more powerful text editor than Nano."
---
## Creating directories
We now know how to explore files and directories,
but how do we create them in the first place?

### Step one: see where we are and what we already have
Let's go back to our `shell-lesson-data` directory on the Desktop
and use `ls -F` to see what it contains:

~~~
$ pwd
~~~
{: .language-bash}

~~~
/Users/nelle/Desktop/shell-lesson-data
~~~
{: .output}

~~~
$ ls -F
~~~
{: .language-bash}

~~~
creatures/  data/  molecules/  north-pacific-gyre/  notes.txt  pizza.cfg  solar.pdf  writing/
~~~
{: .output}

### Create a directory

Let's create a new directory called `thesis` using the command `mkdir thesis`
(which has no output):

~~~
$ mkdir thesis
~~~
{: .language-bash}

As you might guess from its name,
`mkdir` means 'make directory'.
Since `thesis` is a relative path
(i.e., does not have a leading slash, like `/what/ever/thesis`),
the new directory is created in the current working directory:

~~~
$ ls -F
~~~
{: .language-bash}

~~~
creatures/  data/  molecules/  north-pacific-gyre/  notes.txt  pizza.cfg
solar.pdf  thesis/  writing/
~~~
{: .output}

Since we've just created the `thesis` directory, there's nothing in it yet:

~~~
$ ls -F thesis
~~~
{: .language-bash}

Note that `mkdir` is not limited to creating single directories one at a time.
The `-p` option allows `mkdir` to create a directory with nested subdirectories
in a single operation:

~~~
$ mkdir -p project/data project/results
~~~
{: .language-bash}

> ## Two ways of doing the same thing
> Using the shell to create a directory is no different than using a file explorer.
> If you open the current directory using your operating system's graphical file explorer,
> the `thesis` directory will appear there too.
> While the shell and the file explorer are two different ways of interacting with the files,
> the files and directories themselves are the same.
{: .callout}

> ## Good names for files and directories
>
> Complicated names of files and directories can make your life painful
> when working on the command line. Here we provide a few useful
> tips for the names of your files and directories.
>
> 1. Don't use spaces.
>
>    Spaces can make a name more meaningful,
>    but since spaces are used to separate arguments on the command line
>    it is better to avoid them in names of files and directories.
>    You can use `-` or `_` instead (e.g. `north-pacific-gyre/` rather than `north pacific gyre/`).
>    To test this out, try typing `mkdir north pacific gyre`and see what directory (or directories!)
>    are made when you check with `ls -F`.
>
> 2. Don't begin the name with `-` (dash).
>
>    Commands treat names starting with `-` as options.
>
> 3. Stick with letters, numbers, `.` (period or 'full stop'), `-` (dash) and `_` (underscore).
>
>
> If you need to refer to names of files or directories that have spaces
> or other special characters, you should surround the name in quotes (`""`).
{: .callout}

### Create a text file
Let's change our working directory to `thesis` using `cd`,
then run a text editor called Nano to create a file called `draft.txt`:

~~~
$ cd thesis
$ nano draft.txt
~~~
{: .language-bash}

> ## Which Editor?
>
> When we say, '`nano` is a text editor' we really do mean 'text': it can
> only work with plain character data, not tables, images, or any other
> human-friendly media. We use it in examples because it is one of the
> least complex text editors. However, because of this trait, it may
> not be powerful enough or flexible enough for the work you need to do
> after this workshop. On Unix systems (such as Linux and macOS),
> many programmers use [Emacs](http://www.gnu.org/software/emacs/) or
> [Vim](http://www.vim.org/) (both of which require more time to learn),
> or a graphical editor such as
> [Gedit](http://projects.gnome.org/gedit/). On Windows, you may wish to
> use [Notepad++](http://notepad-plus-plus.org/).  Windows also has a built-in
> editor called `notepad` that can be run from the command line in the same
> way as `nano` for the purposes of this lesson.
>
> No matter what editor you use, you will need to know where it searches
> for and saves files. If you start it from the shell, it will (probably)
> use your current working directory as its default location. If you use
> your computer's start menu, it may want to save files in your desktop or
> documents directory instead. You can change this by navigating to
> another directory the first time you 'Save As...'
{: .callout}

Let's type in a few lines of text.
Once we're happy with our text, we can press <kbd>Ctrl</kbd>+<kbd>O</kbd>
(press the <kbd>Ctrl</kbd> or <kbd>Control</kbd> key and, while
holding it down, press the <kbd>O</kbd> key) to write our data to disk
(we'll be asked what file we want to save this to:
press <kbd>Return</kbd> to accept the suggested default of `draft.txt`).

<div style="width:80%; margin: auto;"><img alt="screenshot of nano text editor in action"
src="../fig/nano-screenshot.png"></div>

Once our file is saved, we can use <kbd>Ctrl</kbd>+<kbd>X</kbd> to quit the editor and
return to the shell.

`nano` doesn't leave any output on the screen after it exits,
but `ls` now shows that we have created a file called `draft.txt`:

~~~
$ ls
~~~
{: .language-bash}

~~~
draft.txt
~~~
{: .output}

> ## Creating Files a Different Way
>
> We have seen how to create text files using the `nano` editor.
> Now, try the following command:
>
> ~~~
> $ touch my_file.txt
> ~~~
> {: .language-bash}
>
> 1.  What did the `touch` command do?
>     When you look at your current directory using the GUI file explorer,
>     does the file show up?
>
> 2.  Use `ls -l` to inspect the files.  How large is `my_file.txt`?
>
> 3.  When might you want to create a file this way?
>
> > ## Solution
> > 1.  The `touch` command generates a new file called `my_file.txt` in
> >     your current directory.  You
> >     can observe this newly generated file by typing `ls` at the
> >     command line prompt.  `my_file.txt` can also be viewed in your
> >     GUI file explorer.
> >
> > 2.  When you inspect the file with `ls -l`, note that the size of
> >     `my_file.txt` is 0 bytes.  In other words, it contains no data.
> >     If you open `my_file.txt` using your text editor it is blank.
> >
> > 3.  Some programs do not generate output files themselves, but
> >     instead require that empty files have already been generated.
> >     When the program is run, it searches for an existing file to
> >     populate with its output.  The touch command allows you to
> >     efficiently generate a blank text file to be used by such
> >     programs.
> {: .solution}
{: .challenge}

> ## What's In A Name?
>
> You may have noticed that all of Nelle's files are named 'something dot
> something', and in this part of the lesson, we always used the extension
> `.txt`.  This is just a convention: we can call a file `mythesis` or
> almost anything else we want. However, most people use two-part names
> most of the time to help them (and their programs) tell different kinds
> of files apart. The second part of such a name is called the
> **filename extension** and indicates
> what type of data the file holds: `.txt` signals a plain text file, `.pdf`
> indicates a PDF document, `.cfg` is a configuration file full of parameters
> for some program or other, `.png` is a PNG image, and so on.
>
> This is just a convention, albeit an important one. Files contain
> bytes: it's up to us and our programs to interpret those bytes
> according to the rules for plain text files, PDF documents, configuration
> files, images, and so on.
>
> Naming a PNG image of a whale as `whale.mp3` doesn't somehow
> magically turn it into a recording of whale song, though it *might*
> cause the operating system to try to open it with a music player
> when someone double-clicks it.
{: .callout}

## Moving files and directories
Returning to the `shell-lesson-data` directory,

```
cd ~/Desktop/shell-lesson-data/
```
{: .language-bash}

In our `thesis` directory we have a file `draft.txt`
which isn't a particularly informative name,
so let's change the file's name using `mv`,
which is short for 'move':

~~~
$ mv thesis/draft.txt thesis/quotes.txt
~~~
{: .language-bash}

The first argument tells `mv` what we're 'moving',
while the second is where it's to go.
In this case,
we're moving `thesis/draft.txt` to `thesis/quotes.txt`,
which has the same effect as renaming the file.
Sure enough,
`ls` shows us that `thesis` now contains one file called `quotes.txt`:

~~~
$ ls thesis
~~~
{: .language-bash}

~~~
quotes.txt
~~~
{: .output}

One must be careful when specifying the target file name, since `mv` will
silently overwrite any existing file with the same name, which could
lead to data loss. An additional option, `mv -i` (or `mv --interactive`),
can be used to make `mv` ask you for confirmation before overwriting.

Note that `mv` also works on directories.

Let's move `quotes.txt` into the current working directory.
We use `mv` once again,
but this time we'll use just the name of a directory as the second argument
to tell `mv` that we want to keep the filename
but put the file somewhere new.
(This is why the command is called 'move'.)
In this case,
the directory name we use is the special directory name`.` that we mentioned earlier.

~~~
$ mv thesis/quotes.txt .
~~~
{: .language-bash}

The effect is to move the file from the directory it was in to the current working directory.
`ls` now shows us that `thesis` is empty:

~~~
$ ls thesis
~~~
{: .language-bash}

~~~
$
~~~
{: .output}

Alternatively, we can confirm the file `quotes.txt` is no longer present in the `thesis` directory
by explicitly trying to list it:

~~~
$ ls thesis/quotes.txt
~~~
{: .language-bash}

```
ls: cannot access 'thesis/quotes.txt': No such file or directory
```
{: .output}

`ls` with a filename or directory as an argument only lists the requested file or directory.
If the file given as the argument doesn't exist, the shell returns an error as we saw above.
We can use this to see that `quotes.txt` is now present in our current directory:

~~~
$ ls quotes.txt
~~~
{: .language-bash}

~~~
quotes.txt
~~~
{: .output}

> ## Moving Files to a new folder
>
> After running the following commands,
> Jamie realizes that she put the files `sucrose.dat` and `maltose.dat` into the wrong folder.
> The files should have been placed in the `raw` folder.
>
> ~~~
> $ ls -F
>  analyzed/ raw/
> $ ls -F analyzed
> fructose.dat glucose.dat maltose.dat sucrose.dat
> $ cd analyzed
> ~~~
> {: .language-bash}
>
> Fill in the blanks to move these files to the `raw/` folder
> (i.e. the one she forgot to put them in)
>
> ~~~
> $ mv sucrose.dat maltose.dat ____/____
> ~~~
> {: .language-bash}
> > ## Solution
> > ```
> > $ mv sucrose.dat maltose.dat ../raw
> > ```
> > {: .language-bash}
> > Recall that `..` refers to the parent directory (i.e. one above the current directory)
> > and that `.` refers to the current directory.
> {: .solution}
{: .challenge}

## Copying files and directories

The `cp` command works very much like `mv`,
except it copies a file instead of moving it.
We can check that it did the right thing using `ls`
with two paths as arguments --- like most Unix commands,
`ls` can be given multiple paths at once:

~~~
$ cp quotes.txt thesis/quotations.txt
$ ls quotes.txt thesis/quotations.txt
~~~
{: .language-bash}

~~~
quotes.txt   thesis/quotations.txt
~~~
{: .output}

We can also copy a directory and all its contents by using the
[recursive](https://en.wikipedia.org/wiki/Recursion) option `-r`,
e.g. to back up a directory:

```
$ cp -r thesis thesis_backup
```
{: .language-bash}

We can check the result by listing the contents of both the `thesis` and `thesis_backup` directory:

```
$ ls thesis thesis_backup
```
{: .language-bash}

```
thesis:
quotations.txt

thesis_backup:
quotations.txt
```
{: .output}

## Removing files and directories

Returning to the `shell-lesson-data` directory,
let's tidy up this directory by removing the `quotes.txt` file we created.
The Unix command we'll use for this is `rm` (short for 'remove'):

~~~
$ rm quotes.txt
~~~
{: .language-bash}

We can confirm the file has gone using `ls`:

~~~
$ ls quotes.txt
~~~
{: .language-bash}

```
ls: cannot access 'quotes.txt': No such file or directory
```
{: .output}

> ## Deleting Is Forever
>
> The Unix shell doesn't have a trash bin that we can recover deleted
> files from (though most graphical interfaces to Unix do).  Instead,
> when we delete files, they are unlinked from the file system so that
> their storage space on disk can be recycled. Tools for finding and
> recovering deleted files do exist, but there's no guarantee they'll
> work in any particular situation, since the computer may recycle the
> file's disk space right away.
{: .callout}


> ## Using `rm` Safely
>
> What happens when we execute `rm -i thesis_backup/quotations.txt`?
> Why would we want this protection when using `rm`?
>
> > ## Solution
> > ```
> > $ rm: remove regular file 'thesis_backup/quotations.txt'? y
> > ```
> > {: .language-bash}
> > The `-i` option will prompt before (every) removal (use <kbd>Y</kbd> to confirm deletion
> > or <kbd>N</kbd> to keep the file).
> > The Unix shell doesn't have a trash bin, so all the files removed will disappear forever.
> > By using the `-i` option, we have the chance to check that we are deleting only the files
> > that we want to remove.
> {: .solution}
{: .challenge}


If we try to remove the `thesis` directory using `rm thesis`,
we get an error message:

~~~
$ rm thesis
~~~
{: .language-bash}

~~~
rm: cannot remove `thesis': Is a directory
~~~
{: .error}

This happens because `rm` by default only works on files, not directories.

`rm` can remove a directory *and all its contents* if we use the
recursive option `-r`, and it will do so *without any confirmation prompts*:

~~~
$ rm -r thesis
~~~
{: .language-bash}

Given that there is no way to retrieve files deleted using the shell,
`rm -r` *should be used with great caution*
(you might consider adding the interactive option `rm -r -i` or just `rm -ri`).

## Operations with multiple files and directories

Oftentimes one needs to copy or move several files at once.
This can be done by providing a list of individual filenames,
or specifying a naming pattern using wildcards.

> ## Copy with Multiple Filenames
>
> For this exercise, you can test the commands in the `shell-lesson-data/data` directory.
>
> In the example below, what does `cp` do when given several filenames and a directory name?
>
> ~~~
> $ mkdir backup
> $ cp amino-acids.txt animals.txt backup/
> ~~~
> {: .language-bash}
>
> In the example below, what does `cp` do when given three or more file names?
>
> ~~~
> $ ls -F
> ~~~
> {: .language-bash}
> ~~~
> amino-acids.txt  animals.txt  backup/  elements/  morse.txt  pdb/
> planets.txt  salmon.txt  sunspot.txt
> ~~~
> {: .output}
> ~~~
> $ cp amino-acids.txt animals.txt morse.txt
> ~~~
> {: .language-bash}
>
> > ## Solution
> > If given more than one file name followed by a directory name
> > (i.e. the destination directory must be the last argument),
> > `cp` copies the files to the named directory.
> >
> > If given three file names, `cp` throws an error such as the one below,
> > because it is expecting a directory name as the last argument.
> >
> > ```
> > cp: target ‘morse.txt’ is not a directory
> > ```
> > {: .output}
> {: .solution}
{: .challenge}

### Using wildcards for accessing multiple files at once

> ## Wildcards
>
> `*` is a **wildcard**, which matches zero or more  characters.
> Let's consider the `shell-lesson-data/molecules` directory:
> `*.pdb` matches `ethane.pdb`, `propane.pdb`, and every
> file that ends with '.pdb'. On the other hand, `p*.pdb` only matches
> `pentane.pdb` and `propane.pdb`, because the 'p' at the front only
> matches filenames that begin with the letter 'p'.
>
> `?` is also a wildcard, but it matches exactly one character.
> So `?ethane.pdb` would match `methane.pdb` whereas
> `*ethane.pdb` matches both `ethane.pdb`, and `methane.pdb`.
>
> Wildcards can be used in combination with each other
> e.g. `???ane.pdb` matches three characters followed by `ane.pdb`,
> giving `cubane.pdb  ethane.pdb  octane.pdb`.
>
> When the shell sees a wildcard, it expands the wildcard to create a
> list of matching filenames *before* running the command that was
> asked for. As an exception, if a wildcard expression does not match
> any file, Bash will pass the expression as an argument to the command
> as it is.
{: .callout}

> ## List filenames matching a pattern
>
> When run in the `molecules` directory, which `ls` command(s) will
> produce this output?
>
> `ethane.pdb   methane.pdb`
>
> 1. `ls *t*ane.pdb`
> 2. `ls *t?ne.*`
> 3. `ls *t??ne.pdb`
> 4. `ls ethane.*`
>
> > ## Solution
>>  The solution is `3.`
>>
>> `1.` shows all files whose names contain zero or more characters (`*`)
>> followed by the letter `t`,
>> then zero or more characters (`*`) followed by `ane.pdb`.
>> This gives `ethane.pdb  methane.pdb  octane.pdb  pentane.pdb`.
>>
>> `2.` shows all files whose names start with zero or more characters (`*`) followed by
>> the letter `t`,
>> then a single character (`?`), then `ne.` followed by zero or more characters (`*`).
>> This will give us `octane.pdb` and `pentane.pdb` but doesn't match anything
>> which ends in `thane.pdb`.
>>
>> `3.` fixes the problems of option 2 by matching two characters (`??`) between `t` and `ne`.
>> This is the solution.
>>
>> `4.` only shows files starting with `ethane.`.
> {: .solution}
{: .challenge}

> ## Organizing Directories and Files
>
> Jamie is working on a project and she sees that her files aren't very well
> organized:
>
> ~~~
> $ ls -F
> ~~~
> {: .language-bash}
> ~~~
> analyzed/  fructose.dat    raw/   sucrose.dat
> ~~~
> {: .output}
>
> The `fructose.dat` and `sucrose.dat` files contain output from her data
> analysis. What command(s) covered in this lesson does she need to run
> so that the commands below will produce the output shown?
>
> ~~~
> $ ls -F
> ~~~
> {: .language-bash}
> ~~~
> analyzed/   raw/
> ~~~
> {: .output}
> ~~~
> $ ls analyzed
> ~~~
> {: .language-bash}
> ~~~
> fructose.dat    sucrose.dat
> ~~~
> {: .output}
>
> > ## Solution
> > ```
> > mv *.dat analyzed
> > ```
> > {: .language-bash}
> > Jamie needs to move her files `fructose.dat` and `sucrose.dat` to the `analyzed` directory.
> > The shell will expand *.dat to match all .dat files in the current directory.
> > The `mv` command then moves the list of .dat files to the 'analyzed' directory.
> {: .solution}
{: .challenge}

> ## Reproduce a folder structure
>
> You're starting a new experiment and would like to duplicate the directory
> structure from your previous experiment so you can add new data.
>
> Assume that the previous experiment is in a folder called '2016-05-18',
> which contains a `data` folder that in turn contains folders named `raw` and
> `processed` that contain data files.  The goal is to copy the folder structure
> of the `2016-05-18-data` folder into a folder called `2016-05-20`
> so that your final directory structure looks like this:
>
> ~~~
> 2016-05-20/
> └── data
>    ├── processed
>    └── raw
> ~~~
> {: .output}
>
> Which of the following set of commands would achieve this objective?
> What would the other commands do?
>
> ~~~
> $ mkdir 2016-05-20
> $ mkdir 2016-05-20/data
> $ mkdir 2016-05-20/data/processed
> $ mkdir 2016-05-20/data/raw
> ~~~
> {: .language-bash}
> ~~~
> $ mkdir 2016-05-20
> $ cd 2016-05-20
> $ mkdir data
> $ cd data
> $ mkdir raw processed
> ~~~
> {: .language-bash}
> ~~~
> $ mkdir 2016-05-20/data/raw
> $ mkdir 2016-05-20/data/processed
> ~~~
> {: .language-bash}
> ~~~
> $ mkdir -p 2016-05-20/data/raw
> $ mkdir -p 2016-05-20/data/processed
> ~~~
> {: .language-bash}
> ~~~
> $ mkdir 2016-05-20
> $ cd 2016-05-20
> $ mkdir data
> $ mkdir raw processed
> ~~~
> {: .language-bash}
> >
> > ## Solution
> > The first two sets of commands achieve this objective.
> > The first set uses relative paths to create the top-level directory before
> > the subdirectories.
> >
> > The third set of commands will give an error because the default behavior of `mkdir`
> > won't create a subdirectory of a non-existent directory:
> > the intermediate level folders must be created first.
> >
> > The fourth set of commands achieve this objective. Remember, the `-p` option,
> > followed by a path of one or more
> > directories, will cause `mkdir` to create any intermediate subdirectories as required.
> >
> > The final set of commands generates the 'raw' and 'processed' directories at the same level
> > as the 'data' directory.
> {: .solution}
{: .challenge}

> ## Creating Multiple Directories at once
> Bash also supports brace expansion whereby multiple paths can be
> created with a single expression.
> For example to reproduce the folder structure only a single command is needed:
> ~~~
> $ mkdir -p 2016-05-20/data/{raw, processed}
> ~~~
> {: .language-bash}
> As bash expands it to:
> ~~~
> $ mkdir -p 2016-05-20/data/raw 2016-05-20/data/processed
> ~~~
> {: .language-bash}
> This can be useful when creating nested file structures or when creating multiple
> directories quickly.
{: .callout}

{% include links.md %}
