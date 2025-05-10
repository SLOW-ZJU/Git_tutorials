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
# Git will mark your file as staged for commit. Use the following command to commit them:
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
```

#### Summary

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
