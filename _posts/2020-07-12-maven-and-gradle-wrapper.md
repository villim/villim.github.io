---
title: Maven & Gradle Wrapper
layout: post
---

## Maven vs Gradle

Maven seems too old and too verbal, Gradle is much faster and flexible. Once a while I was planning to switch all Maven projects to Gradle.

![Gradle vs Maven](http://villim.github.io/img/2020/gradle-vs-maven.png)

But infact, Maven still have better Plugins support and more important, as we can specify ``` <parent> ``` tag, we can define much more flexible projects structure. That's really helpful when working on some common libraries like Spring. 

The differences deserves another post. But it would be better to keep eyes on both of them. Here just want to document an important feature both provided **Wrapper**.


## Wrapper

When someone come to check our source code, they may have differnt Maven/Gradle version, or even not install at all. How can they find out which version should use?

Even for the developers themselves, it could be an issue. In nowadays software management, we usually install tools with Package Manager like [Brew](https://brew.sh). So Maven and Gradle may be updated automatically.

That's why Wrapper coming. The idea is simple, but really great. Based on the project specific Maven/Gradle scripts, we can use exactly the same version it should be. After wrapper scripts created, we can use following script commands:

* mvnw
* mvnw.cmd ( for Windows )
* gradlew
* gradlew.bat ( for Windows )

We should provide this for all our projects.

## Creating Gradle Wrapper

```bash
$ cd project-root-folder
$ gradle wrapper --gradle-version 5.6.4 --distribution-type all
``` 


## Creating Maven Wrapper

The easiest way is using Maven Wrapper Plugin.

```
$ cd project-root-folder
$ mvn -N io.takari:maven:wrapper -Dmaven=3.6.1
```

**-N** means **–non-recursive** so that the wrapper will only be applied to the main project of the current directory, not in any submodules.

