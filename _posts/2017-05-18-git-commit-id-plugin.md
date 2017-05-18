---
title: git-commit-id-plugin
layout: post
---

When build RPM with Maven, I want to appened reversion number to rpm file. When using SVN we have [buildnumber-maven-plugin](http://www.mojohaus.org/buildnumber-maven-plugin/usage.html), now using Git we have [git-commit-id-plugin](https://github.com/ktoso/maven-git-commit-id-plugin).

## What is git-commit-id-plugin

This plugin makes basic repository information available through maven resources. This can be used to display "what version is this?" or "who has deployed this and when, from which branch?" information at runtime, making it easy to find things like "oh, that isn't deployed yet, I'll test it tomorrow" and making both testers and developers life easier.

How to use it?

## git-commit-id-plugin conf example

```
<plugin>
    <groupId>pl.project13.maven</groupId>
    <artifactId>git-commit-id-plugin</artifactId>
    <executions>
        <execution>
        <id>get-the-git-infos</id>
        <goals>
          <goal>revision</goal>
        </goals>
      </execution>
    </executions>
    <configuration>
    <dotGitDirectory>${project.basedir}/.git</dotGitDirectory>
    <prefix>git</prefix>
    <dateFormat>dd-MM-yyyy '@' HH:mm:ss z</dateFormat>
    <dateFormatTimeZone>${user.timezone}</dateFormatTimeZone>
    <verbose>false</verbose>
    
    <!-- ALTERNATE SETUP - GENERATE FILE -->
    <generateGitPropertiesFile>true</generateGitPropertiesFile>
    <generateGitPropertiesFilename>${project.build.outputDirectory}/git.properties</generateGitPropertiesFilename>
    <format>properties</format>
    <skipPoms>true</skipPoms>
    <injectAllReactorProjects>true</injectAllReactorProjects>
    <failOnNoGitDirectory>true</failOnNoGitDirectory>
    <failOnUnableToExtractRepoInfo>true</failOnUnableToExtractRepoInfo>
    <skip>false</skip>
    <runOnlyOnce>false</runOnlyOnce>
    <abbrevLength>7</abbrevLength>
    <commitIdGenerationMode>flat</commitIdGenerationMode>
    </configuration>
</plugin>

```

## git.properties example

In previous configuration, we can see it will save reversion infos into a git.properties file.

```
<generateGitPropertiesFilename>${project.build.outputDirectory}/git.properties</generateGitPropertiesFilename>
```
We need create this file under:

{project-folder}/src/main/resources/git.properties

```
git.tags=${git.tags}
git.branch=${git.branch}
git.dirty=${git.dirty}
git.remote.origin.url=${git.remote.origin.url}
git.commit.id=${git.commit.id}
git.commit.id.full=${git.commit.id.full}
git.commit.id.abbrev=${git.commit.id.abbrev}
git.commit.id.describe=${git.commit.id.describe}
git.commit.id.describe-short=${git.commit.id.describe-short}
git.commit.user.name=${git.commit.user.name}
git.commit.user.email=${git.commit.user.email}
git.commit.message.full=${git.commit.message.full}
git.commit.message.short=${git.commit.message.short}
git.commit.time=${git.commit.time}
git.closest.tag.name=${git.closest.tag.name}
git.closest.tag.commit.count=${git.closest.tag.commit.count}

git.build.user.name=${git.build.user.name}
git.build.user.email=${git.build.user.email}
git.build.time=${git.build.time}
git.build.host=${git.build.host}
git.build.version=${git.build.version}
```

## How to use

These keys in git.properties file, can be refered during whole Maven building life cycle.

For example, we can append {git.commit.id.abbrev} to file name when repackaging.

```
<plugin>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-maven-plugin</artifactId>
  <executions>
    <execution>
      <goals>
        <goal>repackage</goal>
      </goals>
    </execution>
  </executions>
  <configuration>
    <addResources>true</addResources>
    <finalName>${project.artifactId}-${project.version}-${git.commit.id.abbrev}</finalName>
  </configuration>
</plugin>

```