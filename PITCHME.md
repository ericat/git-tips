# Git: an Octocat's Tale
---
## Git <3:
- Setup |
- Standards |
- Best practices |
- Debugging |
- Common issues |
- Productivity |
---
# Setup
###  config, aliases
---
# Setup: files
`.gitconfig`

`.gitignore`

`.gitignore_global`

`.git/hooks/`
---
## Setup: default editor

In .gitconfig:

```
[core]
  editor = vim
```
+++
`git config --global core.editor "vim"`
---
## Setup: ignoring files

In .gitconfig:

```
[core]
  excludesfile = /Users/ericat/.gitignore_global
```

Useful for node_modules, .DS_Store
---
## Setup: autocorrect

`git config --global help.autocorrect 1`
+++
```
git stassus
WARNING: You called a Git command named 'stassus', which does not exist.
Continuing under the assumption that you meant 'status'
in 0.1 seconds automatically...
On branch master
```
---
## Setup: aliases

- alias g="git status"
- alias gc="git commit"
- alias gp="git push"
- alias gg='git log --oneline --graph --all'

Add to ~/.bash_profile
---
## Standards: naming

Commits:
```
fix: validation on text input

This fixes the validation on the text input, broken in commit a05bcd3.
Closes SEWA-104.
```

vs

```
commit IV
```
+++
Branches:

```
feat/SEWA-104/react-barcodes
```

vs

```
Feature-react_barcodes-Step_1
```
+++
## Search History

`git branch -r | grep "react"`


`git log --grep="screenshot"`

```
commit d39d7cb385ac0cf6e657431b09ad80d6b3a86355
Author: Ericat <erica.salvaneschi@gmail.com>
Date:   Fri Jul 22 16:34:20 2016 +0200

    add phantomjs

    Add sample render page and generating screenshots
```
---
## Best practices: Rebasing
* Linear history (`pull --rebase`)
* Reword / delete / squash commits (`git rebase -i <hash>`)


In case things go wrong:

`git rebase --abort`

`git reset --HARD fa40d8c`
+++
## Rebasing: Rules

- revert on shared branches
- reset, rebase on private branches
---
# Debugging
##  bisect, log, blame
---
## git blame
Quick and dirty way to see the history of a file

`git blame filename`

`git blame -L 10,11 filename`
+++
`git grep '<div class="ticket-price-variation">'`

`git blame filename | grep Erica`
---
## git bisect
`git bisect start HEAD` // your currect code is broken

`git bisect bad` // still broken

`git bisect good` // it works!

`git bisect reset` // I'm done
---
# How To
## Fix Common Issues
---
## Fix a detached HEAD

```
cat .git/HEAD

ref: refs/heads/develop
```
+++
If you are on branch `develop`:

`git checkout develop`
---
## Forgot to add a file

`git add -u`

`git commit --amend --no-edit`
---
## I've lost my changes

`git reflog`
---
## Productivity Tips

`git diff -w`

`git checkout -`

`git checkout --theirs, --ours`
+++
Add / Checkout with `--patch`:

`git checkout -p`

`git add -p`

---
## Git By Example
https://github.com/ericat/git-tips

