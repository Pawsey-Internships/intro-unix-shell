+++
title = "b. Executable Scripts"
weight = 2
chapter = false
+++

You can avoid having to run you script with `bash middle.sh` by giving the script the execute permission:
```Bash
$ chmod a+x middle.sh
```

Recall from the file permission section that `a+x` means giving the execute permission to the user, group and others.

You will now be able to run you script on the command line with:
```Bash
$ ./middle.sh
```

{{% notice note %}}
#### Text vs. Whatever

We usually call programs like Microsoft Word or LibreOffice Writer "text
editors", but we need to be a bit more careful when it comes to
programming. By default, Microsoft Word uses `.docx` files to store not
only text, but also formatting information about fonts, headings, and so
on. This extra information isn't stored as characters and doesn't mean
anything to tools like `head`: they expect input files to contain
nothing but the letters, digits, and punctuation on a standard computer
keyboard. When editing programs, therefore, you must either use a plain
text editor, or be careful to save files as plain text.
{{%/notice %}}