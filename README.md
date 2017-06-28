## Git Best Practices
* Commit early and often
* Keep branches short-lived (merge often)
* Keep branches up-to-date (pull often)
* Rebase when possible
* Enforce naming standards

More on [git best practices](https://sethrobertson.github.io/GitBestPractices/#commit).

## Standards
* Capitalise subject line in commit messages
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

Git uses capitalisation and the imperative mood when merging or reverting, so that's what we use too:

__Good__ `Add validation error msg`

__Bad__ `adding validation error msg`

Some people prefer to use lowercase. This works well with labels, for example:

`docs(changelog): update change log to beta.5`

A handy table for labels:

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

The above information comes from Angular's [commit standards and guidelines](https://github.com/angular/angular/blob/master/CONTRIBUTING.md).

You should also use a body to explain what the commit does. A good idea is to references the JIRA / Github issue, for example:

```
fix: validation on text input

This fixes the validation on the text input, broken in commit a05bcd3.

Closes SEWA-104.
```

You can set up your editor to open a standard template on commit. Find instructions [here](#template).

### Naming Branches
* Prefix with feature or fix labels;
* Use lowercase;
* Include JIRA issue;
* Separate words with either slash, underscore or hyphen (avoid mixing and matching...).

__Good__ `feat/SEWA-104/react-barcodes`

__Bad__ `feat_SEWA_104_React-barcodes_Step-2`

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

`git config --global commit.template ~/.gitmessage.txt`

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

#### Ignore Line Endings

To Add:
gitattributes
hooks
aliases


## Git by Example
<!--https://contegixapp1.livenation.com/confluence/display/RI/Git+Tips-->
Comparing files
  Show history of a file
Finding stuff
Undoing Commits
Debugging

## Productivity Tips
git checkout -
