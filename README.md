<h1 align="center">Git Tips</h1>
<p align="center"><strong>A collection of git-related tips, tricks and best practices</strong></p>
<img src='https://github.com/ericat/git-tips/blob/master/topguntocat.png' />
<p align="center">Copycat @<a href="https://octodex.github.com/">Octocats</a></p>

##Table of Contents
- [Git Best Practices](#git-best-practices)
- [Standards](#standards)
  * [Commits](#commits)
    + [Examples](#examples)
  * [Naming Branches](#naming-branches)
- [Setup](#setup)
    + [Configure git to open your default editor on every commit:](#configure-git-to-open-your-default-editor-on-every-commit)
    + [Use a template for your commit messages](#use-a-template-for-your-commit-messages)
    + [Ignore Files](#ignore-files)
- [Git by Task](#git-by-task)
  * [Commit Code](#commit-code)
  * [Stash Code](#stash-code)
  * [Inspect your changes](#inspect-your-changes)
  * [Search Code](#search-code)
      - [Pagination when logging](#pagination-when-logging)
  * [Some Housekeeping](#some-housekeeping)
- [Git Troubleshooting](#git-troubleshooting)
    + [Fix a detached head](#fix-a-detached-head)
    + [Fatal: xx cannot be resolved to branch](#fatal-xx-cannot-be-resolved-to-branch)
- [Git By Example](#git-by-example)
    + [Switch to previous branch](#switch-to-previous-branch)
    + [Use grep](#use-grep)
    + [Abort a merge](#abort-a-merge)
    + [Show file in other git branch](#show-file-in-other-git-branch)
    + [Pick a file from another branch/commit](#pick-a-file-from-another-branchcommit)
    + [Pick a file from another branch/commit (that does not exist in the current branch)](#pick-a-file-from-another-branchcommit-that-does-not-exist-in-the-current-branch)
    + [Pick a file from another branch but rename it](#pick-a-file-from-another-branch-but-rename-it)
    + [Find branches who are not yet merged to develop](#find-branches-who-are-not-yet-merged-to-develop)
    + [Find out which branch contains a specific commit](#find-out-which-branch-contains-a-specific-commit)
    + [See which branch a commit belongs to](#see-which-branch-a-commit-belongs-to)
    + [List all dev working on a project](#list-all-dev-working-on-a-project)
    + [See only meaningful changes without whitespace in diffs](#see-only-meaningful-changes-without-whitespace-in-diffs)
    + [See changed words when editing prose](#see-changed-words-when-editing-prose)
    + [View all global settings](#view-all-global-settings)
    + [Check parent of a merge and file changes](#check-parent-of-a-merge-and-file-changes)
    + [Checking history of a file](#checking-history-of-a-file)
    + [Find out which remote branch a local branch is tracking](#find-out-which-remote-branch-a-local-branch-is-tracking)
    + [Update your remote](#update-your-remote)
    + [Find the commit where the branch was started](#find-the-commit-where-the-branch-was-started)
    + [Add everything but whitespace changes](#add-everything-but-whitespace-changes)
    + [Find a commit that touches a particular snippet of code](#find-a-commit-that-touches-a-particular-snippet-of-code)
    + [Need to remove some files from a previous commit](#need-to-remove-some-files-from-a-previous-commit)
    + [Checkout a new branch from a hash](#checkout-a-new-branch-from-a-hash)
    + [Check if a rebase is in progress](#check-if-a-rebase-is-in-progress)
    + [Checkout only part of a file](#checkout-only-part-of-a-file)
    + [Some JIRA Assistance](#some-jira-assistance)
## Git Best Practices
* Commit early and often
* Keep branches short-lived
* Keep branches up-to-date
* Rebase when possible
* Enforce naming standards

More on [git best practices](https://sethrobertson.github.io/GitBestPractices/#commit).

## Standards
### Commits
* Use consistent casing in the subject line
* Do not end the subject line with a period
* Use imperative mood in commit messages
* Limit the subject line to 50 characters
* Use a body

The commit should look like this:

```
<title>
<BLANK LINE>
<body>
```


#### Examples

Git uses capitalisation and the imperative mood when merging or reverting, so that's what we use:

**Good** `Add validation error msg`

**Bad** `adding validation error msg`


However, some people prefer to use _lowercase_. This works well with _labels_, for example:


```
docs(changelog): update change log to beta.5
```


This is a handy table for labels:

| Label | Description |
| ------ | ------ |
| feat | A new feature |
| fix | A bug fix |
| style | Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc) |
| refactor | A code change that neither fixes a bug nor adds a feature |
| perf | A code change that improves performance |
| test| Adding missing or correcting existing tests |
| chore| Changes to the build process or auxiliary tools and libraries such as documentation generation |
| doc | Documentation only changes |



The above information comes from [Angular's commit standards and guidelines](https://github.com/angular/angular/blob/master/CONTRIBUTING.md).


You should also use a _body_ to explain what the commit does. A good idea is to reference the JIRA / Github issue, for example:

```
fix: validation on text input

This fixes the validation on the text input, broken in commit a05bcd3.

Closes SEWA-104.
```

You can set up your editor to open a standard template on commit. Find instructions [here](https://github.com/ericat/git-tips#Use-a-template-for-your-commit-messages).

### Naming Branches
* Prefix with `feature` or `fix` labels;
* Use lowercase;
* Include JIRA issue;
* Separate words with either slash, underscore or hyphen (avoid mixing and matching...).

**Good** `feat/SEWA-104/react-barcodes`

**Bad** `feat_SEWA_104_React-barcodes_Step-2`

## Setup
#### Configure git to open your default editor on every commit:

```
git config --global core.editor "code --wait"
git config --global core.editor "atom --wait"
git config --global core.editor "subl -n -w"
git config --global core.editor "vim"
```

#### Use a template for your commit messages
Create a file called `~/.gitmessage.txt` in your home directory with the following content:

```
Subject line
<blank line>
Body.
[JIRA-XXX]
```

Tell git to use it:

```
git config --global commit.template ~/.gitmessage.txt
```

#### Ignore Files
You can ignore files locally or globally by adding them to:

* your repo's `.git/info/excludesfile`
* a local `.gitignore`
* your `.gitignore_global` in your home directory

Then point the `core.excludesfile` setting in your `.gitconfig` to it:

```
[user]
	name = Kitty
	email = kitty@ticketmaster.co.uk
[core]
	excludesfile = /Users/kitty/.gitignore_global
```

The `.gitignore_global`:

```
npm-debug.log
node_modules
coverage
.DS_Store
```

## Git by Task
### Commit Code
The first commit of a repository cannot be rebased like regular commits, so
it's good practice to create an empty commit as your repository root:

```
git commit -m "root" --allow-empty
```

Amend the latest message, if you haven't pushed:

```
git commit --amend -m "New commit message"
```

If you forgot to add a file to the latest commit, you can still reuse the same
commit message:

```
git add filename
git commit --amend --no-edit
```

### Stash Code
Useful when something needs a quick fix, but you are not finished
with what you were doing:

```
git add -a

git stash

git stash apply
```

Some cleanup:
```
git stash list
git stash clear
```

This will apply and delete from the stack:
```
git stash pop
```

### Inspect your changes
Diffing code:

```
git diff origin/develop  // see changes that develop does not have

git diff origin/develop <filename> // can also pass a file name

git diff HEAD // compare with staged changes

git diff -w   // see changes without indent changes

git diff --cached // see diffs for files already in the staging area
```

### Search Code
```
git log -3 // show the last 3 commits

git log --after="2014-7-1"

git log --after="yesterday" // and also "1 week ago" or --before
```

A list of examples:

```
git log —oneline

git log -3

git log --author="ericat"

git log -p -S"Math" // code changes that include "Math", the -p also includes the code changes

git log -p -G <regex>

git log --no-merges

git log --grep="PD-6300"

git log —all --grep="PD-6300"

git log --all --oneline --decorate --author="Erica" --since="1.week"

git log --author=“Ericat|Rebecca"

git log — webpack.config.babel.js // show the history of changes for a particular file. Can omit — if there is no risk of mixing it up with a branch

git log master..wip-star-items // see all changes in wip that are not in master.

git shortlog // see history without hashes
```

##### Pagination when logging
When `git log` shows a `:` at the bottom, it means paginated results. You can navigate with:

B (back)
F (forwards)

or simply  j k.

You can also search within the pagination with `/searchterm`

### Some Housekeeping
List all branches that have already been merged into `master`:
```
git branch --merged master
```

Delete them:
```
git branch --merged develop | grep -v 'master$' | xargs git branch -d
```

Delete local branches that have been deleted remotely:

```
git prune
```

Fetch and purge old data, making sure everything is up to date:

```
git fetch -p
```

## Git Troubleshooting
#### Fix a detached head
Simply chekout the current branch. If you are on a detached HEAD from develop, do:

```
git checkout develop
```

#### Fatal: xx cannot be resolved to branch
This may happen if you create a branch with a similar name to another, but with different casing.

For example:

`fix/SEWA-776/ism-tool-tip` and `fix/sewa-776/seatmap-tooltip`

The error you may get:
```
fatal: fix/sewa-776/seatmap-tooltip cannot be resolved to branch.
fatal: The remote end hung up unexpectedly
```

To fix, rename `.git/refs/head/SEWA-776` to `.git/refs/head/sewa-776`.

## Git By Example
#### Switch to previous branch
```
git checkout -
```

#### Use grep
Find a list of files containing a CSS variable with grep

Bonus: open them in vim

```
git grep —name-only \$tint-white | xargs vi
```

#### Abort a merge
```
git reset --hard HEAD
```

Checkout a specific version of a file:

```
git checkout <hash> -- <file_path>
```

#### Show file in other git branch
```
git show fe-tests:test/acceptance/sell.js
```

#### Pick a file from another branch/commit
```
git checkout <hash> -- <path_to_file>
```

#### Pick a file from another branch/commit (that does not exist in the current branch)
```
git checkout <other_branch> — <path_to_file>
```

#### Pick a file from another branch but rename it
```
git show <branch>:<path_to_file> > <new_path_to_file>
```

#### Find branches who are not yet merged to develop
```
git branch --no-merge develop
```

#### Find out which branch contains a specific commit
```
git branch -a —contains <hash>
```

#### See which branch a commit belongs to
```
git log --all --source --oneline
```

#### List all dev working on a project
```
git shortlog

git shortlog -s -n -e

git shortlog -sn // list devs with n of commits
```

#### See only meaningful changes without whitespace in diffs

```
git diff -w
```

This is useful if you suspect Git has been converting line endings.

#### See changed words when editing prose

```
git diff --word-diff
```

#### View all global settings
```
git config --global -l

git config --list
```

#### Check parent of a merge and file changes
```
git show --pretty=raw <hash>
```

#### Checking history of a file
```
git log -- package.json

git blame package.json

git blame -L150 package.json

git blame -L150,+10 package.json
```

#### Find out which remote branch a local branch is tracking
```
git branch -vv
```

#### Update your remote
```
git remote set-url origin <url>
```

#### Find the commit where the branch was started
Visually, through the command line:

```
git log --graph --oneline --all --decorate
```

Through a few other commands:

```
git reflog --date=local | grep branchname

git cherry -v develop // finds the diff between your branch and develop
```

same as:

```
git log --oneline feat/JIRA-687-react-input ^develop

git log develop..master // show all commits that your branch have that are not yet in master
```

#### Add everything but whitespace changes
```
git diff --ignore-all-space | git apply --cached
```

#### Find a commit that touches a particular snippet of code

```
git grep class="ticket-price-variation"
```

The above will output a list of files that contain a particular snippet.

#### Need to remove some files from a previous commit
```
git reset —soft HEAD^
```

#### Checkout a new branch from a hash
If you want to checkout and old version of your code, you can do it in another branch:

```
git checkout -b test-branch 56a4e5c08
```

#### Check if a rebase is in progress
You can check whether a rebase is in process by looking for the directory `.git/rebase-merge/`.

#### Checkout only part of a file
```
git checkout -p (<filename>, optional)
```

When you've committed yet another `console.log` (you could also use a linter :P)...

#### Some JIRA Assistance
Find out what has changed in the past two weeks (sprint goals?):

```
git log --since='2 weeks ago' --oneline
```

What have you done last week? #timesheets

```
git log --all --oneline  --author='Erica' --since='1.week'
```

Grep for a ticket name:

```
git log --grep='PD-6300'

git log —all --grep='PD-6300'
```

