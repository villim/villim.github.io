---
title: Debug SpringBoot with Gradle in Eclipse
layout: post
---

There're 2 ways to debug SpringBoot Application in Eclipse.

## 1st way, Run SpringBoot Application in Eclipse

This is most easy and natural way in Eclipse, you need use:

* Spring version Eclipse : [STS](https://spring.io/tools/sts) 
* or Standard Eclipse installed [Spring Tools](http://marketplace.eclipse.org/content/spring-tools-aka-spring-ide-and-spring-tool-suite) from Eclipse Marketplace

Then just need configure in **Run -> Debug Confugrations -> Spring Boot App** 

![debug-springboot-run-in-eclipse](http://villim.github.io/img/2018/debug-springboot-run-in-eclipse.png)


## 2nd way, Run SpringBoot Application in Shell

### 2.1 Run SpringBoot with --debug-jvm 


Run Spring-boot with **--debug-jvm** , Gradle will start with remote debug mode.

```bash
➜  XXX-springboot-project-folder git:(master) ✗ gradle bootRun --debug-jvm

> Task :XXX-springboot-project:bootRun
Listening for transport dt_socket at address: 5005
<============-> 93% EXECUTING [1m 1s]
> :XXX-springboot-project:bootRun
```

From the Shell,  you will see Gradle is waiting for connection to remote debug on port 5005.

### 2.2 Configure Eclipse Remote Debugging

Configure with **Project -> Debug as... -> Debug Configuration -> Remote Java Application.**  As host set localhost, and port 5005.

![debug-springboot-run-in-shell](http://villim.github.io/img/2018/debug-springboot-run-in-shell.png)

After click **DEBUG** button, debugging mode will attach to 5005, and Gradle will continue to launch application.

