---
title: "Lazigit Interactive-Rebase (e) - [PENDING]"
date: "2024-04-26"
tags: ["Terminal"]
---

![2024-04-26T152158](2024-04-26T152158.jpg)

**PENDING TO COMPLETE**



## Steps Overview

1.   Boot lazygit cli, and navigate to the <u>panel-3</u>, where the commits are located ([screenshot](2024-04-26T152347.jpg))
2.   Use the key `e` to enter <u>interactive rebase mode</u> ([screenshot](2024-04-26T152511.jpg))
3.   You can then use different keys to toggle <u>rebase options</u> for each commit ([screenshot](2024-04-26T153203.jpg))
4.   Use the key `m` to show rebase option, and <u>choose `c` to continue rebase </u> ([screenshot](2024-04-26T153430.jpg))



## Rebase Options

##### pick (`p`)

>    `pick` simply means that the commit is included. Rearranging the order of the pick commands changes the order of the commits when the rebase is underway. If you choose not to include a commit, you should delete the entire line.

##### fixup (`f`)

>   This is similar to `squash`, but the commit to be merged has its message discarded. The commit is simply merged into the **commit above it**, and the **earlier commit's message is used** to describe both changes.

##### squash (`s`)

>    This command lets you combine two or more commits into a single commit. A commit is squashed into the **commit above it.** Git gives you the **chance to write a new commit message** describing both changes.

##### edit (`e`)

>   If you choose to `edit` a commit, you'll be given the chance to amend the commit, meaning that you can add or change the commit entirely. You can also make more commits before you continue the rebase. This allows you to split a large commit into smaller ones, or, remove erroneous changes made in a commit.

##### reword (`r`)

>   The `reword` command is similar to `pick`, but after you use it, the rebase process will pause and give you a chance to alter the commit message. Any changes made by the commit are not affected.

##### reoder (`<c-j>`/`c-k`)

>   As its name claims, change the order of the commits, but be really **careful** on using this one, as the change of git commit order **might result in conflit**. Only do use this git rebase option when the two commit are almost completly irrelevant.



## Reference

-   https://docs.github.com/en/get-started/using-git/about-git-rebase
-   https://stackoverflow.com/questions/45563865/what-does-pick-in-gits-interactive-rebase-do
