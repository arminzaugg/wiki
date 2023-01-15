---
title: Git basics
---
### Understand merge and rebase
Git merge is the usual approch to combine the work of different branches. It is a `special` commit because it has two parents. The basic command is ```git merge <branch_name_source>```, assuming the active branch is the one receiving the input.

Some people think merging branches is not ideal, because the commit history can become messy as all merged branches are visible in the history. An alternativ to that is `git rebase`. The rebase command creates a copy of the commit(s) to be rebased and then attches the copies to the new base (branch). The branch which has beenn rebased then will have an orphan tip. 

One way to accomplish the same thing with `git merge` is to use the `fast-forward` option. However this is only possible when the the commits to be merged follow directly after the origin branch.


### Comands for merging and rebasing
- ```git merge <branch_name_source>```, assuming the active branch should receive the commit.
- ```git merge <branch_name_source> --ff```, does not create a merge commit, only attaches the commits to be received to the orgin branch.
:::info
Think of merge as of `merge specified branch into active branch`. The active branch is alway the one who receives the commit. The `--into-name <branch>` option allows to choose another non-active branch which will then receive the commit.
:::
- ```git rebase <branch_name>```, moves the base/orign of the active branch to the `branch_name`.








:::caution
Better figure out how to use mermaid
:::

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```
