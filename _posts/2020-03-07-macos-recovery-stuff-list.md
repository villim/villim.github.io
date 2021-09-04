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

## Try VPN Applicatin first !!!

If VPN application not working new current MacOS, we must solve it first before continue !!

## Alfred

Probably the best Mac Power User Tool

1. Sync Dropbox Alfred.sync folder
2. Alfred Preference -> Advanced -> Set preference folder


## iTerm & ZSH

[ZSH Configuration](http://villim.github.io/replace-bash-with-zsh) 

## Homebrew

Install from [here](https://brew.sh ), and then run with command line:

``` brew install exiftool htop  youtube-dl openjdk zsh tig rpm nmap wget unrar aria2 tree ```

## Config VIM

Following [Vim Configuration](https://github.com/villim/dotvim) from Github

## Java & Git & Maven

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

export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_171.jdk/Contents/Home
export PATH=$JAVA_HOME/bin:$PATH
```

When installing Java, if encounter ```Could not find tools.jar``` problem, check [here](https://stackoverflow.com/questions/64968851/could-not-find-tools-jar-please-check-that-library-internet-plug-ins-javaapple/65211651#65211651)

## XCode Command Line tool

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

* [Beyond Compare](https://scootersoftware.com)
* Dark Mode for Safari
* [Dash](https://kapeli.com/dash)
* [Docker](https://www.docker.com/products/docker-desktop) 
* [GIMP](https://www.gimp.org)
* [Go2Shell](https://zipzapmac.com/Go2Shell)
* [Jetbrain Toolbox](https://www.jetbrains.com/toolbox-app/) 
* Java JDK 
* [Monodraw](https://monodraw.helftone.com)
* MindNode Pro
* Microsoft Remote Desktop Beta
* [MacVim](https://macvim-dev.github.io/macvim/)
* [Postgres](https://www.postgresql.org/download/)
* [Postman](https://www.postman.com/downloads/)
* [StarUML](https://staruml.io)
* [SourceTree](https://www.sourcetreeapp.com)
* [SoapUI](https://www.soapui.org)
* [SQLDeveloper](https://www.oracle.com/cn/tools/downloads/oracle-sql-developer-download.html)
* [Visual Studio Code](https://code.visualstudio.com)
* [Vagrant](http://villim.github.io/running-virtualbox-with-vagrant-on-macos)
* [Wireshark](https://www.wireshark.org)

### Reading & Writing

* [Byword](https://www.bywordapp.com) ( Writting, support Markdown )
* [calibre](https://calibre-ebook.com) ( Digit Book Format Converter )
* Day One ( Dirary Writting )
* iChm ( CHM reader )
* Kindle
* Microsoft Office
* [Pocket](https://getpocket.com)
* [Reeder](https://www.reederapp.com) ( RSS reader )
* [Simple Comic](https://simple-comic.en.softonic.com/mac) 
* [Typora](https://typora.io) （ Markdown Writting )

### System Tools

* [1Password 6](https://1password.com/zh-cn/) ( Password Management Tool )
* [Alfred](https://www.alfredapp.com) ( Productive Tool )
* [Avira Security](https://www.avira.com)  ( Anti-Virus )
* Amphetamine ( keeping screen alive ) 
* [AppCleaner](http://freemacsoft.net/appcleaner/) ( App Uninstaller )
* [BaiduPan](http://pan.baidu.com/download#pan)
* [Dropbox](https://www.dropbox.com)
* [Flume](https://flumeapp.com) ( Instagram MacOS Client )
* [Handbrake](https://handbrake.fr) ( Vedios Format Converter )
* [IINA](https://iina.io) ( Vedio Player )
* [LyricsX](https://github.com/ddddxxx/LyricsX/releases) ( iTunes Music Lyrics )
* [Microsoft Teams](https://teams.microsoft.com/edustart) ( Communication Tool )
* [Maipo](http://weiboformac.sinaapp.com) ( Weibo MacOS Client )
* [OmniFocus](https://www.omnigroup.com/omnifocus) ( Todo Tool )
* [Skeype](https://www.skype.com/en/) ( Communication Tool )
* [The Unarchiver](https://macpaw.com/the-unarchiver) ( Compress Tool )
* [Tweetbot](https://www.tapbots.com/tweetbot/mac/) ( Tweet MacOS Client )

## Backup !!!!

When everything is done, don'f forget to backup system with TimeMachine !!!!
