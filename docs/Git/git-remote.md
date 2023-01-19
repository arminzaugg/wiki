---
title: Git remote work
---
### Understanding remote basics
You can think of git remotes a backups. They can not be adjusted directly. The only way to interact with them is to sync the state between the local repo and the remote repo.
:::info
If you checkout a remote branch e.g. ```git checkout origin main```, you go into a detached HEAD mode if you commit to it.
:::

### Fetching pushing and pulling
Git fetch does two things and two things only:
1. Download missing data from remote to local if any.
2. Update relativ references e.g. move origin main branch to the new commit.

```git pull``` pull is essentially a short cut for ```git fetch && git merge origin main```. It downloads the remote state with `git fetch` and the creates a new merge commit with its two parents origin main and main.

```git push``` uploads ones work to the remote branch. Think of it as publishing your work.

### Handling diverge history
What if my coworkers have pushed to the repo while I was doing work on my local repo?
:::info
Git only allows to push local changes to remote when local and remote are in sync. This means local work and the remote work must have the same origin parent. This is important because otherwhise the `git pull` instruction would become ambigious.
:::
Thats why always run `git fetch` befor pushing. Rebase when needed.
:::tip
Becase `git fetch; git rebase origin/main main; git push` is so common there is a shorthand for this: `git pull --rebase`
:::

#TODO Create heading on remote arguments













