---
title: "Git Another Git Process Seems to be Running"
date: "2024-02-08"
tags: ["Terminal"]
---

## Error Happened
In my case, this error happens when I force quit editor when writting commit message using the code editor, or `ctl+d` force quit terminal after running the `lazygit` tui command.

Error Message:
```
Another git process seems to be running in this repository, e.g.
an editor opened by 'git commit'. Please make sure all processes
are terminated then try again. If it still fails, a git process
may have crashed in this repository earlier:
remove the file manually to continue.
```

## Resolution

```
rm -f .git/index.lock;
rm -f .git/COMMIT_EDITMSG;
```
- `.git/index.lock`: When you perform a Git command that edits the index, Git creates a new index. lock file, writes the changes, and then renames the file. The index. lock file indicates to other Git processes that the repository is locked for editing
- `.git/COMMIT_EDITMSG`: This file contains the commit message of a commit in progress. If git commit exits due to an error before creating a commit, any commit message that has been provided by the user (e.g., in an editor session) will be available in this file, but will be overwritten by the next invocation of git commit.


## Reference
- [https://medium.com/fusionqa/another-git-process-seems-to-be-running-in-this-repository-71b2f72fac5c](https://medium.com/fusionqa/another-git-process-seems-to-be-running-in-this-repository-71b2f72fac5c)
- [https://stackoverflow.com/questions/38004148/another-git-process-seems-to-be-running-in-this-repository](https://stackoverflow.com/questions/38004148/another-git-process-seems-to-be-running-in-this-repository)