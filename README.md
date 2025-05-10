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

Start with a new repository

```bash
mkdir learn_git
cd learn_git
# Set up this folder as a new Git repository.
git init
```

then use `ls -a` and you can find `.git` ,this means your directory `learn_git` is a new Git repository, `.git` stores all Git-related data, including commit history, branches, remote repository information and more.

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

Now we create a `test1.txt`

```bash
echo 111 > test1.txt
```

Clone an exist repository

```bash
git clone <URL>
```

## Useful Tools

Visual Studio Code

Lazygit

## Acknowledgement
