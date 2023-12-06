# Intro to Git for Version Control

## Overview

[_Version control_](https://en.wikipedia.org/wiki/Version_control) is a powerful way to organize, back up,
and share with collaborators your research computing code.
A Verson control system keeps track of a set of files and saves snapshots (i.e. _versions_, _commits_) of 
the files at any point in time. Using version control allows you to confidently make changes to your code 
(any any other files), with the ability to roll back to any previous state. This help avoid filling our 
directories up with files that look like this:

    my_code.py
    my_code_version2.py
    my_code_version2B-RPA-edit.py
    my_code_FINAL_VERSION.py
    my_code_THIS_IS_ACTUALLY_THE FINAL VERSION.py

Version control also allows you to share code with collaborators, make simultaneous edits, and merge your 
changes in a systematic, controlled way.

Version control also allows you to share code with collaborators, make simultaneous edits, and merge your 
changes in a systematic, controlled way.

Version control has been used for a long time in software development.
More recently, it has become an essential part of modern data and computational science.
Our strong recommendation is that _all of your research code be stored in a version control system_.

The tool we will be using for version control is called [Git](https://git-scm.com).
Git is incredibly powerful--it also has a somewhat steep learning curve.
Fortunately, in this class, we will only be using a small subset of what git can do, avoiding the more 
complex aspects.

*For a full-length tutorial, we recommend the article [Version Control with Git](http://swcarpentry.github.io/git-novice/) 
on Software Carpentry website.*
Here we simply enumerate the most common git commands.

## Summary of useful Git commands

Set up your username and email to identify yourself.
This username and email will be used to identify,
who made changes to any managed files.

    git config --global user.name "Your Name"
    git config --global user.email "email@email.com"

To initialise a new Git repository, first navigate to the directory containing the files you wish managed and 

    $ git init
    hint: Using 'master' as the name for the initial
    branch. This default branch name
    hint: is subject to change. To configure the
    initial branch name to use in all
    hint: of your new repositories, which will
    suppress this warning, call:
    hint: 
    hint:   git config --global init.defaultBranch <name>
    hint: 
    hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
    hint: 'development'. The just-created branch can be renamed via this command:
    hint: 
    hint:   git branch -m <name>
    Initialized empty Git repository in /notebook_dir/mypublic/Tutorial/.git/      

Stage files for addition to the repository:

    git add <filename>

Commit staged files:


    git commit -m "your brief commit message goes here"

Get information about your repository:

    git status    # tells you what files are staged, which ones have been modified, are new,... )
    git log       # view the commit log
    git diff      # view file content differences


Revert a file to an earlier version:

    git checkout <commit tag> <filenames>


Git is useful but many times, we are collaborating with others on projects. This is where a service
like GitHub comes into play. 

To sync with remote repositories such as one on GitHub, we use the `git remote` command.

    git remote add <name> <url>

This command in conjunction with others such as `git fetch`, `git push` and `git pull`, allows for easier collaboration 
between teams. 











    