## SpringBoot Thin Jar

Don't Put Fat Jars in Docker Images
https://phauer.com/2019/no-fat-jar-in-docker-image/

hin JARs with Spring Boot
https://www.baeldung.com/spring-boot-thin-jar

Official: Spring Boot Thin Launcher
https://github.com/spring-projects-experimental/spring-boot-thin-launcher



mvn org.springframework.boot.experimental:spring-boot-thin-maven-plugin:properties -Dthin.output=.



java -Dthin.dryrun=true -jar ps-api-file-importer-rest-app/target/ps-api-file-importer-rest-app-4.00.00-SNAPSHOT-f6915e3.jar

java -Dthin.root=/Users/williamw/.m2 -jar ps-api-file-importer-rest-app/target/ps-api-file-importer-rest-app-4.00.00-SNAPSHOT-f6915e3.jar
java -Dthin.root=. -jar ps-api-file-importer-rest-app/target/ps-api-file-importer-rest-app-4.00.00-SNAPSHOT-ca16771.jar


java -Dthin.root=/Users/williamw/.m2 -jar ps-api-file-importer-rest-app/target/ps-api-file-importer-rest-app-4.00.00-SNAPSHOT-f6915e3.jar --thin.dryrun

java -Dthin.root=. -jar ps-api-file-importer-rest-app/target/ps-api-file-importer-rest-app-4.00.00-SNAPSHOT-f6915e3.jar --thin.dryrun






# How to Use Fat and Thin Jar

## What is Fat and Thin Jar

Spring Boot is known for its “fat” JAR deployments, where a single executable artifact contains both the application
code and all of its dependencies, making it possible to directly run with **java -jar**.

When we have many similar Spring Boot Applications, it could be odd that including the same dependencies over and over.
Like when we deploy as Docker Image, we would hope the image size is smaller, to make deployment much quicker and more
reliable.

To read more at [Spring Boot Thin Launcher](https://github.com/spring-projects-experimental/spring-boot-thin-launcher)

## How to create Fat Jar file

```bash
> ./mvnw clean install -P fat-jar
```

will create executable file like:

```bash
ll ps-api-file-importer-rest-app/target
-rw-r--r--   1 williamw  staff    122M Mar  2 23:08 ps-api-file-importer-rest-app-4.00.00-SNAPSHOT-1a350ad.jar
```

You can run with:

```bash
> cd ps-api-file-importer-rest-app/target/
> java -jar ps-api-file-importer-rest-app-4.00.00-SNAPSHOT-1a350ad.jar
```

## How to create Thin Jar file

```bash
> ./mvnw clean install -P fat-jar
```

will create jar file and a Folder thin:

```bash
> ll ps-api-file-importer-rest-app/target
-rw-r--r--   1 williamw  staff    69K Mar  2 23:08 ps-api-file-importer-rest-app-4.00.00-SNAPSHOT-1a350ad.jar
drwxr-xr-x   3 williamw  staff    96B Mar  2 23:08 thin

> ll ll ps-api-file-importer-rest-app/target/thin/root/
-rw-r--r--   1 williamw  staff    69K Mar  2 23:08 ps-api-file-importer-rest-app-4.00.00-SNAPSHOT-1a350ad.jar
drwxr-xr-x  23 williamw  staff   736B Mar  2 23:08 repository
```

You can run with:

```bash
> cd ps-api-file-importer-rest-app/target/thin/root/
> java -Dthin.root=. -jar ps-api-file-importer-rest-app-4.00.00-SNAPSHOT-1a350ad.jar
```

