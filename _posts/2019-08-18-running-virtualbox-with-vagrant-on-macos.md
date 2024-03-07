---
title: Running VirtualBox with Vagrant on MacOS
layout: post
---

## Choose Virtual Machine Tool

The best **Virtual Machine** tool I like is [VMware Workstation](https://www.vmware.com/cn/products/workstation-pro.html). However, it's too too expensive.

But for now, as I just need a VM for testing occasionally, and I don't even need working with GUI. **VirtualBox** is a good enough, it's totally free. 

Let's install **VirtualBox** first, [download here](https://www.virtualbox.org/wiki/Downloads). 

## What is Vagrant

However, **VirtualBox** is really ... difficult to use, not friendly enbough. The good new is we have a wounderful tool which named [Vagrant](https://www.vagrantup.com/).

![Vagrant](http://villim.github.io/img/2019/vagrant.png)

**Vagrant** provides easy to configure, reproducible, and portable work environments built on top of industry-standard technology and controlled by a single consistent workflow to help maximize the productivity and flexibility of you and your team.

Install Vagrant with brew cask:

```
brew install --cask vagrant
```


## How to Use Vagrant

### Create VM Root Folder

```bash
$ mkdir VMs & cd VMs
```

### Create a CentOS7 in Vagrant

```
$ vagrant box add centos/7
==> box: Loading metadata for box 'centos/7'
    box: URL: https://vagrantcloud.com/centos/7
This box can work with multiple providers! The providers that it
can work with are listed below. Please review the list and choose
the provider you will be working with.

1) hyperv
2) libvirt
3) virtualbox
4) vmware_desktop

Enter your choice: 3
==> box: Adding box 'centos/7' (v1905.1) for provider: virtualbox
    box: Downloading: https://vagrantcloud.com/centos/boxes/7/versions/1905.1/providers/virtualbox.box
    box: Download redirected to host: cloud.centos.org
    box: Progress: 43% (Rate: 738k/s, Estimated time remaining: 0:06:27)
```

### Create a CentOS7 configuration

```
$ vagrant init
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
```
After **init** will create a configuration file named Vagrantfile.

```
$ ls -al
-rw-r--r--  1 villim  staff   2.9K Aug 16 23:30 Vagrantfile
```

### Change Vagrantfile for Operation System name

modify **config.vm.box** to **centos/7**

```
# file ~/VMs/Vagrantfile
 15   #config.vm.box = "base"
 16   config.vm.box = "centos/7"
```
### Start and connect to CentOS7 VM

```
$ vagrant up
$ vagrant ssh
```

**up** will start system, and **ssh** will connect to it.

### Mount External Folder

There is a great feature to **Mount External Folder** from our MacOS system. In this way, we save great many spaces and easier to share files.

First, need install plugin:

```
$ vagrant plugin install vagrant-vbguest
```

Then modify Vagrantfile file again, add the foler for example:

```
 47   # config.vm.synced_folder "../data", "/vagrant_data"
 48   config.vm.synced_folder "/Users/villim/ForSharing", "/vagrant_data"
```

Then we need restart system again:

```
$ vagrant halt
$ vagrant up
```


## Appendixs: Install Java on CentOS

Download Oracle JDK from [here](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html).

```
$ sudo yum localinstall jdk-8u102-linux-x64.rpm
```

More detailed steps can read from [here](https://www.mkyong.com/java/how-to-install-oracle-jdk-8-on-centos/
).


## Appendixs: Install Maven on CentOS

The easiest way is just:

```
$ sudo yum install maven
```

However, this won't install latest Maven. If need latest version, we can first download from [here](https://maven.apache.org/download.cgi).

```
$ sudo tar xf /tmp/apache-maven-3.6.1.tar.gz -C /opt
$ sudo ln -s /opt/apache-maven-3.6.1 /opt/maven
```

Create maven configuration file: **/etc/profile.d/maven.sh** with following content:

```
export JAVA_HOME=/usr/java/jdk1.8.0_171-amd64
export M2_HOME=/opt/maven
export MAVEN_HOME=/opt/maven
export PATH=${M2_HOME}/bin:${PATH}
```

Then reload maven environment resource:

```
$ sudo chmod +x /etc/profile.d/maven.sh
$ source /etc/profile.d/maven.sh
```


## Appendixs: Install Gradle on CentOS

Download gradle from [Gradle Official Site](https://gradle.org/releases/)


First, unzip files:

```
$ mkdir /opt/gradle
$ unzip -d /opt/gradle gradle-5.6.4.zip
```

Then change PATH with the unzip folder:
```
$ vim .bash_profile
# with PATH=$PATH:/opt/gradle/gradle-5.6.4/bin
$ source .bash_profile
```


