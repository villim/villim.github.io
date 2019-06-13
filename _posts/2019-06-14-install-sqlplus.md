---
title: Install SQLPlus
layout: post 
---

My current MacOS version is Mojave. And Using Oracle version 12.

Caused our DBA don't use any Oracle Client Tools. In order to make sure every SQL file we dilivered is able to run with SQLPlus, we have to test with it.

## (1) Software Download

As Oracle version is 12, so Download: 

Windows from [here](https://www.oracle.com/technetwork/topics/winx64soft-089540.html)

1. instantclient-basiclite-windows.x64-12.2.0.1.0.zip
2. instantclient-sqlplus-windows.x64-12.2.0.1.0.zip 

MacOs from [here](https://www.oracle.com/technetwork/topics/intel-macsoft-096467.html)

1. instantclient-basic-macos.x64-12.2.0.1.0-2.zip
2. instantclient-sqlplus-macos.x64-12.2.0.1.0-2.zip 


## (2.1) Install Steps for Windows

### step 2.1.1 Install Software

```
Unzip 
instantclient-basiclite-windows.x64-12.2.0.1.0.zip
instantclient-sqlplus-windows.x64-12.2.0.1.0.zip  
to C:\Program Files\instantclient_12_2
```

### step 2.1.2 Update PATH

Modify PATH ( System Variables ) with following folders

```
* C:\Program Files\instantclient_12_2\;
* C:\Program Files\instantclient_12_2\sdk;
```

### step 2.1.3 Add Two more System Variables

```
* TNS_ADMIN=C:\Program Files\instantclient_12_2
* NLS_LANG=AMERICAN_AMERICA.UTF8
```

### step 2.1.4 tnsnames.ora file 

create tnsnames.ora file under C:\Program Files\instantclient_12_2\ with following content:

```
TEST-DB =
 (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = YourHostName)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SERVICE_NAME = YourServiceName)
    )
  )
```

## (2.2) Install Steps for MacOS

### step 2.2.1 Install Software

```bash
cd ~
unzip instantclient-basic-macos.x64-12.2.0.1.0-2.zip
unzip instantclient-sqlplus-macos.x64-12.2.0.1.0-2.zip
```

After done, all files will be extracted to 

```bash
~/instantclient_12_2
```

### step 2.2.2 Link Oracle required libraries

```bash
cd ~/instantclient_12_2
ln -s libclntsh.dylib.12.1 libclntsh.dylib
ln -s libocci.dylib.12.1 libocci.dylib

mkdir ~/lib
ln -s ~/instantclient_12_2/libclntsh.dylib.12.1 ~/lib/
ln -s ~/instantclient_12_2/{libnnz11.dylib,libociei.dylib} ~/lib/
```

### Step 2.2.3 Link SQLPlus libraries

```bash
ln -s ~/instantclient_12_2/{libsqlplus.dylib,libsqlplusic.dylib} ~/lib/
export PATH=~/instantclient_12_2:$PATH
```

### step 2.2.4 Add host mapping

```bash
sudo echo "127.0.0.1 `hostname`" >> /etc/hosts
```

### step 2.2.5 tnsnames.ora file

```bash
cd ~/instantclient_12_2
mkdir -p NETWORK/ADMIN/

echo "TEST-DB =
 (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = YourHostName)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SERVICE_NAME = YourServiceName)
    )
  )" >> NETWORK/ADMIN/tnsnames.ora

```

tnsnames.ora is the place we maintain our DB connections


## (3) Login Oracle

### 3.1 Windows

```
RUN -> CMD
$ cd C:\Program Files\instantclient_12_2\
$ sqlplus YourUserName@TEST-DB
```

### 3.2 MacOS

```bash
$ cd ~/instantclient_12_2
$ ./sqlplus YourUserName@TEST-DB

SQL*Plus: Release 12.2.0.1.0 Production on Mon Jun 3 15:35:28 2019

Copyright (c) 1982, 2017, Oracle.  All rights reserved.

Enter password:
Last Successful login time: Mon Jun 03 2019 15:35:24 +08:00

Connected to:
Oracle Database 12c Enterprise Edition Release 12.2.0.1.0 - 64bit Production

SQL>
```


## (4) Execute SQL file

```bash
SQL > @{path}{file}
```

## (5) Known Issue

* ORA-24454: client host name is not set

```
Missing STEP 5
```


* ORA-12154:TNS:could not resolve the connect identifier specified

```
create file NETWORK/ADMIN/tnsnames.ora
```

* ORA-12162: TNS:net service name is incorrectly specified

```
1. check There’s SPACES before “ TEST-DB =“  in tnsnames.ora
2. check NETWORK/ADMIN/tnsnames.ora excited
3. try copy tnsnames.ora to ~/instantclient_12_2/tnsnames.ora
```