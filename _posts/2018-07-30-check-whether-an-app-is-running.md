---
title: Check whether an App is Running
layout: post
---

Creating a Spring-boot Application, want to running it as a single instance. At the beginning, try to validate directly inside Java code. But thought it again, it seems quite complex and unnecessary, we can simply and directly control this by **Shell Script** while starting Application.

The basic idea is to find whether current application is running with **Process Id**. 

The **Process Id** can be found in **PID file**. If there's no PID file for this applicaiton means the application is not started. But there is a exception, if application is exit abnormally, PID file could still exist with no Process Id in it.

Based on these information, first idea is:

## If we know the application's name

we can find running process with either **Process Id** or **Applicaiton's name** with **ps** command.

```bash
PIDFILE=/path/to/pid-file
APP_NAME='applications name'
if [ -e ${PIDFILE} ]; then
    PID=`cat ${PIDFILE}`
    PSINFO=`ps -f -p ${PID} | grep ${APP_NAME}`
    if [ ! -z "${PSINFO}" ]; then
        echo ${APP_NAME} is already running PID=${PID}
        exit 1
    fi
fi

```

Later in Stack Overflow, find a much elegent implementation. no need to know Application's Name at all.

## But If we dont know app's name at all

```bash
PIDFILE=/path/to/pid-file
if [ -f "$PIDFILE" ] && kill -0 `cat $PIDFILE` 2>/dev/null; then
    echo still running
    exit 1
fi  
echo $$ > $PIDFILE
```

The most celever statement is: **Kill -0**

In Kill's manual, you won't find **-0** at all:

```
     Some of the more commonly used signals:

     1       HUP (hang up)
     2       INT (interrupt)
     3       QUIT (quit)
     6       ABRT (abort)
     9       KILL (non-catchable, non-ignorable kill)
     14      ALRM (alarm clock)
     15      TERM (software termination signal)
```

Doesn't matter, let's try to kill -0 with a running process id:

```bash
kill -0 {a running process id}
```

you will see no output to screen, that means it return 0 .

But if we kill a non-running process id, it will return 1 with a exception error:

```bash
$ kill -0 312333 # un-exsited process id
kill: kill 312333 failed: no such process
```

Thus, with kill command, we would be able to judge whether App is running just based on PID file, what a Hack!!!! Salute you ~ 