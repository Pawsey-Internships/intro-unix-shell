+++
title = "b. Changing Permissions"
weight = 2
chapter = true
+++

## Changing Permissions

To collaborate with other users, you may need to change the permissions of a file. The'chmod' command (short for change mode) is the main method of doing this. It has the syntax:

	chmod [references][operator][modes] filename
	
**Note:** There are no spaces between `[references][operator][modes]`.

The `[references]` value specifies which of the three groups you want to modify:
  - **u** for user
  - **g** for group
  - **o** for others
  - any combination of `u`, `g` and `o'.

The `[operator]` value specifies whether you are adding, removing or assigning a permission:
- **‘+’** for adding
- **‘-‘** for removing
- **“=”** for assigning a permission.

Finally, the `[modes]` value specifies the permission (or permissions) to modify:
- **‘r’** read
- **w** write
- **x** execute
- any combination of `r`, `w` and `x`

For example, if `username` would like help debugging `code_for_project.py` from another member of their research group, they may want to add write permissions for users in the `interns0001` group:

```Bash
$ chmod g+w code_for_project.py
```


{{% notice note %}}
## Octal permissions

![Octal file permissions](images/octal-permissions.jpg)
Given that permissions need to be stored for every single file and directory, the storage
costs of this information would quickly grow if not represented efficiently.
Internally file permissions are represented as a bit mask where different permissions correspond to
different set bits. As such a group of three permissions `rwx` can be represented as a decimal number `7`.
As such you may see chmod command that look like:
```Bash
$ chmod 777
```

which is equivalent to

```Bash
$ chmod ugo+rwx
```

You don't need to worry about these at all as the letter permissions are used more often, but it is good to be aware of the history.
{{% /notice %}}
