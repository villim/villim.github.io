---
title: Switch SourceTree to CLI
layout: post
---

The other day when I were using SourceTree happily, suddenly had a thought, do I still able to work with CLI?

To be honest, I were not sure. Seemed it's not that easy to view all the details like SourceTree -_-||  

So I throw away SourceTree and started working on CLI. Ofcourse it works, just as good as GUI. The difference is, when using CLI you have to memorize a better picture of the repository. But using SourceTree, you are much easier to see all the details in one screen. However, if you understand CLI you can using any GUI tools, whereas not sure.

But I have to say, they are both great! But I decide to use CLI from now on, it seems more healthy for me.

## Prepare

My current Git version is : 2.6.3

If you want to use SourceTree, dont need read anymore, just [download from here](https://www.sourcetreeapp.com/). Windows has slight different with Mac version, Mac one is better.

If you want to use CLI, you need configure Git first. Please check out the other post for [Git Configuration](http://villim.github.io/my-git-configuration/)

## Braches activities
One of the best freature of SourceTree is, you can see all the activities in the main frame. Different color for each branch and you can see the commits.

![SourceTree screenshot](https://www.sourcetreeapp.com/images/sourcetree-hero-mac-log.png)

Lucky, there's a replacement in CLI, called **tig**. Checkout their page [here](https://github.com/jonas/tig).

### Insall tig
```bash
$ brew install tig
```

### Usng tig
```bash
$ cd your-project-dir
$ tig
```

just with 'tig' command you will see the colored picture of all the branches. type in 'h' to see more guide. 

The most I use is, 'd' for Diff View, 'm' for Main View and 'l' for Log View

It's a great took, need keeping eye on it.

## Check Branches 

### Show Branches
```bash
$ cd <your-project-dir>
$ git branch 				#show local branch
$ git branch -r 			#show remote branch
$ git branch -a 			#show all branch
```

### Show Deitaled Branches
```bash
$ git remote show origin
```

Here we can see all the remote branches, and the ones we checkout and their status. ( whether out of date )

### Checkout and Detele Branches
```bash
$ git checkout master   # checkout master branch
$ git checkout -b <branch-name>  # create and switch to a local branch
$ git branch -D/d <branch-name>  #  delete local branch. D means --delete --force
$ git checkout -b <remote-branch-name> origin/<remote-branch-name>  # checkout and switch to a remote branch
$ git push origin --delete <remote-branch-name>  # delete a remote branch
```

### Prune unexisted remote branch
```bash
$ git remote prune origin
$ git fetch -p  # Same function as previous one
```

## Tag
```bash
$ git push --tags   # push local tag to remote
$ git fetch origin tag <tagname> 		# get remote tag
$ git push origin --delete tag <tagname>   # delete remote tag
```

## Stash
```bash
$ git stash  # save working copies to stash
$ git stash list  # view stash
$ git stash apply  # get stashed files
$ git stash branch <branch-name>  # create branch from stash
```

## Other commands
```bash
$ git clean -d [-n | -f]   # clean project, use -n for dry run, -f for force remote
$ git reset  # dierctly delete prvious commit, HEAD move backward
$ git revert  # a new commit with reversed info to delete privious commit, HEAD move forward
```

With these commands, you should be good to conitune CLI now.
