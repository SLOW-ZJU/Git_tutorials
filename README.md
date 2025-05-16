# Git Tutorials

## Table of Contents

- [Introduction](#introduction)
- [Get Started](#get-started)
- [Commands](#commands)
- [Useful Tools](#useful-tools)
- [Acknowledgement](#acknowledgement)

## Introduction

This is the official website of [Git](https://git-scm.com/doc). All your questions can be answered here.

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
git config --global init.defaultBranch main
```

Start with a new repository

```bash
mkdir learn_git
cd learn_git
# Set up this folder as a new Git repository.
git init
```

Then use `ls -a` and you can find `.git`, this means your directory `learn_git` is a new Git repository, `.git` stores all Git-related data, including commit history, branches, remote repository information and more.

To remove Git management from this folder, run the following command:

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

Mode|Command|Affects HEAD|Affects Staging Area|Affects Working Directory
:--:|:--:|:--:|:--:|:--:
Soft|`git reset --soft <commit-id>`|✅Yes|❌No|❌No
Mixed(Default)|`git reset --mixed <commit-id>`|✅Yes|✅Yes|❌No
Hard|`git reset --hard <commit-id>`|✅Yes|✅Yes|✅Yes

`--soft`:Only the HEAD pointer is moved, the staging area and working directory remain unchanged
`--mixed`:Only the staging area is reset to the state of the specified commit, while the working directory's file contents remain unchanged.
`--hard`:Both the working directory and staging area will fully match the state of the specified commit.

If you use it incorrectly, don't worry, `git reflog` is your undo button for Git’s local history! `git reflog`  tracks all changes to branch tips and other references (like branches/tags) in your local repository. It’s a safety net for recovering lost commits or branches, even after destructive operations (e.g., reset, rebase, or deleted branches).

Here’s a simple exercise to practice git reset with different modes. Follow the steps to observe how each mode affects your repository.

```bash
cd ~/learn_git/
cp -r test/ soft
cp -r test/ mixed
cp -r test/ hard
cd hard
# Check your commit ID of your first commit.
git log --oneline
# You can inspect your workspace and staging area using commands like git log or git ls-files."
git reset --hard <commit_id> 
cd ~/learn_git/mixed/
git reset --mixed <commit_id>
cd ~/learn_git/soft/
git reset --soft <commit_id>
```

### Remote repository

#### Create SSH Key

```bash
ssh-keygen -t ed25519 -C "your_email"
# It will prompt you for the save path. You can usually accept the default.
# Enter file in which to save the key (/home/yourname/.ssh/id_ed25519):
# View the SSH public key and copy the entire line.
cat ~/.ssh/id_ed25519.pub
```

Log in to GitHub, click your profile picture in the top right corner, then select Settings. In the left sidebar, choose SSH and GPG keys, click New SSH key. Enter a title, and paste the copied public key into the Key field, then click Add SSH key.

#### Add an remote repository

Firstly, log in to GitHub and create a new repository named `learn_git`.

```bash
cd ~/learn_git/test/
# Add a new remote repository to the local repository. 'origin' is the default name,you can change it to whatever you want.
git remote add origin <Your SSH URL>
# Run this command can show all remote repository of the current local repository.
git remote -v
# Push the local branch to the remote repository.
git push -u origin main
# Go to your GitHub repository and click 'Add a README'. Type something randomly and commit it.
# Go back to the terminal and enter the following command：
git pull #git pull fetches changes from the remote repository and merges them into your local branch.
```

The complete syntax should be:

```bash
# Push the local branch to a specific branch on the remote repository.
git push <remote_repo_name> <local_branch_name>:<remote_branch_name>
# Pull 
git pull <remote_repo_name> <remote_branch_name>:<local_branch_name>
```

With the -u option added, Git not only pushes the contents of the local main branch to the new remote main branch, but also sets up a tracking relationship between the local main branch and the remote main branch. This allows future push or pull operations to be simplified.You can use `git push` or `git pull`.

You can also link a local branch to a remote tracking branch as follows:

```bash
git branch --set-upstream-to=<remote_repo_name>/<remote_branch> <local_branch>
```

If you want to remove the association with a remote repository:

```bash
git remote remove <remote_repo_name>
```

#### Clone an exist repository

Only the default branch will be checked out; if you want to check out a specific branch, use `-b` or switch manually.

```bash
git clone <URL>
```

### Branch management

```bash
cd ~/learn_git/test/
# List all branches of current local repository.
git branch
# List all branches of current local repository and remote repository.
git branch -a
# Create a new branch:
git branch <new_branch_name>
# Switch to a specific branch:
git checkout <branch_name> # Or
git switch <branch_name> # (Recommend)
# If you want to delete a branch, run:
git branch -d <branch_name>
```

#### Integrate branch changes

##### Merge

Combines changes from a source branch into a target branch, creating a new merge commit to preserve branch history.

```bash
# Merge the feature branch into the current branch
git merge <feature-branch>
```

##### Rebase

Rewrites commit history by moving the current branch’s commits to the tip of the target branch, resulting in a linear history.

```bash
# Rebase the current branch onto the target branch.
git rebase <target-branch>  
```

##### Visualization

Initial Branch Structure

```
      C1 --- C2 --- C3 (main)
        \
         C4 --- C5 (experiment)
```

After `git merge`:

```
      C1 --- C2 --- C3 -------- M (main)
        \                     /
         C4 ------------ C5 (experiment)
```

After `git rebase`:

```
      C1 --- C2 --- C3 (main)
                     \
                      C4' --- C5' (experiment)
```

#### Other parameters

```bash
# Rename the current branch.
git branch -m <new_name>
# Lists all local branches with latest commit hash and upstream tracking branch.
git branch -vv
# List all branches of remote repository.
git branch -r
# Create a new branch and switch to it.
git checkout -b <new_branch_name> # Or
git switch -c <new_branch_name>
```

## Useful Tools

Visual Studio Code

Lazygit

## Acknowledgement
