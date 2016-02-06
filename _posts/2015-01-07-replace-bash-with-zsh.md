---
layout: post
title: Replace Bash with Zsh
tags: Bash, Zsh

---

Have been using Zsh for a while, I do recommend you swith to it. 

But if you ask why? I can just say, Zsh is far far better than Bash, the advantage is everywhere, in all kinds of small details. Just try! and you will findout. 谁用谁知道！

## ZSH

On mac, if you wanna switch to Zsh. You can do:

`Terminal -> Preferences -> Startup -> Shell open with -> check *Command (Complete path)* -> Input ***/bin/zsh***
`

But the best is to replace default shell with:

```bash
chsh -s /bin/zsh
```

<br/>
## OH-MY-ZSH

In order to configure Zsh much easier, suggest using [OH-MY-ZSH](http://villim.github.io/zsh-unreadable-codes/)

Becareful, after change to use Zsh, you should modify file **.zshrc** rather than **.bashrc** anymore. for example, you want to export *JAVA_HOME* by:

```bash
export JAVA_HOME=`/usr/libexec/java_home`
```

<br/>
## ZSH Configure

By the way, */usr/libexec/java_home* is the best way to refer to JDK as Apple recommended. If you installed multi JDK, you can easily swith by 

```bash
export JAVA_HOME=`/usr/libexec/java_home -v 1.6`
```

