---
title: Generated Classes Dependency in Eclipse
layout: post
---

## The Invisible Ghost

In order to write less code, there are some tool will generate specific Java classes based on annotation. And these generated Classes, methods, variables are required in runtime.

For example, when using [spring-data-jpa-datatables](https://github.com/darrachequesne/spring-data-jpa-datatables#spring-data-jpa-datatables), we will depends on generated classes.

Yet，Eclipse is blind. It will complain about with error message:

```
The import domain.model.transaction.Transaction_ cannot be resolved
```

**Transaction_** is the generated Class under **target/generated-sources/java**

This is understandable, Eclipse is not designed to depends on generated classes.


## Solution

A quick thought is, move these generated Classes to a new sub-project as source code. However, it seems ... not elegant.

Lucky, there's a better way.

### 1. M2E-APT Plugin

Under my sub-project, I can see **Referenced Libraries** && **Maven Dependencies**, this means my build path is managed by [M2Eclipse](http://www.eclipse.org/m2e/).

So M2Eclipse is not able to see the Classes under target folder, but we can ask help from [m2e-apt](https://marketplace.eclipse.org/content/m2e-apt).

**m2e-apt** aims at providing automatic Annotation Processing configuration in Eclipse, based on your project's pom.xml and its classpath dependencies (Requires Java >= 1.6). 

We can install in from **Eclipse Marketplace**.

### 2. build-helper-maven-plugin

Now we configure domain module to expose generated Classes.

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>build-helper-maven-plugin</artifactId>
    <version>1.8</version>
    <executions>
        <execution>
            <id>add-source</id>
            <phase>generate-sources</phase>
            <goals>
                <goal>add-source</goal>
            </goals>
            <configuration>
                <sources>
                    <source>target/generated-sources/java/</source>
                </sources>
            </configuration>
        </execution>
    </executions>
</plugin>
```

Eclipse should be satisfied now (￣▽￣) 