# Command Line

### Introduction

The command line allows users to interact with the programs on a computer through a sequence of linear commands. It is found through the terminal on Mac, or the Ubuntu app for the Windows subsystem for Linux.

Some basic terminology:

* Directory: another name for a folder
* Bash: The command language used on Unix based computers

Commands have the form:

```text
$ command -flag(s) argument(s)
```

The `$` indicates that you are working in the command line of a Unix based system and is not part of the command.

Here's some examples:

```text
$ ls -la
$ mkdir myfolder
$ rm -r myfolder
```

### Basic Commands

`ls` allows you to see the contents of a directory:

```text
$ ls
myfolder1  myfolder2  myfolder3  mytext.txt
```

`cd` changes your directory, and `pwd` prints your working directory:

```text
/home$ pwd
/home
/home$ cd myname
/home/myname$ cd ..
/home$
```

`touch` can easily create new empty files:

```text
$ ls
myfolder
$ touch myfile
$ ls
myfolder myfile
```

`rm` is used to remove objects like files or directories:

```text
$ touch myfile
$ ls
myfolder myfile
$ rm myfile
$ ls
myfolder
```

`mkdir` creates a new directory:

```text
$ mkdir mynewdir
$ ls
mynewdir
```

`cat` can be used to read files:

```text
$ cat mytext.txt
This is the text in mytext.txt
```

`sudo` is a prefix to allow your commands to run with elevated privileges and is usually needed for installations:

```text
$ sudo apt-get update
$ sudo apt-get install python3
```

Vim is a text editor that runs directly through the command line. As someone new to vim, it can used to easily make small text edits or explore text. Vim can also be used as a complete substitute for other text editors like Sublime Text and Notepad++ if enough time is taken to learn all the commands, shortcuts, settings, etc... To use vim, just use the `vim` command with the name of the file you wish to edit/create:

```text
$ vim mycode.py
```

Press `i` to go into vim's insert mode, and text can be added or edited. To get out of vim, press `Esc` to go back into command mode, and then type `:wq` to save changes and quit or `:q!` to quit without saving changes.

### Outside Resources

* [Intro to Linux Terminal](https://www.digitalocean.com/community/tutorials/an-introduction-to-the-linux-terminal)

