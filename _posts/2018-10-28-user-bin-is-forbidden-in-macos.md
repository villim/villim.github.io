---
title: /user/bin is forbidden in MacOS
layout: post
---

Upgrade to MacOS Mojave, I want to build RPM packages in Eclipse.

## First, I install RPM with Brew:

```bash
$ brew install rpm
```
However, when I want to use it in Eclipse for building RPM packages, it failed with error: 

```bash
[ERROR] Failed to execute goal org.codehaus.mojo:rpm-maven-plugin:2.1.5:rpm (generate-rpm) on project ps-api: Unable to query for default vendor from RPM: Error while executing process. Cannot run program "rpm": error=2, No such file or directory -> [Help 1]
```

## Link to /user/bin/

ok, it means can not find RPM, let's link to /usr/bin/ 

```bash
$ sudo sudo ln -sf /usr/local/Cellar/rpm/4.14.1_1/bin/rpm /usr/bin/rpm
$ sudo ln -sf /usr/local/Cellar/rpm/4.14.1_1/bin/rpmbuild /usr/bin/rpmbuild
```

Strangly, it failed again with error:

```bash
cp: /usr/bin/rpm: Operation not permitted
```

## What is System Integrity Protection

After checked document, it caused by [System Integrity Protection](https://developer.apple.com/library/archive/documentation/Security/Conceptual/System_Integrity_Protection_Guide/ConfiguringSystemIntegrityProtection/ConfiguringSystemIntegrityProtection.html).

Simple explanation is, from OS X, MacOS have a new security protection. It write Rootless protection to NVRAM rather than in the file system itself, As a result, this configuration applies to all installations of macOS across the entire machine and persists across macOS installations that support System Integrity Protection. In this way, it will greatly reduce the risk to be hacked for dummies.

## Disable System Integrity Protection

To disable it, we have to use a tool named: **csrutil**

(1) Boot to Recovery OS by restarting your machine and holding down the **Command + R** keys at startup.

(2) Launch Terminal from the Utilities menu.

(3) You can check current status with

```bash
$ csrutil status
System Integrity Protection status: enabled.
```
(4) Disable with

```
csrutil disable
```

(5) Reboot is required


![macos-disable-system-integrity-protection.jpg](http://villim.github.io/img/2018/macos-disable-system-integrity-protection.jpg)