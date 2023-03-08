---
title: Git Interactive Rebase
description: 
published: true
date: 2023-02-17T17:47:21.810Z
tags: git
editor: markdown
dateCreated: 2023-02-17T17:19:33.517Z
---

# Git Interactive Rebase

Git interactive rebase is a more advanced form of rebasing that allows you to selectively edit, delete, or reorder commits in a branch history. This can be useful for cleaning up commit messages, combining related commits, or removing unnecessary changes. Interactive rebase can be a powerful tool for maintaining a clean and organized Git history.

## How to Perform Git Interactive Rebase

To start an interactive rebase, you must first ensure that you are on the branch that you want to rebase. Then, use the following command:

```
git rebase -i <new-base>
```

Where `<new-base>` is the commit you want to set as the new base for the branch. This will open a text editor with a list of all the commits in the branch history.

Each commit will have an action associated with it, such as `pick`, `edit`, `squash`, `fixup`, and others. You can edit the actions to selectively remove, reorder, or combine commits as needed. Once you have made the necessary changes, save and exit the text editor.

## Interactive Rebase Example

Let's say you have a feature branch with several commits that could be cleaned up or combined. To do this, first, switch to the feature branch and use the following command to start an interactive rebase:

```
git rebase -i main
```

This will open a text editor with a list of all the commits in the branch history. You can edit the actions to selectively remove, reorder, or combine commits as needed. For example, you can combine two commits by changing the action for the second commit to `squash`. This will combine the changes made in that commit with the previous commit.

Once you have made the necessary changes, save and exit the text editor. This will re-write the branch history with the changes you made.

> - Interactive rebase can be a powerful tool for maintaining a clean and organized Git history, but it should be used with caution.
> - Changing the commit history of a shared branch can create confusion and issues for other team members.
> - It's important to understand the potential risks and benefits of using interactive rebase before incorporating it into your workflow.

![git-logo.png](/git-logo.png){.align-center}