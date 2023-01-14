---
title: Moving around in git
---
### Understanding Commits

Commits are the nodes within a repository tree. A single commit consists of all tracked files in the repo at a given commit time and a reference to its parent commit. When a commit happens the respectiv files are zipped and hashed. The hash value is the reference to the commit / commit hashes

HEAD, branch, tags and others are relative links to commit hashes. You can also think about them as aliases.

One can always move to a certain commit hash using ```git checkout <commit_id>```

### Commands to move around

- ```git checkout HEAD^```, moves HEAD one node up.
- ```git checkout HEAD~2```, move HEAD two nodes up.
- ```git checkout <commit_id>```, moves HEAD to specified commit id.
- ```git branch -f <branch_name> <commit_id or relativ HEAD ref>```, points branch to specified commit id.
- ```git switch <branch_name>```, change to branch.

:::note
`git checkout` has been replaced with two new commands because `checkout` did two many things. Everthing `checkout` did, can now be done with `git switch` and `git restore`.
:::


### Reset and Revert

Git reset, ```git reset HEAD^``` does the same as ```git branch -f <branch_name> HEAD^```, assuming one is working on the same branch and HEAD points to the tip of the branch (no detached HEAD). Because one moves backwards in the tree, `git reset` is not suited when working with other people on remote repositories.

For this one should use `git revert`. ```git revert HEAD~2```, appends the relativ commit to the tip of the node as a new commit, so that one move forward in history although its kind of old news.

