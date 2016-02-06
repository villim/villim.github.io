---
titile: Open FTP Service on OSX
layout: post
---

On the old OSX version, it was able to use GUI configure FTP under: **System Preferences -> Sharing** . Unfortunatly, it has been removed from 10.9.5

However, you can still easily open it with command line:

## Load FTP
```bash
$ sudo launchctl load /System/Library/LaunchDaemons/ftp.plist
```

## Check FTPD Status
```bash
$  sudo launchctl list | grep ftpd
	0	com.apple.ftpd
```

## Unload FTP
```bash
$ sudo launchctl unload /System/Library/LaunchDaemons/ftp.plist
```

## Configure File
```bash
$  ll /etc/ftpd.*
	ftpd.conf          ftpd.conf.default  ftpusers
```

* FTP will use your home folder **~** as root folder
* You can configure permission lile: **umask guest 0707** , read more in **man ftpd**

## Test
```bash
$ ftp localhost 21
```

## Alfred Workflow
To make it more easier, I was thinking to add a Alfred Workflow. 

Then I found must use **SUDO**, although we can bypass the password. But  neither export askpass nor modify sudoers with empty password, not seems like a secure solution. I'd rather just working with a bash script.

## Using SFTP!!
Let's rethink about why OSX remove the GUI configuration for FTP?

Probably, cause not too many people will use it now. And more important, it's unsafe.

Right now, Apple recommend you using SSH+SFTP. You can find the configuration uder : **System Preferences -> Sharing -> Remote Login**

So, if you don't have special reason, just using this one!

