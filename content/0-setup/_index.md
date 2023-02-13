+++
title = "Setup"
weight = 1
chapter = true
+++

# Setup

{{%attachments style="grey" /%}}

## 1. Download files

- Download the attached [shell-lesson-data.zip (CHECK!)](https://pawsey-internships.github.io/intro-unix-shell/0-setup/_index.files/shell-lesson-data.zip) and move it to your Desktop.
- Unzip/extract the file.
   **Let your instructor know if you need help with this step**.
   You should end up with a new folder called **`shell-lesson-data`** on your Desktop.

## 2. Install software
If you do not already have the shell software installed, you will need to
[download and install](https://carpentries.github.io/workshop-template/#shell) it.

## 3. Open a new shell

- After installing the software, open a terminal.
   If you're not sure how to open a terminal on your operating system, see the instructions below.
- In the terminal type `cd` then press the <kbd>Return</kbd> key.
   This step will make sure you start with your home folder as your working directory. In the lesson, you will find 
   out how to access the data files in this folder.

{{% notice note %}}
Where to type commands: How to open a new shell

The shell is a program that enables us to send commands to the computer and receive output.
It is also referred to as the terminal or command line.

Some computers include a default Unix Shell program.
The steps below describe some methods for identifying and opening
a Unix Shell program if you already have one installed.
There are also options for identifying and downloading a Unix Shell program,
a Linux/UNIX emulator, or a program to access a Unix Shell on a server.

If none of the options below address your circumstances,
try an online search for: Unix shell [your computer model] [your operating system].
{{% /notice %}}

{{< tabs groupID="accessing-shell">}}

{{% tab name="Windows" %}}
Computers with Windows operating systems do not automatically have a Unix Shell program
installed.
In this lesson, we encourage you to use an emulator included in [Git for Windows][install_shell],
which gives you access to both Bash shell commands and Git.

Once installed, you can open a terminal by running the program Git Bash from the Windows start
menu.

**For advanced users:**

As an alternative to Git for Windows you may wish to [Install the Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
which gives access to a Bash shell command-line tool in Windows 10.

Please note that commands in the Windows Subsystem for Linux (WSL) may differ slightly
from those shown in the lesson or presented in the workshop.
{{% /tab %}}

{{% tab name="MacOS" %}}
For a Mac computer running macOS Mojave or earlier releases, the default Unix Shell is Bash.
For a Mac computer running macOS Catalina or later releases, the default Unix Shell is Zsh.
Your default shell is available via the Terminal program within your Utilities folder.

To open Terminal, try one or both of the following:
* In Finder, select the Go menu, then select Utilities.
  Locate Terminal in the Utilities folder and open it.
* Use the Mac 'Spotlight' computer search function (<kbd>⌘</kbd> + <kbd>space</kbd>).
  Search for: `Terminal` and press <kbd>Return</kbd>.

To check if your machine is set up to use something other than Bash,
type `echo $SHELL` in your terminal window.

If your machine is set up to use something other than Bash,
you can run it by opening a terminal and typing `bash`.
  (<b>Note</b> this will only change your shell for the current window/session.)

[How to Use Terminal on a Mac](http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/))
{{% /tab %}}

{{% tab name="Linux" %}}
The default Unix Shell for Linux operating systems is usually Bash.
On most versions of Linux, it is accessible by running the
[Gnome Terminal](https://help.gnome.org/users/gnome-terminal/stable/) or [KDE Konsole](https://konsole.kde.org/) or [xterm](https://en.wikipedia.org/wiki/Xterm),
which can be found via the applications menu or the search bar.
If your machine is set up to use something other than Bash,
you can run it by opening a terminal and typing `bash`.
{{% /tab %}}
{{< tabs >}}

