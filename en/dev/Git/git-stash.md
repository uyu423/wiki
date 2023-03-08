---
title: Git Stash
description: 
published: true
date: 2023-02-17T17:30:43.629Z
tags: git
editor: markdown
dateCreated: 2023-02-17T17:20:38.575Z
---

# Git Stash

Git stash is a feature in Git that allows you to temporarily save changes that are not ready to be committed. This can be useful when you need to switch to a different branch or work on a different feature without committing your current changes. Stashing changes can help you avoid creating unnecessary commits and keep your Git history clean.

## How to Use Git Stash

To stash changes, use the following command:

```
git stash save
```

This will save your current changes and revert the working directory to the last commit. You can now switch to a different branch or work on a different feature.

To apply stashed changes, use the following command:

```
git stash apply
```

This will apply the changes you stashed and restore the working directory to the state it was in when you stashed the changes.

You can also use the `git stash list` command to view a list of stashes you have made, and the `git stash drop` command to delete a stash.

## Stash Example

Let's say you are working on a feature branch, and you receive a critical bug report that requires immediate attention. You don't want to commit your current changes to the feature branch because they are not yet complete, but you need to switch to the main branch to work on the bug.

To stash your changes, use the following command:

```
git stash save "Work in progress"
```

This will save your changes and revert the working directory to the last commit. You can now switch to the main branch and work on the bug.

Once you have fixed the bug, you can switch back to the feature branch and apply the stashed changes using the following command:

```
git stash apply
```

This will apply the changes you stashed and restore the working directory to the state it was in when you stashed the changes.

> - Stashing changes can be useful for temporarily saving changes that are not ready to be committed, but it's not a substitute for proper version control practices.
> - Relying too heavily on Git stash can make it difficult to track changes and create confusion.
> - Stashing changes that have conflicts can create issues when applying the changes later.

![git-logo.png](/git-logo.png){.align-center}