---
title: Remote Debug with Intellij
layout: post
---

When we need debug on remove server directly, we need use JDWP - [Java Debug Wire Protocol](https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/introclientissues005.html)

## At Remote Side

Start SpringBoot application with following parameters, port 8001 can be changed:

Java 5-8:

```bash
java -Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=y,address=8001 -jar sprint-boot-app.jar
```

Java 9 - later:

```bash
java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:8001 -jar sprint-boot-app.jar
```

If When using Dockerfile:

```txt
EXPOSE 8080 8001
ENV JAVA_TOOL_OPTIONS='-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:8001'
ENTRYPOINT ["java", "-jar", "sprint-boot-app.jar"]
```


## At Intellij Side

Open **Run/Debug Configurations**, create a new Configuration with following arguments:

```
agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=8001
```

* Port number should be the same as we specified at remote side.
* Java 5-8: address=8001
* Java 9-x: address=*:8001

![Remote Debug with Intellij](http://villim.github.io/img/2020/remote-debug-with-intellij.png)
