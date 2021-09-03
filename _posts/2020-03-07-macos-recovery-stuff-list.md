---
title: MacOS Recovery Stuff List
layout: post
---

MacOS is Great for many things, such as **Time Machine**. But unluky, it's not always reliable. 

I only have one SSD for recovery, and the most trustless thing is I never tested the backup. And it's impossible to test for every week's backup  -_- so when the backup file damaged ... The only way is reinstall from scratch.


## Recovery MacOS

Apple provide document: [About macOS Recovery](https://support.apple.com/en-us/HT201314), [Chinesse](https://support.apple.com/zh-cn/HT204904)

![macos-recovery-mode-reinstall](http://villim.github.io/img/2020/macos-recovery-mode-reinstall.jpg)

* Press following Keys, after restarted system and after saw Apple icon release
* Command (⌘)-R : reinstall the version was on your Mac ( Recommend )
* Option-⌘-R : upgrade to the latest version compatible with your Mac
* Shift-Option-⌘-R : install pre-loaded version or still provided close version

## Disable System Integrity Protection

[Disable system integrity protection](http://villim.github.io/user-bin-is-forbidden-in-macos)

## Alfred

Probably the best Mac Power User Tool

1. Sync Dropbox Alfred.sync folder
2. Alfred Preference -> Advanced -> Set preference folder

## Homebrew

https://brew.sh 

## iTerm & ZSH

[ZSH Configuration](http://villim.github.io/replace-bash-with-zsh) 

## VIM

Pull [Vim Configuration](https://github.com/villim/dotvim) from Github

## Git & Maven

Install with Homebrew is most easiest way, but sometime, manually installed is also useful. Add configuration to **.zshrc** or **.bashrc** file.

``` bash
vim ~/.zshrc
source ~/.zshrc
```
with contents:

``` text
export M2_HOME= ~/apache-maven-3.6.1
export PATH=$PATH:$M2_HOME/bin

export GRADLE_HOME= ~/gradle-5.6.4
export PATH=$PATH:$GRADLE_HOME/bin
```

Also need XCode Command Line tool:

```
xcode-select --install
```

if encounter problem, try:

```
sudo xcode-select -switch /
```

## Wall Papers

1. Sync from Dropbox.WallPaper-retina
2. Desktop & Screen Saver -> Add Folder

## Required Apps

###  Programming Tools

* [Vagrant](http://villim.github.io/running-virtualbox-with-vagrant-on-macos)
* Jetbrain Toolbox
* Visual Studio Code
* Wireshark
* Monodraw
* StarUML
* Dash
* MindNode Pro
* GIMP
* Go2Shell
* Dark Mode for Safari

### Reading & Writing

* Byword ( Writting, support Markdown )
* Typora （ Markdown Writting )
* calibre ( Digit Book Format Converter )
* Simple Comic
* iChm ( CHM reader )
* Reeder ( RSS reader )


### System Tools

* Amphetamine ( Screen Saver Tool )
* AppCleaner ( App Uninstaller )
* Handbrake ( Vedios Format Converter )
* The Unarchiver ( Compress Tool )
* LyricsX ( iTunes Lyrics )
* IINA ( Player )
* Tweetbot ( Tweet )
* Maipo ( Weibo )
* Flume ( Instagram )

