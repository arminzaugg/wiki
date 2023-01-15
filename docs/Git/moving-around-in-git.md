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
- ```git checkout HEAD^2```, moves head one node up to the secondary parent. This can be usefull when navigating through merge commits which have more than one parent and are thus ambigious.

:::note
`git checkout` has been replaced with two new commands because `checkout` did two many things. Everthing `checkout` did, can now be done with `git switch` and `git restore`.
:::


### Reset and Revert

Git reset, ```git reset HEAD^``` does the same as ```git branch -f <branch_name> HEAD^```, assuming one is working on the same branch and HEAD points to the tip of the branch (no detached HEAD). Because one moves backwards in the tree, `git reset` is not suited when working with other people on remote repositories.

For this one should use `git revert`. ```git revert HEAD~2```, appends the relativ commit to the tip of the node as a new commit, so that one move forward in history although its kind of old news.

### Commands for reset and revert
- ```git reset HEAD^```, moves `branch` on commit up/back in the tree.
- ```git revert HEAD^```, creates a copy of the HEAD^ commit and creats a new commit which is forward in history.

### Cherry-pick and interactive rebase

Cherry-pick allows one to make a copy any commit from the repo and attach it to the current `HEAD`.

While `git cherry-pick` is nice if you know exactly which commits you like to copy. Its not ideal if it gets a bit more complex. For that one can use `git rebase -i` which has an interactive mode and displays all the information one needs to complete the task.

As in `git rebase` normal mode the active branch/HEAD gets a new base specified in the command. However instead of creating copies of all intermediary commits one can choose and reorder.

### Commands for cherry-pick and interactive rebase
- ```git cherry-pick <commit_id> <commit_id> etc.```, assuming created commit copies should be attached to the current HEAD.
- ```git rebase -i```, starts interactive rebase.
    
### Use cases for cherry-pick or interactive rebase
- `git cherry-pick` is an easy way to choose which commits should be added to main after a debuging session where only the solution should be in main.
- `git commit --ammnd` can be only applied to the tip of the current branch. So if one has to mess with previous commits, `git rebase -i` is an option to reorder commits so that the one to be amended is on top.
    
### Get some orientation
```git describe <ref>``` will tell you where you at relative to the closest anchor aka tag. The ref can be anything which can be resolved into a commit (branch, HEAD, relative HEAD, commit_id). This is useful if you e.g. came back from holiday. The output looks like `<tag>_<numCommits>_g<hash>`.