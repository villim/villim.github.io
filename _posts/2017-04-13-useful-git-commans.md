---
title: Useful Git Commands
layout: post
---

## Check Detailed Content Change 

When error happened, while you debugging, you may want to check how it happened, who commit the change. **BLAME** is a powerful tool:

```bash
# git blame <file_path>
```

But **git blame** will tell you each line is committed at WHEN and  by WHO. But you may want to know more, you want to check exactly how the content is changed. At this time, you can try :

```bash
# git log -p <file_path>
```

## Check Other Brach's File

When working on story branch, need check the master branch's version. 

Of course we can STASH current working directory changes and switch to master branch. Lucky, there's another easy way: 

```bash
# git show master:file_name
```
and you can also diff the difference by:

```bash
git diff master file_name
```
