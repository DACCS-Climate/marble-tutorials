# Version Control

## Table of Contents
- [Introduction to Git](#intro-git)
- [Setting up a Git Repository](#setup-git)
  - [Setting up using the Graphical User Interface](#setup-git-gui)
  - [Setting up using the Terminal](#setup-git-terminal)
- [Main Areas of the Platform](#main-areas)

## <a id="intro-git"></a>Introduction to Git

Version control is a vital tool

Git is one of the most popular version control systems in use today.

## <a id="setup-git"></a>Setting up a Git Repository 

### <a id="setup-git-gui"></a>Setup Git Repository Using the Graphical User Interface

If there is no Git repository set up you will see the following:

![No Repository Set Menu](images/getting-started/git-no-repo-menu.png)

Click `Initialize Repository` to create a Git repository in the current folder. 

> [!NOTE]
> 
> The current folder is the last one shown in the folder breadcrumb.
> 
> ![Folder Breadcrumb Menu](images/getting-started/folder-breadcrumb.png) 
> 
> For example, if `mypublic` is the last one in the breadcrumb, then `mypublic` is the current folder selected 

Once it is done the left sidebar will show the Git interface.  This is where you will see changes to files in the Git folder.

![Repository Created UI](images/getting-started/git-repo-created.png)

### <a id="setup-git-terminal"></a>Setup Git Repository Using the Jupyter Terminal

Click the Terminal button to start a Terminal session.

![Terminal Icon](images/getting-started/terminal-icon.png)

![Terminal Session Screen](images/getting-started/terminal-session-screen.png)

Check to see that you are in the default folder by executing the `ls` command.

```
ls
```

If you are in the default folder you will see the following subfolders available to you:

![Terminal Default Subfolders](images/getting-started/terminal-default-folders.png)

Navigate into the `notebook_dir` directory.

```
cd notebook_dir
```
You should see the public folders available to you.  These are the same folders seen when clicking the `File Browser` icon.

![Terminal Notebook Dir](images/getting-started/terminal-notebook-dir.png)
![File Browser Default Folders](images/getting-started/file-browser-default-folders.png)

Navigate into the `mypublic` folder, then create a new folder here and then navigate into it.

Substitute `your-folder-name` with a new folder name. 

```
cd mypublic

mkdir your-folder-name

cd your-folder-name
```
Initialize your Git repository

```
git init
```

![Terminal Git Init](images/getting-started/terminal-git-init.png)