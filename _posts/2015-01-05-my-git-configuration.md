---
layout: post
title: My Git Configuration
tags: Git

---

Configure Git isn't difficult, but it's qutie annoying to recall memory each time. This post is just for me to repeat easily next time.

### Install Git

Mac already integrate Git, in case you still don't have it:

```bash
brew install git
```

### Standard Configuration

```bash
git config --global user.name "Villim Wang"
git config --global user.email "xxx@xxx.xx"
git config --global core.editor vim
git config --global merge.tool vimdiff
git config --global color.ui true
```

### Alias Configuration
```bash
git config --global [--system] alias.st status
git config --global [--system] alias.ci commit
git config --global [--system] alias.co checkout
git config --global [--system] alias.br branch
```

### Check Configuration 

```bash
git config --list
```

