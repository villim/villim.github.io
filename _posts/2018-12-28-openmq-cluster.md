---
title: OpenMQ Cluster Configuration
layout: post
---

GlassFish MessageQueue also known as (OpenMQ or Open MQ), is an open-source message-oriented middleware project by Oracle (formerly Sun Microsystems) that implements the Java Message Service 2.0 API (JMS).

OpenMQ provides enterprise features including clustering for scalability and high availability. The cluster feature is implemented by sharing messages and cluster with Database.

To configure cluster feature, we need:

## (1) Update default.properties

Default Propeties file located at:

```bash 
MessageQueue5.1/mq/lib/props/broker/default.properties
```
To be able to easily change cluster vairables, we can put all of them in a separate file, with key **imq.cluster.url**, check following example:

```xml
#######################
# Persistence Settings
#######################

# Type of data store
####################

# Both file-based and JDBC-based persistence is currently supported. File-based
# is the default. To plugged in a database, change the value of this property
# to 'jdbc' and update all appropriate JDBC related properties.
#
# imq.persist.store=<file|jdbc>
#
imq.persist.store=file

imq.cluster.url=file:/{your-customized-location}/imq-cluster.properties
```


## (2) Create imp-cluster.properties file

imp-cluster.properties file looks like following:

```text
imq.cluster.ha=true
# imq.cluster.clusterid no more than 13 characters
imq.cluster.clusterid={your costomized cluster id}

##TO BE CHANGED WHILE DEPLOYEMNT##
# TODO: different value for each node 
imq.brokerid=broker1

imq.persist.store=jdbc

imq.persist.jdbc.dbVendor=oracle
imq.persist.jdbc.oracle.driver=oracle.jdbc.pool.OracleConnectionPoolDataSource
# There were defect when put user/password in url
imq.persist.jdbc.oracle.property.url=jdbc:oracle:thin:@{db hostname}:1521/{db service name}
imq.persist.jdbc.oracle.user={db user name}
imq.persist.jdbc.oracle.password={db password}

imq.cluster.sharecc.persist.jdbc.dbVendor=oracle
imq.cluster.sharecc.persist.jdbc.oracle.property.url=jdbc:oracle:thin:@{db hostname}:1521/{db service name}
imq.cluster.sharecc.persist.jdbc.oracle.user={db username}
imq.cluster.sharecc.persist.jdbc.oracle.password={db password}

##TO BE CHANGED WHILE DEPLOYEMNT##
# TODO: change to server ipaddress 
# There's defect when not specify ip
imq.cluster.heartbeat.hostname=

java.util.logging.FileHandler.pattern=/{log files path}/openmq/${imq.instancename}_log.txt
# Keep 7 log files, each 100M at most
java.util.logging.FileHandler.limit=104857600
java.util.logging.FileHandler.count=7

```

There are few things need pay attention:

1. **imq.cluster.clusterid** must be an alphanumeric string 
2. JDBC URL should not specify username and password, encounter problem using Oracle in version 5.1
3. Encounter problem when not configure **imq.cluster.heartbeat.hostname**



## (3) Add Ojdbc jar file 

Put ojdbc jar file under lib path, like following:

```bash
# openmq/mq/lib/ext/ojdbc7-12.1.0.1.jar
```

Otherwise, you will encounter error as:

```bash
[#|2018-11-28T10:18:59.909-0500|SEVERE|5.1|imq.log.Logger|_ThreadID=1;_ThreadName=main;|ERROR [B3198]: Error initializing cluster manager:
com.sun.messaging.jmq.jmsserver.util.BrokerException: [B3024]: Failed to load JDBC driver: oracle.jdbc.pool.OracleConnectionPoolDataSource
```

## (4) Test

If everything configured correctly, after you restart OpenMQ, Tables like **MQxxxxCLUSTER** will be created in database.


## (5) Use cluster

Cluster means one Queue instance is down, messages in this instance will be transfered to others.

But to handle messages in other queue instance, you must have listeners on them too. So we have configure part of listeners on different queue instanct while starting.

But to use 100% of our listeners, We can have all of them listening to node1 first, if node1 is down, then automaticly change to node2. We will have similar code as following:

```java
props.put("imqAddressList", env.getProperty("mq://{node1}:7676,{node2}:7676"));
```


