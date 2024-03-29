---
title: Remote Debug with Intellij
layout: post
---

When we need debug on remove server directly, we need use JDWP - [Java Debug Wire Protocol](https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/introclientissues005.html)

## At Remote Side

start SpringBoot application with following parameters:

```
java -Xdebug -Xrunjdwp:transport=dt_socket,server=y,address=8001,suspend=y -jar sprint-boot-app.jar
```

Port 8001 can change.


## At Intellij Side

Open **Run/Debug Configurations**, create a new Configuration with following arguments:

```
agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=8001
```
Port number should be the same as we specified at remote side.

![Remote Debug with Intellij](http://villim.github.io/img/2020/remote-debug-with-intellij.png)
