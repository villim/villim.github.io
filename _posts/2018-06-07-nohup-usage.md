---
layout: post
title: nohup usage
---

## GOAL: To Run a SpringBoot App

As creating more and more SpringBoot Applications, we no longer deploy our apps to Web Container, such as Tomcat or Jetty. But we need create our own shell script to run these SpringBoot Apps, and continue running even the User exit and terminal closed.

## What is nohup

We can use **nohup**. In manual, it is said nohup means invoking a utility immune to hangups. Obviously, **nohup** is short for **no hangup**.

## nohup Usage

### Create test script

Let's create a test bash shell script **test.sh** first:

```bash
#!/bin/bash

COUNTER=0
while [  $COUNTER -lt 100 ]; do
   echo The counter is $COUNTER
   sleep 2
   let COUNTER=COUNTER+1
done
```

### Run with nohup

```bash
➜  ~ nohup sh test.sh
appending output to nohup.out
^C
```

we can see a alert message **appending output to nohup.out**, in which is continue printing **The counter is xxxx**, and in this terminal, nohup still blocking terminal, we cant conitnue using, and we can input **CTRL_C** to exit application.

Althoug we can't input anything while **nohup** is running, we can close current terminal. From nohup.out file, we can see test.sh is still running. But now if we want to exit the script, we have to findout PID and Kill it instead.



### Run nohup with &

In order not blocking terminal, we can use **nohup** with **&** together:

```bash
➜  ~ nohup sh test.sh &
[1] 56078
appending output to nohup.out
➜  ~
➜  ~ kill 56353
[1]  + 56353 terminated  nohup sh test.sh
```

This time, **CTRL_C** is not working anymore, we have to **Kill [PID]** to exit test.sh.


### Run nohup with logging

In previous way, nohup create nohup.out log file, but usually that's not what we want.

Let's say, we want to log to **test.log** file.

```bash
➜  ~ nohup sh test.sh  1>>test.log 2>&1 &
[1] 57118
➜  ~
```

Now there's no **nohup.out** file anymore, all the logs goes to **test.log** file. If we dont want see any log, we can use:

```bash
➜  ~ nohup sh test.sh  1>>/dev/null 2>&1 &
[1] 57119
➜  ~
```


**/dev/null** is a emply black hole, anything throw into it will just dispear.
**1>logfile** means print STDOUT to logfile
**2>logfile** means print STDERR to logfile
**2>&1** means redirect STDERR to STDOUT, we cant use **1>logfile 2>logfile**, cause that will logfile be opened twice, and STDOUT and STDERR will compete to write.




