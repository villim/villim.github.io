---
title: You Have Mail
layout: post
---

## What's the hell

记不得那天开始，每次运行命令行，都会看到这样的提示：

```bash
Last login: Thu Jan 14 14:56:23 on ttys004
You have mail.
$ > 
```

之前偷懒，一直选择直接忽略，不过每天都看到还是太扎眼了，今天终于看不过去了。用 mail 命令看了一下：

```bash
➜  ~  mail
Mail version 8.1 6/6/93.  Type ? for help.
"/var/mail/williamwang": 5 messages 5 unread
>U  1 williamwang@wl000701  Wed Jun 10 14:02  20/871   "Cron <williamwang@wl00070178> /Users/williamwang/xxx"
 U  2 williamwang@wl000701  Wed Jun 10 15:02  20/928   "Cron <williamwang@wl00070178> /Users/williamwang/xxx/xxx.sh"
 ... ...
```

原来是因为之前测试 cron job 造成的，没什么大不了。接下来我想删掉这些邮件时，却做了一个很吊诡的事情，我竟然是先去 Google 了！

搜索了好一会儿，没看到什么靠谱的东西有用的信息。静下心来，突然反问自己为什么没有看 mannual 呢？明明命令行已经提醒的很清楚了 **Mail version 8.1 6/6/93.  Type ? for help.**!

## Read the FxxKing mannual ! Jackass 

用 help 看一下，一切都很清晰了，就不需要解释了

```bash 
$ help
    Mail   Commands
t <message list>		type messages
n				goto and type next message
e <message list>		edit messages
f <message list>		give head lines of messages
d <message list>		delete messages
s <message list> file		append messages to file
u <message list>		undelete messages
R <message list>		reply to message senders
r <message list>		reply to message senders and all recipients
pre <message list>		make messages go back to /var/mail
m <user list>			mail to specific users
q				quit, saving unresolved messages in mbox
x				quit, do not remove system mailbox
h				print out active message headers
!				shell escape
cd [directory]			chdir to directory or home if none given
```

如果你要禁用 Mail，添加配置
```bash
$ vim ~/.zshrc  -- Add this line "unset MAILCHECK" 
```

## The Pain of Google 

Internet is not just a message carrier anymore, in some way, it's already a living life. And it's continue evoluting. Right now it's already much much much more smarter than human. You almost can find any knowledge you want to know on IT.

As we becoming more and more dependent on IT, our thinking partern changed. Previously, we must act as Sherlock Holmes to search details in clues, burn out our brain to get result. But right now, just a few clicks in browser, we will stand on the shoulders of giants.

Sharing knowledge is MUST, and infact it's human's best invention. But as a individual, gradually losing the ablity to think is terrifing.

Take today's case for example, the problem which I just need spent 5 mins to learn. However, I directly choose Google without a thought, that's really a bad sighn! Have to bear it in mind from now on, to be a more valualbe individual is more appealling for me.




