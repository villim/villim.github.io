---
title: Run Shell Command in Background
layout: post
---

Some time, we just don't want to keep eyes on the command. We can simply 

## Put a command to Background

Just append **&** at the end of command

```bash
$ 	some-command &
```

A more sophiscated way could be:

```bash
$	some-command > /dev/null 2>&1 &
```

### STDIN, STDOUT and STDERR
STDIN, STDOUT and STDERR are three standard sources of input and output for a program. They are numbered with built-in numberings are 0, 1, and 2. Without explicitily declare, we will use STDOUT by default.

So  **> /dev/null** will send all messages to blackhole, and then we redirect STDERR to STDOUT. The reason is we wanna the application be a little quite.


## Send Running Application to Background
To send a job to the background without canceling it by
```bash
$  bg 
```	


## Suspend Current Foreground Job 
use **CTRL+Z** , you can put command in background too. But the command status is suspended. In VIM we use it a lot to external command.

## View Running Jobs
```bash
$  jobs
[1]  + running    sh Soft/MessageQueue5.1/mq/bin/imqbrokerd > /dev/null 2>&1
```


### To bring a background job to the foreground
```bash
	fg JOBS-ID
	
	%JOBS-ID
```


Restart suspended job and put it to background with:
```bash
	%JOBS-ID &
```