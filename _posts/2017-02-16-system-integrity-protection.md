---
title: OSX System Integrity Protection
layout: post
---

## Operation not permitted

In order to use **rpm-maven-plugin** plugin. Need install RPM on OSX.

```
 ➜  ps-api git:(master) ✗ brew install rpm
```

And need link to **/usr/bin/** , let Maven able to locate it. Then I encountered **Operation not permitted** Exception.

```
➜  ps-api git:(master) ✗ sudo ln -sf /usr/local/bin/rpm /usr/bin/rpm

ln: /usr/bin/rpm: Operation not permitted
```


## System Integrity Protection

It was caused by [System Integrity Protection](https://developer.apple.com/library/mac/documentation/Security/Conceptual/System_Integrity_Protection_Guide/ConfiguringSystemIntegrityProtection/ConfiguringSystemIntegrityProtection.html)

**Security configuration** is stored in NVRAM rather than in the file system itself. As a result, this configuration applies to all installations of OS X across the entire machine and persists across OS X installations that support System Integrity Protection.

System Integrity Protection can be configured using the csrutil(1) command.

### Check SIP Status

You can check whether System Integrity Protection is currently enabled on your system by running the following command in the Terminal:

``` 
$ csrutil status 
```

### Disable SIP Status

To enable or disable System Integrity Protection, you must boot to Recovery OS and run the csrutil(1) command from the Terminal.

1. Boot to Recovery OS by restarting your machine and holding down the Command and R keys at startup.
2. Launch Terminal from the Utilities menu.
3. Enter the following command: **$ csrutil enable** 
After enabling or disabling System Integrity Protection on a machine, a reboot is required.