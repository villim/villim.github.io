---
title: Git Cherry Pick
layout: post
---

在项目工程中使用代码仓库的时候，有时会出现一种特殊的情况，必须要保留几个独立的分支，它们之间的代码在个别模块有细微的差别，但其他部分总体上又必须保持一致。
     
遇到这个场景，自然会让分支的管理，变得痛苦许多。我们可能需要把一次修改，提交多个分支。譬如改了一个Bug，需要同时提交到所有独立的分支里。Lucky～ 使用的Git的话，可以稍微缓解一点这种痛楚。Git提供了一个功能能，叫做cherry-pick。使用它，至少我们不用手动地自己切换到一个又一个不同分支里，一遍又一遍手动的修改文件，然后分别提交。

比如这个场景，在commit C的时候，我们发布了V1-release。我们的产品依赖于一个第三方的接口，这个release使用第三方v1的版本。

```
A--B--C  ← master ← HEAD
      \--E  ← v1-release (3rd-Party v1)
```

发布完以后，我们继续master的开发，master开始使用第三方v2版本(commit D&F)。而v1-release维持使用第三方v1版本，只需要修改bug, 而且如果这个bug是和第三方v1相关，也并不需要merge回master里面(commit G)。

```
A--B--C--D--F  ← master ← HEAD  (3rd-Party v2)
      \--E--G  ← v1-release (3rd-Party v1)
```

但是master的Commit F是一个通用的Bug Fix，我们需要把它提交到v1-release里面去。这个时候，我们就可以用到cherry-pick了。

```bash
$ git checkout v1-release
$ git cherry-pick F
```
执行的结果就是这样，在v1-release分支上，提交了一个新的Commit H，它的内容更改和Commit F是一模一样的。

```
A--B--C--D--F  ← master ← HEAD  (3rd-Party v2)
      \--E--G--H  ← v1-release (3rd-Party v1)
```

cherry-pick和merge一样，可能需要你解决冲突文件。还有，当你重复cherry-pick一个commit的时候，可能会遇到这个错：

```
Error message
The previous cherry pick was now empty ...
means that changes made by cherry-picked commit are already present in current branch. You probably forgot to checkout correct branch.
```

最后，你还可以放弃终止cherry-pick:

```bash 
git cherry-pick --abort
```