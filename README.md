# Git Tutorials

## Table of Contents

- [Introduction](#introduction)
- [Get Started](#get-started)
- [Commands](#commands)
- [Useful Tools](#useful-tools)
- [Acknowledgement](#acknowledgement)

## Introduction

## Get Started

 Download Git for Linux

```bash
sudo apt update
sudo apt install git
```

Configure your Git

`--global` applies to all Git repositories, while `--local` only affects the current one.

```bash
git config --global user.name "Your Name"
git config --global user.email "Your Email"
git config --global core.editor "vim"
```

Start with a new repository

```bash
mkdir learn_git
cd learn_git
# Set up this folder as a new Git repository.
git init
```

Then use `ls -a` and you can find `.git` ,this means your directory `learn_git` is a new Git repository, `.git` stores all Git-related data, including commit history, branches, remote repository information and more.

To remove Git management from this folder,run the following command:

```bash
rm -rf .git
git status
```

Now your directory is no longer under Git version control.

Create a new Git repository.

```bash
# You can add a project name after git init to create the repository in a specific directory.
git init test
cd test
```

## Commands

### Add files to the repository 

Make sure you're in the `learn_git/test` and let's see how to use Git to manage your files.

```bash
# Create a new file
echo 111 > test1.txt
# Check the current repository status, including file modifications, uncommitted changes, and branch information.
git status 
# After running the above command，Git will show your file as untracked.Stage the untracked file for commit using the following command:
git add test1.txt
git status
# Git will mark your file as staged for commit. Use the following command to commit them(The text after -m serves as the commit message.):
git commit -m "first commit"
```

Run `git status`, your working tree should now be clean.

#### Advanced usage

```bash
# Stage all tracked file changes (modifications/deletions), excluding new untracked files.
git add -u
# Stage all changes in the working directory (new, modified, and deleted files).
git add -A #or git add --all
# Only adds files in the current directory.
git add .
# Display the commit history of a repository.(--oneline for compact one-line view)
git log
# This command lists all files that are currently tracked in the repository's staging area or working tree.
git ls-files
```

### Undo changes in Git

```bash
echo 222 > test2.txt
echo 333 > test3.txt
git add test2.txt test3.txt 
git commit -m "second commit"
# This command is used to remove files from Git's tracking index and from the working directory:
git rm test2.txt
# If you want to stop tracking but keep files locally:
git rm --cached test3.txt
git add test3.txt
git commit -m "third commit"
```

If you want to revert to a specific version,use `git reset`.

Mode|Command|Affects HEAD|Affects Staging|Affects Working Dir
:--:|:--:|:--:|:--:|:--:
Soft|`git reset --soft commit_id`|✅Yes|❌No|❌No
Mixed(Default)|`git reset --mixed commit_id`|✅Yes|✅Yes|❌No
Hard|`git reset --hard commit_id`|✅Yes|✅Yes|✅Yes



```bash

```
Clone an exist repository

```bash
git clone <URL>
```

## Useful Tools

Visual Studio Code

Lazygit

## Acknowledgement
