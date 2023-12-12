# Version Control

[_Version control_](https://en.wikipedia.org/wiki/Version_control) is a powerful way to organize, back up,
and share with collaborators your research computing code.
A Verson control system keeps track of a set of files and saves snapshots (i.e. _versions_, _commits_) of 
the files at any point in time. Using version control allows you to confidently make changes to your code 
(any any other files), with the ability to roll back to any previous state.

```{contents}
:local:
:depth: 1
```



## Introduction to Git

Git is one of the most popular version control systems in use today. It has a native command line interface but also has 
a desktop GUI client to make using Git simpler.  The online GitHub website allows you to store your repository online and access it anywhere with a free account. 

## Setting up a Git Repository 

[GitHub Desktop Client](https://desktop.github.com/)

### Creating a GitHub Account
To begin using Git you need to create a free account on [GitHub](https://github.com/).  
Go to the GitHub website and follow the instructions to create an account. 

### Creating a Remote Repository

After creating account click `Repository` at the top menu and then `New`

![GitHub Top Menu](images/version-control/github-top-menu.png)

![GitHub New Button](images/version-control/github-new-button.png)

Fill in the form with the details of the repository and click the `Create Repository` button at the bottom of the page.

### Creating a Personal Access Token

A Personal Access Token is used to authenticate the user when pushing files to the remote repository

Go to [GitHub](https://github.com/) and log into your account.

Click on: **Your User Profile** &rarr; **Settings** &rarr; **Developer Settings** &rarr; **Personal Access Token** &rarr; **Generate New Token or Tokens(classic)**

Choose an expiration date.  Check all the boxes in the form.  Click **Generate Token**. Copy the generated token.

```{note}
The Personal Access Token will be shown *only* when it is created.
```

Whenever you push a commit, use the personal access token in place of a password when ask for your GitHub credentials.

```{warning}
Storing personal access tokens or SSH keys in a JupyterLab container poses security risks.  It is recommended to store authentication credentials on your personal computer.
``` 


### Setup Git Repository Using the Graphical User Interface

If there is no Git repository set up you will see the following:

![No Repository Set Menu](images/version-control/git-no-repo-menu.png)

### Adding a Remote Repository

Adding a remote repository allows you to store your work online at GitHub and access it anywhere.

From the menu click `Git` and then select `Add Remote Repository`.  Enter the URL of the repository you created on 
GitHub into the `Add Remote Repository` dialog box.  Click `OK` 

### Creating a Local Repository

```{note}
The repository needs to be in a folder with write permissions enabled.  
 
If you also want the repository to be viewable publically, put it in the `mypublic` folder.  
 
If you want it to be private put it in the `writable-workspace` folder.
```

Click `Initialize Repository` to create a Git repository in the current folder. 


```{note}
The current folder is the last one shown in the folder breadcrumb.
 
![Folder Breadcrumb Menu](images/version-control/folder-breadcrumb.png) 
 
For example, if `mypublic` is the last one in the breadcrumb, then `mypublic` is the current folder selected 
```

Once it is done the left sidebar will show the Git interface.  This is where you will see changes to files in the Git folder.

![Repository Created UI](images/version-control/git-repo-created.png)



### Setup Git Repository Using the Jupyter Terminal

Click the Terminal button to start a Terminal session.

![Terminal Icon](images/version-control/terminal-icon.png)

![Terminal Session Screen](images/version-control/terminal-session-screen.png)

Check to see that you are in the default folder by executing the `ls` command.

```
ls
```

If you are in the default folder you will see the following subfolders available to you:

![Terminal Default Subfolders](images/version-control/terminal-default-folders.png)

Navigate into the `notebook_dir` directory.

```
cd notebook_dir
```
You should see the public folders available to you.  These are the same folders seen when clicking the `File Browser` icon.

![Terminal Notebook Dir](images/version-control/terminal-notebook-dir.png)
![File Browser Default Folders](images/version-control/file-browser-default-folders.png)

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

![Terminal Git Init](images/version-control/terminal-git-init.png)


### Adding a Remote Repository
```
git remote add origin url-of-your-git-repository
```


## Using Git with the Graphical User Interface
By default when you create a new repository you will be using the **master** branch.
This is the main branch where the initial work files will be pushed to and also where the final work version will be.

It is good practice to create work branches from the master branch where all the changes to your work will be done.
Once the changes are complete they can be pushed and merged with the master branch

### Making Your First Commit

Start by creating a file.  In this example a Jupyter Notebook file is created by clicking one of the Jupyter Notebook buttons in the launcher.

![Jupyter Notebook Launcher Buttons](images/version-control/jupyter-notebook-buttons.png)

When the file is created or altered it will be seen under the `Untracked` section in the Git sidebar.

![Git Untracked](images/version-control/git-untracked.png)

### Staging a File

To get the file ready to be committed and pushed, hover the mouse over the file and click the plus `+` symbol next to it.  This **Stages** the file.

![Git Untracked Staged](images/version-control/git-untracked-plus.png)

The file will now appear under the `Staged` section.

![Git Staged](images/version-control/git-staged.png)

### Making a Commit

Select the file and fill in the Title/Summary for the commit.  It should be short and descriptive.  
It can be as simple as "Updated Untitled.ipynb" or more specific, such as "Added visualization for rainfall 2022".

A description is recommended but is not required.

![Git Commit Title](images/version-control/git-commit-title.png)

When done click the `Commit` button below the commit description.  If successful you will see a `Committed changes` status pop up in the lower right corner.

![Git Commit Successful](images/version-control/git-commit-successful.png)

### Pushing a Commit

Making a commit sets a "flag" in the progress of your work that shows what has been done at certain points. Pushing a commit moves these changes to the remote 
repository where they can be merged with the master/main branch.  Up to now no branches have been made.

Click the `Git` menu and `Push to Remote`

![Git Push Menu](images/version-control/git-push-menu.png)

Enter in your login credentials.  For the password enter your Personal Access Token.  Click `OK`.


![Git Push Credentials](images/version-control/git-push-credentials.png)

If successful you will see a `Successfully pushed` status pop up in the lower right corner.

![Push Successful](images/version-control/push-successful.png)


### View the Changes Made Between Versions

There are two ways to view the changes made between versions of a file.

1. Right-click on the file and select `Diff`.  

![Diff Right Click](images/version-control/diff-right-click.png)

2. Enable the double-click shortcut for viewing a `Diff`.  

From the `Git` menu select **"Double click opens diff"**.  A checkmark will appear to show this option is enabled. 
Then double click on the file.

![Diff Double Click](images/version-control/git-menu-diff.png)

The `diff` screen of the file will open and show the changes made to the file.  Areas where changes were made are 
highlighted in red. On the left is the `HEAD` panel and on the right is the `WORKING` panel. 

`HEAD` is the old version of the file.  If additions were made 
there will be green slashes on top of the red highlight.  If there were deletions they will be highlighted in darker 
red on top of the red highlight. 

`WORKING` is the new version of the file.  It shows the final version of the file.  Areas where changes were made are 
highlighted in green.  

![Diff Panel](images/version-control/diff-panel.png)

### Stashing Files

Stashing a file means to temporarily store files you're working on so the changes made to them will not affect other files, 
and changes to other files will not affect the working file.  Stashing is typically done before switching branches, so 
the changes from other branches will not overwrite changes in files you are currently working on.

Currently there is no mechanism in the GUI to stash files.  Files can only be stashed from the Terminal.

[Stash Files from Terminal](#stash-terminal)

Once the command is run all files listed under `Changed` will be moved to the `Stash` and will not be seen. 


### Creating a Branch

Click the down arrow in the `Current Branch` section in the Git sidebar.  It will reveal the `Branches` window and show all the created branches.

Click the `New Branch` button.

![New Branch Button](images/version-control/new-branch-button.png)

Fill out the form and input a branch name, and click which branch to base the new branch off of.  After that click `Create Branch`.

It is good practice to not use spaces or special characters in the branch name other than dashes.


![New Branch Form](images/version-control/new-branch-dialog.png)

Git will automatically switch you into the new branch.  Your newly created branch will be shown under `Current Branch` and be in the list of branches.  

![Create Branch Successful](images/version-control/create-branch-successful.png)


### Switching Branches

```{note}
You can only switch branches when you have no files staged or changed.
 
To switch branches simply click another branch listed under the `Branches` section.
```

```{note}
You can only switch to another local branch.  Branches with the `origin` prefix are remote branches and cannot be switched into.
``` 


## Using Git with the Terminal

### Set Up Your Git Identifier

If you are working in a team this will show who made a certain commit.

```
git config --global user.name "Your Name"
git config --global user.email "email@email.com"
```

### Staging a File

Make sure you are in the same directory as the file you want to stage.

```
git add <filename>
```

### View Staged Files

If you have multiple files staged and ready to commit you can see the list by using `git status`.

```
git status
```


### Making a Commit

Add a brief descriptive message about your commit.

```
git commit -m "your brief commit message goes here"
```

### Pushing a Commit

After your commit is complete, push it to the remote repository.

```
git push
```

### View a History of Commits

To see all the commits made in a repository use ht `log` command.

```
git log
```

### View the Changes Made Between Versions

To view a comparison of the changes between versions of the same file run the `diff` command.

```
git diff
```

### Stashing Files

Make sure you are in the same directory as the file you want to stash.  

Running the `stash` command will stash all files that have changes made to them.

```
git stash
```

To see the files you stashed you can list them: 

```
git stash list
```

To resume working on your stashed files you will need to get them out of the stash.  Run the following command and you will see them under the `Changed` section.

```
git stash pop
```


### Creating a Branch

```
git branch <new-branch-name>
```

### Switching Branches

```{note}
You can only switch branches when you have no files staged or changed.
``` 

Switch branches by checking out the branch.  Replace *<branch-name>* with the branch you want to switch to.

```
git checkout <branch-name>
```

```{note}
You can only switch to another local branch.  Branches with the `origin` prefix are remote branches and cannot be switched into.
``` 

## Creating a Pull Request
A Pull Request is done when you want to merge your changes into the **master**/**main** branch.  It also gives you a chance to let others know of the changes you made and ask them to review your changes.

A Pull Request is done from the GitHub site.  After logging into [GitHub](https://www.github.com), you may see a notification about a branch making recent pushes if you pushed recently.

![GitHub PR Notice](images/version-control/github-pr-notice.png)

Click the `Compare & pull request` button.  

If you don't see a notification, click the `Pull Request` menu button and then the `New Pull Request` button on the following page.

![GitHub PR Menu](images/version-control/github-pr-menu.png)  ![GitHub New PR](images/version-control/github-new-pr.png)

You'll be taken to the `Open a pull request` page.

Here, make sure the `base` is set to **master** and the `compare` is set to the branch you want to compare the **master** branch with.

![GitHub Base Compare](images/version-control/github-base-compare.png)

Fill out the form and provide a title and description of the changes made.  

If you have someone who can review your pull request click the cog icon in the right side of the screen under the `Reviewers` section and select their name.

![GitHub Reviewers](images/version-control/github-reviewers.png)

Then click the `Create Pull Request` button.

## Merging Your Branch
Merging branches is done on the GitHub site.

After your Pull Request has been approved (and reviewed, if needed), the `Merge` button will turn green

![GitHub Merge](images/version-control/github-merge-button.png)


## Git Best Practices

### Organize with Branches

Create a branch for each issue you're working on.  Have one for data ingestion, one for visualization, and one for bug fixes.

This keeps the workflow clean.  If something went wrong you know which branch the changes came from.

### Write Descriptive Commit Messages

A good commit message documents the changes made in the commit so that when looking through the commits you can see the direction your work is going in.

### Commit finished tasks only

Each commit should be a completed logical chunk of the overall workflow.  If you need to commit often, split up the workflow into smaller tasks.

### Test code before committing

Related to only committing finished tasks, test your code to ensure it does what it is intended to do before committing.