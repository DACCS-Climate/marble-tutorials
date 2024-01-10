# Introduction to Unix

An introduction to basic Unix shell commands and the file system. This tutorial specifically covers how to use the shell
in a JupyterLab environment.

The shell is a program where users can type commands that are interpreted by the computer. These commands can be simple,
like creating a single file or folder; or complex, like running a complicated analysis on some data. These commands can 
also be combined in unique ways to write specific complex tasks for your computer to execute.

---

## Getting Started

Getting started, select the **terminal** option from the **JupyterLab Launcher**. When loaded, you should a dollar sign
`$` followed by a cursor. The `$` is the symbol used by the shell to indicate the "prompt", where you should write your
commands.

Let's get started with some basic commands.

If you type the following and press enter

```
$ whoami
```

The next line on the screen will display your current username. In a JupyterLab environment on a Marble node, this 
username will not be the same as your Marble username. This is the username used as a general name for everyone using
same JupyterLab image.

In the following sections, we will learn about more commands that help us navigate the file system.

## Directory Navigation

A directory in its simplest definition is a folder holding other folders and/or individual files. A group of files and 
folders that are contained recursively one in another in a tree-like structure are called a filesystem.

Let's take a look at how the filesystem is organised.

On a Unix computer, the filesystem usually looks like something this:

![The File System](https://cdn-wordpress-info.futurelearn.com/info/wp-content/uploads/a2794f8f-b0c1-468d-89c6-bcf29d2d6517-1.png)

At the top is the **root directory** that holds everything else. We refer to it using a slash character `/` on its own.

Inside that directory are several commonly found directories:
- `bin` (which is where some built-in programs are stored),
- `lib` (for the software "libraries" used by different programs),
- `home` (where users' personal directories are located),
- `etc` (system-wide configuration files),
and so on. Remember, deleting files in a Unix environment, can have detrimental effects.

### Printing The Working Directory

Let's find out where we are by running a command called `pwd` (which stands for "print working directory").
At any moment, our **current working directory** is the directory that the computer assumes we want to run commands in 
unless we explicitly specify something else. 

```
$ pwd
/notebook_dir/writable-workspace/.home
```

This response gives us the full path to our current working directory. 

### Listing Directory Contents

Next, you may wish to explore the contents of a folder within the file system. We do this using the `ls`
command which stands for "list":

Using `ls` within our current working directory, you may see something like:

```
$ ls
notebooks  shapefile_datastore 
```

You can also specify a different folder on the file system instead of the current working directory:

```
$ ls /var
backups  cache  lib  local  lock  log  mail  opt  run  spool  tmp
```

Sometimes, the basic `ls` command may yield no results

```
$ ls
$
```

This may be because there are no files in current working directory, but it could also be because some files are hidden.
To see hidden files add the `-a` or `--all` flag to the `ls` command. For example, in your home directory, you may see
lots of hidden files and folders:

```
$ ls -a

.  ..  .bash_history  .cache  .config  .gitconfig  .ipython  .jupyter  .local
```

Note all files here start with `.`, this indicates they are hidden.

There are two special folder names that will be present in all directories: `.` and `..` . These are special references 
to the folder itself and the folder containing the folder itself (or the folder's "parent").

A single `.` will always refer to the folder itself and two `..` will always refer to its parent.

For example, if our current directory is `/notebook_dir/writable-workspace`, then all the following commands will give
identical results as they will all list the contents of the current directory:

```
$ ls
$ ls .
$ ls /notebook_dir/writable-workspace
```

And all the following commands will also give the same result as it will list the contents of the parent of the current 
directory:

```
$ ls ..
$ ls /notebook_dir
```

### Navigating Between Directories

To navigate through the filesystem, use the `cd` command which stands for "change directory".

Let's navigate to the home directory. The `~` symbol refers to the home directory on most systems:

```
$ cd ~
```
 
Remember the hidden directory `..` from the `ls -a` command? We can use that to navigate to the parent of the current 
directory.
For example, if you are currently in `/notebook_dir/writable-workspace`, this command should take you to 
`/notebook_dir`:

```
$ pwd
/notebook_dir/writable-workspace
$ cd ..
$ pwd
/notebook_dir
```

Using the `cd` command without an argument also returns you to the home directory.

We can also use `cd` to specify the path to a specific directory, for example:

```
$ cd
$ pwd
/notebook_dir/writable-workspace/.home

$ cd /notebook_dir/mypublic
$ pwd
/notebook_dir/mypublic
```


## Working with Files and Directories

You would have seen basic ways to navigate through files and directories in Unix. Now, let's make them.

To create a directory, we use the command `mkdir` plus the name of the directory you wish to create.

```
$ ls
Notebook.md   example.ipynb
$ mkdir example_directory
$ ls
example_directory   Notebook.md   example.ipynb
```

Note the `mkdir` yielded no output but when we check for the list of files and directories within the current working 
directory, we see the new directory was created.

## Best Practices for Files and Directories

Complicated names of files and directories can make your life painful when working on the command line. Here we provide 
a few useful tips when naming your files.

1. Don't use whitespace.

   Whitespace can make a name more meaningful but since whitespace is used to break arguments on the command line
   is better to avoid them on name of files and directories. You can use `-` or `_` instead of whitespace.

2. Don't begin the name with `-` (dash).

   Commands treat names starting with `-` as options.

3. Stick with letters, numbers, `.` (period), `-` (dash) and `_` (underscore).

   Many other characters have special meanings on the command line. We will learn
   about some of these during this lesson. There are special characters that can
   cause your command to not work as expected and can even result in data loss.

If you need to refer to names of files or directories that have whitespace or another non-alphanumeric character, you 
should surround the name in quotes (`''`).

Now, let's go to the new directory we have created.


### Creating Files

Let's create a file called `new_file.txt` in this new dictionary using the command `touch`. This will create a new empty
file:

```
$ cd example_directory
$ touch new_file.txt
$ ls
new_file.txt
```

### Deleting Files

Now, let's see how we can remove any files using the `rm` command:

```
$ rm new_file.txt
$ ls
$ 
```

The `ls` command now returns no output.

```{warning} Deleting Is Forever

The Unix shell doesn't have a trash bin that we can recover deleted files from (though 
most graphical interfaces to Unix do).  Instead, when we delete files, they are 
unhooked from the file system so that their storage space on disk can be recycled.
Tools for finding and recovering deleted files do exist, but there's no guarantee
they'll work in any particular situation, since the computer may recycle the 
file's disk space right away.

Note, that the plain `rm` command will not remove directories, only files. To do remove directories and their contents
as well this, we can use the option `-r` or `-R` or `--recursive` which recursively deletes all directories 
and their contents.

Removing the files in a directory recursively can be very dangerous
operation. If we're concerned about what we might be deleting we can
add the "interactive" flag `-i` to `rm` which will ask us for confirmation
before each step

    $ rm -r -i new_file.txt
    rm: remove regular empty file 'new_file.txt'? 

```
## Takeaways

### Key Points:
- The file system is responsible for managing information on the disk.
- Information is stored in files, which are stored in directories (folders).
- Directories can also store other directories, which forms a directory tree.
- `/` on its own is the root directory of the whole file system.
- Directory names in a path are separated with '/' on Unix.
- `..` means 'the directory above the current one'; `.` on its own means 'the current directory'.
- Most files' names are `something.extension`. The extension isn't required, and doesn't guarantee anything, 
but is normally used to indicate the  type of data in the file.
- Most commands take options (flags) which begin with a '-'.

### Key Commands

|**User Action**|**Command**|
|---------------|-----------|
|List| ls *option*|
|Change Directory| cd *option*|
|Print Working Directory| pwd|
|Username| whoami|
|Host name| hostname|
|Make Directory| mkdir *name*|
|Make file| touch *name*|
|Delete| rm *option* *file_path*|
|Remove Directory| rmdir *option* *directory*|
|Move file| mv *old_path* *new_path*|

To learn more about the functions of a command, use `[COMMAND NAME] --help` or  `man [COMMAND NAME]` if the help option 
is not available.  
Online resources are also available to [describe the function of a command](https://explainshell.com).

## Learning More

The goal of this lesson was to familiarize you with the basics of working
with files and directories.
There is a **lot more** to the unix shell and filesystem than what we have covered here!
To ge deeper with self study, we recommend the excellent
[Software Carpentry Unix Shell Lesson](https://swcarpentry.github.io/shell-novice/),
on which the above material was based.
