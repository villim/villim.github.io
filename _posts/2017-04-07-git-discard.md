---
title: Git的撤销
layout: post
---

总的来说，Git的操作都是相当简单的。不过和撤销相关的操作还是会让人有点混乱的感觉。

因为Git有Working Copy，Index和Commit三种状态，因此撤销的操作也会对应到这三个地方。

## (1) Discard Working Directy Files

### 1.1 New file
如果是一个新文件，要撤销，直接删掉就好了。

```bash
rm new_file.txt
```

### 1.2 Git managed files
如果是修改的，已经被版本控制的文件。

```bash
git checkout git_managed_file.txt
```

## (2) Discard Staged Files

当我们把修改后的文件，通过 **Git add** 放到了Index，也就是 Staged Snapshot中后。

```bash
git reset git_managed_file.txt new_file.txt
```

这里有一种特殊情况，是git merge后，要撤销merge的内容:

```bash
git merge --abort
```

## (3) Discard Commited Files

### 3.1 Reset

可以直接重置一个commit或者单个文件。

```bash
git reset --hard HEAD
git reset --hard [hash_commit_id]
git reset HEAD~2 git_managed_file.txt
```

### 3.2 Revert

Revert会撤销一个commit，但是会提交一个新的commit。

```bash
git revert [hash_commit_id]
``` 

## (4) reset, revert & checkout

### 4.1
简单来说，如果要切换到不同分支，使用checkout。当前的Branch和HEAD ref都会更新。

### 4.2
revert只能接受commit作为参数，而不能作用在单独的文件上。如果有人cloned你的工作分支，获取了你的一些commit，这个时候最好选择revert而不是可能改变历史记录的reset或者git commit --amend。

### 4.3
reset不会改变分支，reset的初衷是用来更改HEAD ref。但是当使用hard参数的时候，工作目录也会改变。当撤销某个commit的时候，可以使用下面三个参数。

Option|HEAD|Index|Working Directory
---|---|---|-
--soft|Yes|No|No
--mixed|Yes|Yes|No
--hard|Yes|Yes|Yes

reset默认使用 mixed。当使用soft的时候，staged的文件状态并不会变，可以用来改变commit message。

需要特别注意的是，reset可以改变HEAD ref到其他分支。比如,把HEAD ref从当前master分支指向release分支的：

```bash
git reset --soft release
```
这会导致，你的working directory还是master，可是HEAD ref却跑到release分支去了。需要特别注意，发生奇怪的文件状态。也需要特别注意相对路径，比如HEAD^或者HEAD~,一定要提醒自己HEAD ref到底在什么位置。

当reset针对文件，soft、mixed和hard就不起作用了。因为这时，INDEX(stared status)总是会改变，而working directory永远都不会变。


## (5) 参考

Jon Loeliger- [Version control with Git](https://book.douban.com/subject/5311565/)

Atlassian - [Reset, Checkout, and Revert](https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting)