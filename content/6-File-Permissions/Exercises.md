+++
title = "c. Exercises"
weight = 2
chapter = false
+++

#### Checking Permissions

I am logged in as `nelle` and this is my output of `ls -la` command

```
-rw-r--r-- 1 nelle nelle    34 Nov  3 08:40 .profile
```

Will I be able to write into this file?

{{% expand "Solution" %}}
Yes, the user has the read and write permissions so can modify the file
{{% /expand %}}

I am logged in as `adam` and this is my output of `ls -la` command
```
drwxr-xr-x 1 nelle nelle    4096 Oct  3 09:41 Documents
```

Will adam be able to move a file into the documents directory?
{{% expand "Solution" %}}
No Bob belongs to the “others” category, which doesn’t have the write permission on the folder
{{% /expand %}}

#### Changing Permissions

What Permissions will the following command give?
~~~
chmod ugo=rwx
~~~

{{% expand "Solution" %}}
`ugo=rwx` is equivalent to the following permissions : r w x r w x r w x so all permissions for all users.
{{% /expand %}}

What is the command for setting the permissions to r w – r – – – – x
Will adam be able to move a file into the documents directory?

{{% expand "Solution" %}}
~~~
chmod u+rw,g=r,o=x
~~~

We set the user permissions to read (r) write (w), the group permissions to read and other permissions to execute
{{% /expand %}}

#### Tricky Questions

if a directory with ” r w x r w x r w x” permissions is copied using the cp command, will the permissions be the same on the new directory ?
{{% expand "Solution" %}}
No. In order for the permissions to be preserved, you have to run cp with the -p option.
{{% /expand %}}

what is the difference between a lowercase “t” and an uppercase “T” for the sticky bit? (you may have to google this)
{{% expand "Solution" %}}
A lowercase t means that the sticky bit is set whereas an uppercase T means that the sticky bit is set but the execute permission is not set.
{{% /expand %}}
