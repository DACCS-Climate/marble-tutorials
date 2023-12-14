# Intro to Unix

An introduction to basic Unix commands and the file system.

*The following notes are modications of both the book [An Introduction to Earth and Environmental Data Science](https://earth-env-data-science.github.io/intro.html) by Ryan Abernathey and the [Unix Shell tutorial ](http://swcarpentry.github.io/shell-novice/) that is freely available on the Software Carpentry website. It is recommended that readers take a look at the original works for further readings. The material is being used here under the terms of the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/).*

---

## File and Directory Navigation

In a unix environment, everything is considered a file.

### Getting Started

Getting started, select the **terminal** option from the **JupyterLab Launcher**. When loaded, you should see
something like this.

~~~
jovyan@97d07e419e83:~$
~~~


The **~** tells us we are in the home directory while the **$** tells us the shell is awaiting an input. The **username**
is `joyvan` and the **hostname** is `97d07e419e83`. Because we are using JupyterHub on the cloud, we all have the same username
("jovyan" = resident of the planet Jupyter). However, we each have a different hostname (the name of the computer we are using),
which corresponds to a "virtual machine" running in the cloud. From now on, we will just use a **$** to indicate the prompt.

While the username will always be the same for all Marble users, it is still good to know how to find out your username.

*Try*

~~~
$ whoami
jovyan
~~~

and to find out your hostname

~~~
$ hostname
97d07e419e83
~~~

### Directories

A directory in its simplest definition is a folder holding other folders and/or individual files. The home directory is the 
directory or folder commonly given to a user on a network or Unix or Linux variant operating system. With the home directory 
the user can store all their personal information, files, login scripts, and user information.

Let's take a look at how the filesystem is organised 

On a Unix computer, the filesystem looks like something this:

![The File System](https://cdn-wordpress-info.futurelearn.com/info/wp-content/uploads/a2794f8f-b0c1-468d-89c6-bcf29d2d6517-1.png)

At the top is the **root directory** that holds everything else. We refer to it using a slash character `/` on its own.


Inside that directory are several other directories:
- `bin` (which is where some built-in programs are stored),
- `lib` (for the software "libraries" used by different programs),
- `home` (where users' personal directories are located),
- `etc` (system-wide configuration files),
and so on. Remember, everything is a file, deleting files in a Unix environment, can have detrimental effects.

### Printing The Working Directory

Let's find out where we are by running a command called `pwd` (which stands for "print working directory").
At any moment, our **current working directory** is our current default directory, i.e., the directory 
that the computer assumes we want to run commands in unless we explicitly specify something else. 

~~~
$ pwd
/notebook_dir/writable-workspace/.home
~~~

Here, the terminal's response is `/notebook_dir/writable-workspace`, which indicates where are currently within the
`writable-workspace` folder which itself is located within `notebook_dir` which is all under the `/` or **home directiory**.

### Listing Directory Contents

Next, you may wish to explore the contents of a folder within the file system. We do this using the `ls`
command which stands for "listing":

Using `ls` within our current working directory
~~~
$ ls
notebooks  shapefile_datastore 
~~~

Sometimes, the basic `ls` command may yield no results, especially if you are located within your home directory 
~~~
$ ls
$
~~~

This is because files may be hidden, to see these hidden files we the option `-a` or `--all` which
gives us

~~~
$ ls -a

.  ..  .bash_history  .cache  .config  .gitconfig  .ipython  .jupyter  .lesshst  .local  .npm  .python_history
~~~

Note all files here start with `.`, this indicates they are hidden.

`ls` has many other options. To learn about these options, we can used the `--help` modifier:

~~~
$ ls --help

Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options too.
  -a, --all                  do not ignore entries starting with .
  -A, --almost-all           do not list implied . and ..
      --author               with -l, print the author of each file
  -b, --escape               print C-style escapes for nongraphic characters
      --block-size=SIZE      with -l, scale sizes by SIZE when printing them;
                               e.g., '--block-size=M'; see SIZE format below
   ...
~~~

### Navigating Between Directories

To navigate through the filesystem, there is the `cd` command which stands for "change directory". Note, this commmand
doesn't actually change the directory just the shell's idea of what directory we are in.

Let's navigate to the home directory
~~~
$ cd ~
~~~
 
Remember the hidden directory `..` from the `ls -a` command? 
`..` is a special directory name meaning "the directory containing this one", or more succinctly,
the **parent** of the current directory. In Marble, this command should take you to `/notebook_dir/writable-workspace` 
if you are currently in the home directory, otherwise you will move one level up in the hierarchy. 

~~~
$ cd ..
$ pwd
/notebook_dir/writable-workspace
$ cd ..
$ pwd
/notebook_dir
~~~

Indicating the parent directory in Marble is `/notebook_dir/writable-workspace`.

Using the `cd` command without an argument also returns you to the home directory.

We can also specify the path to the directory wish, for example:

~~~
/notebook_dir/writable-workspace$ cd
~$ pwd
/notebook_dir/writable-workspace/.home
~~~
~~~
~$ cd /notebook_dir/mypublic
 $ pwd
 /notebook_dir/mypublic
~~~


## Working with Files and Directories

You would have seen basic ways to navigate through files and directories in Unix. Now, let's make them.

To create a directory, we use the command `mkdir` plus the name of the directory you wish to create.

~~~
/notebook_dir/mypublic$ mkdir example_of_directory
/notebook_dir/mypublic$ ls
'Environment'   example_of_directory   Marble.md   Plan.ipynb
~~~

Note the `mkdir` yielded no output but when we check for the list of files and directories within the current working directory, 
we see `example_of_directory` was created. 
Be aware that the `mkdir` command makes the new directory within your current working directory. Ensure you create the directory in 
the correct location.

## Best Practices for Files and Directories

 Complicated names of files and directories can make your life painful
 when working on the command line. Here we provide a few useful
 tips for the names of your files.

 1. Don't use whitespaces.

   Whitespaces can make a name more meaningful but since whitespace is used to break arguments on the command line
   is better to avoid them on name of files and directories. You can use `-` or `_` instead of whitespace.

 2. Don't begin the name with `-` (dash).

    Commands treat names starting with `-` as options.

 3. Stick with letters, numbers, `.` (period), `-` (dash) and `_` (underscore).

    Many other characters have special meanings on the command line. We will learn
    about some of these during this lesson. There are special characters that can
    cause your command to not work as expected and can even result in data loss.

 If you need to refer to names of files or directories that have whitespace
 or another non-alphanumeric character, you should surround the name in quotes (`""`).

 Now, let's go to the new directory we have created.

### Autocompleting Inputs
Assuming you made a directory called `example_of_directory`, then type:

~~~
$ cd ex<TAB>
~~~

Where `<TAB>` refers to the **TAB button** on your keyboard. This will auto-input `example_of_directory`.

~~~
$ pwd
/notebook_dir/mypublic/example_of_directory
~~~

### Creating Files
Let's create a file called `new_file.txt` in this new dictionary using the command `touch`.

~~~
/example_of_directory$ touch new_file.txt
/example_of_directory$ ls
new_file.txt
~~~

### Deleting Files

Now, let's see how we can remove any files using the `rm` command:

~~~
$ rm new_file.txt
$ ls
$ 
~~~

The `ls` command now returns no output. 

#### Deleting Is Forever

The Unix shell doesn't have a trash bin that we can recover deleted files from (though 
most graphical interfaces to Unix do).  Instead, when we delete files, they are 
unhooked from the file system so that their storage space on disk can be recycled.
Tools for finding and recovering deleted files do exist, but there's no guarantee
they'll work in any particular situation, since the computer may recycle the 
file's disk space right away.

Note, `rm` can only remove files with only remove files in the current working 
directory. `rm`, alone, cannot remove directories. To do this, we can use 
the option `-r` or `-R` or `--recursive` which recursively deletes all directories 
and their contents.

### With Great Power Comes Great Responsibility

 Removing the files in a directory recursively can be very dangerous
 operation. If we're concerned about what we might be deleting we can
 add the "interactive" flag `-i` to `rm` which will ask us for confirmation
 before each step

~~~
 $ rm -r -i new_file.txt
 rm: remove regular empty file 'new_file.txt'? y
~~~

## Takeaways

### Key Points:
- The file system is responsible for managing information on the disk.
- Information is stored in files, which are stored in directories (folders).
- Directories can also store other directories, which forms a directory tree.
- `/` on its own is the root directory of the whole file system.
- A relative path specifies a location starting from the current location.
- An absolute path specifies a location from the root of the file system.
- Directory names in a path are separated with '/' on Unix, but '\\\\' on Windows.
- '..' means 'the directory above the current one'; '.' on its own means 'the current directory'.
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
|Move file| mv *old_path* *new_path*|

To learn more about the functions of a command, use `command --help` 
Online resources are also available to [describe the function of a command](https://explainshell.com).

## Learning More

The goal of this lesson was to familiarize you with the basics of working
with files and directories.
There is a **lot more** to the unix shell and filexsystem than what we have  covered here!
To ge deeper with self study, we recommend the excellent
[Software Carpentry Unix Shell Lesson](https://swcarpentry.github.io/shell-novice/),
on which the above material was based.