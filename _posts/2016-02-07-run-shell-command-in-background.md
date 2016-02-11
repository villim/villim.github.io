---
title: Run Shell Command in Background
layout: post
---

Some time, we just don't want to keep eyes on the rolling command. We can simply 

## Put a command to Background

Just append **&** at the end of command

```bash
$ some-command &
```

A more sophiscated way could be:

```bash
$ some-command > /dev/null 2>&1 &
```
A simple description about **2>&1**

### STDIN, STDOUT and STDERR
STDIN, STDOUT and STDERR are three standard sources of input and output for a program. 

They are numbered with built-in numberings are 0, 1, and 2. Without explicitily declare, we will use STDOUT by default.

So  **> /dev/null** will send all messages to blackhole, and then we redirect STDERR to STDOUT by **2>&1**. The reason for doing this, is to simplify output, only concerns on ERRORs.

If a application already running, we don't need to restart them, can still put them into background by:

## Send Running Application to Background
To send a job to the background without canceling it by
```bash
$  bg 
```	
Another way to put current job to background, is to SUSPEND it. In VIM we use this trik a lot:

## Suspend Current Foreground Job 
use **CTRL+Z** , you can put command in background too. But the command status is suspended. When using VIM, it's the most easy way to invoke external commands.

Now we need to check what job is running in background:

## View Running Jobs
```bash
$  jobs
[1]  + running    sh Soft/MessageQueue5.1/mq/bin/imqbrokerd > /dev/null 2>&1
```
And we can put hidden job to frontend too:

### To bring a background job to the foreground
```bash
fg JOBS-ID
%JOBS-ID
```
Another scenario is : Restart suspended job and put it to background with

```bash
%JOBS-ID &
```
