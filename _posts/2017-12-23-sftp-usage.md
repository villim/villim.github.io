---
titile: SFTP Usage
layout: post
---

## What is SFTP?

FTP seems like a really ancient term now ... Although we don't use it too much now, it is still a chooice when we want to transfer files between two remote systems as its name "File Transfer Protocol".

SFTP, It's easy to guess stands for Secure File Transfer Protocol. Most of the time, SFTP is preferable to FTP! espeicily when you choose a business solution. The reason is also obviously.

Althoguht there's plenty of GUI tools, but infact the commandline is also quite handy and powerful.


##Connect & Disconnnect

```bash
# sftp username@remote_hostname_or_ip
# username@remote_hostname_or_ip's password:
# <password>
Connected to remote_hostname_or_ip
sftp> exit 
```

## Navigating

###  on SFTP Server

```bash
sftp> pwd
sftp> ls
sftp> cd 
```

### on local machine

```bash
sftp> lpwd
sftp> lls
sftp> lcd
```

## Transferring Files

### upload to SFTP

```bash
sftp> put localFile
sftp> put -r localDirectory 
```
### donwload from SFTP

```bash
sftp> get remoteFile
sftp> get -Pr remoteDirectory  
# -P maintain the appropriate permissions 
```

## More Commands

### DF - Display statistics

```bash
# display remote SFTP
sftp> df -h
    Size     Used    Avail   (root)    %Capacity
  40.7GB   14.8GB   23.8GB   25.9GB          36%
  
# display local machine
sftp> !df -h
Filesystem                   Size   Used  Avail Capacity iused               
/dev/disk1s1                234Gi  201Gi   28Gi    88% 2146890 
devfs                       332Ki  332Ki    0Bi   100%    1150                   
/dev/disk1s4                234Gi  4.0Gi   28Gi    13%       6 
... ...                   
``` 

### CHMOD - Change permissions of file

```bash
# Change SFTP file
sftp> chmod 777 publicFile

# Change local file
sftp> !chmod 644 somefile
```

There are more commands we can use : CHGRP, CHOWN, RENAME ... try to find more description from help document.

### Help Document
```bash
sftp> help
```



