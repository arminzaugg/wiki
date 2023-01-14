---
title: Git basics
---
### Understand merge and rebase
Git merge is the usual approch to combine the work of different branches. It is a `special` commit because it has two parents. The basic command is ```git merge <branch_name_source>```, assuming the active branch is the one receiving the input.

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
