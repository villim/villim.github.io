---
title: Get Git Commit Info in Gradle
layout: post
---

There is a case we want to appened Git-Commit-Id to our Jar file name or RPM file, and we may need read that information in our Application.

When using Maven, we can use [**git-commit-id-plugin**](http://villim.github.io/git-commit-id-plugin), I have document it in [previous post](http://villim.github.io/git-commit-id-plugin).  Now, I have switched to Gradle, unlucky, I didn't find a mature plugin to do the same function. 

## General Idea

We can learn from **git-commit-id-plugin**, and try to wirte some simple task to achieve similiar function. The general idea is, generate a properties file under class path, while Maven/Gradle building process, write Git information to that properties file. Then this properties will be packaged in Jar file.


## Grgit

[Grgit](https://github.com/ajoberstar/grgit) is a wrapper over JGit that provides a fluent API for interacting with Git repositories in Groovy-based tooling.

with **grgit** we will be able to read Git information in Gradle. I just need very simple feature from grgit, so used a old version 1.1.0

I defined **grgit** in my parent **build.gradle**, and store in gloable variable for all the sub modules.

```groovy
buildscript {
    repositories {
    	maven {
      		url "https://plugins.gradle.org/m2/"
    	}
    }

    dependencies {
        classpath "org.ajoberstar:grgit:1.1.0"
    }
}

ext {
	// Open the Git repository in the current directory.
    git = org.ajoberstar.grgit.Grgit.open(file('.'))
    // Get commit id of HEAD.
    gitRevision = git.head().id
    // Get abbreviated commit Id of HEAD
    gitAbbRevision = git.head().abbreviatedId
}
```

## Use Git-Id in Jar file

As we already get Git-Id in parent build.gradle, in sub module build.gradle file, just need assign the value to VERSION variable.

```groovy
version="${project.version}-${gitAbbRevision}"
```

## Use Git-Id in RPM file

Similiar to Jar file, I use **nebula-gradle-ospackage** to build RPM files. Just change the VERSION in similar way.

```groovy
 ospackage {
    packageName = "${project.name}"
    version = "${project.version}-${gitAbbRevision}"
    release = '1'
    arch = I386
    os = LINUX
}
```

## Write Git-Id to Properties File

Haven't really familiar with Groovy, this code must be quite stupid and foolish, but it's working :) Let's improve it later.

```groovy
task getVersions(dependsOn: processResources) {
    doLast {
    	def separator = System.getProperty('line.separator')
        def version = project.version.toString()
        boolean success = new File("$buildDir/resources/main/version.properties").delete()
        def file = new File("$buildDir/resources/main/version.properties")
		//file.write("project.version=${version}$separator")
        file << "project.version=${moduleVersion}$separator"
        file << "git.version=${gitRevision}$separator"
        file << "git.abbreviated.version=${gitAbbRevision}$separator"
    }
}

classes {
    dependsOn getVersions
}
```

As we set task dependencies, no need to manually invoke getVersions method, while we building classes, it will automatically generated.

Now you can read this **version.properties** in your application, and use it as your like.