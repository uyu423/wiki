---
title: Git Cherry-picking
description: 
published: true
date: 2023-02-17T17:27:52.482Z
tags: git
editor: markdown
dateCreated: 2023-02-17T17:18:25.616Z
---

# Git Cherry-picking

Git cherry-picking is a technique for applying individual commits from one branch to another. This can be useful when you want to incorporate a specific change from one branch into another without merging the entire branch. It's a great way to apply hotfixes or critical patches to a production branch without bringing in unwanted changes.

## How to Perform Git Cherry-picking

To cherry-pick a commit, you must first identify the hash of the commit you want to apply. You can do this by using the `git log` command to view the commit history:

```
git log
```

Once you have identified the hash of the commit, switch to the branch you want to apply the commit to, and use the following command:

```
git cherry-pick <commit-hash>
```

Where `<commit-hash>` is the hash of the commit you want to apply. This will apply the changes made in that commit to the current branch.

## Cherry-picking Example

Let's say you have a feature branch with several commits, and you want to apply one of those commits to the master branch. To do this, first, identify the hash of the commit you want to apply using `git log`:

```
git log
```

Assuming the hash of the commit is `abc123`, switch to the master branch and use the following command to cherry-pick the commit:

```
git cherry-pick abc123
```

This will apply the changes made in that commit to the master branch.

> - Cherry-picking can be useful for applying specific changes, but it can also bring in unwanted changes if not used carefully.
> - Cherry-picking a commit that has dependencies on other changes in the branch can create conflicts and make it difficult to track down bugs.
> - Cherry-picking should be used sparingly and with caution.

![git-logo.png](/git-logo.png){.align-center}