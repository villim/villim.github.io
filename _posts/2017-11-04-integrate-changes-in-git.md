---
title: Integrate Changes in Git 
layout: post
---
在Git里，“合并”不同分支里的变化，主要有三个命令：merge, rebase and cherry-pick。

对于前两个，Atlassian有很不错的图文详解 [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)。其中 [The Golden Rule of Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing) 非常重要。总的来说，已经非常详尽和明白了，不过这里再稍微归纳一下。

## cherry-pick 

**cherry-pick** 很易理解，单独拎出某一个提交，并重新把它提交到其他某分支上。在多个长生命周期的分支管理时，非常好用。[更多查看之前的文章： Git Cherry Pick](http://villim.github.io/git-cherry-pick)

## Merge

Merge是最安全，最常用，不带任何破坏性的合并手段。它把合并的内容作为新的commit提交进来，不会对当前分支的历史记录有任何破坏。具体使用时，其实有几种不同的情况：Fast-forward, Squash。

### Fast-forward

创建branch以后，master没有新的更新，于是branch是最新的版本，两个分支没有分叉。

```bash
git checkout master
git merge branch
```
用不带参数的merge命令时，Git会默认选择快速合并，直接把HEAD指针指向branch所在的版本。

### Non Fast-forward

还是上面相同的情况下，

```bash
git checkout master
git merge –no-ff test
```

指定了 **-no-ff** 参数以后，虽然master并没有新commit，两分支不冲突，Git还是会把branch里新内容额外提交一次。并且，这个新的commit保留了branch上的commit引用，所以可以看到branch的commit历史记录。

### squash

依旧是上面相同的情况下，

```bash
git checkout master
git merge –squash branch
```
指定参数**squash**的时候，和 -no-ff 是类似的，会额外的生产一个新的commit，但是区别在于，现在不会保留之前branch的引用，导致无法追溯branch上的commit历史记录。从效果看起来，就像是把branch上的多个commit整合为了一个commit。

很显然 squash 的目的就是消除不必要commit日志，让日志看了起来更清爽一些。譬如以branch为基础的开发流程里，一般情况下，我们合并branch到master的时候，并没有必要保留程序员在branch里面琐碎的日志记录，只需要一条简单的日志告诉我们，这个commit完成了什么功能即可。


## Rebase

Merge 最大的问题，就是会额外生产一个commit，在一个长期的开发过程中，可能会让日志看起来不是很“整洁”。使用Rebase便可以去掉这些不必要的信息。

```bash
git checkout branch1
git rebase branch2
```

Rebase的做法是，将合入分支branch2上的多个commit节点，重新依次在branch1分支上提交一遍，整合了两个分支的时间线，保持了一条线性的历史。会让开发过程看起来更清晰流畅。

但因为Rebase改动了当前分支的commit历史，相对来说是不安全的。遵循[The Golden Rule of Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing) 非常最要的!

**The golden rule of git rebase is to never use it on public branches.**

因为rebase过后的public branch，比如说我们操作的是master，只会改变了本地的master，并不会改变remote master，于是其他也在master工作的人，并不会看到这个改变。当我们想直接push当前master到remote repository，会因为冲突被阻止。只能强行绕过：

```bash
git push --force # Be very careful with this command!
```

即使这样强行push成功了，因为改变了master的历史记录，还是会让其他感到莫名其妙，不清楚到底发生了什么。


## When to Merge & Rebase

总的来说 Merge 因该是最可靠，也是最简单易于理解，即使出了错，更容回滚的方式。利用好squash，应该能解决很大一部分无聊日志的问题，对于剩下的情况，我并没有洁癖，即使看到多一些merge的日志，也不是什么大问题。应该成为合并变更的首选。

因为不要使用Rebase操作public branch，所以它的最佳实践可以是，两个工作在相同feature的不同部分，又无法共用branch的开发者，需要相互共享同步代码。这样，既能分开独立地开放，又可以让需要协作的工作，保持清晰的时间线，方便回溯和review。

而cherry-pick是在那种没有办法同步所有代码，只有部分commit需要合并时的唯一选择。