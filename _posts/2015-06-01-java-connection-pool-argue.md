---
title: Java Database Connection Pool Framework
layout: post

---

Connection Pool 是个老东西了，不过之前重来没有认真关注过。因为一般都被搞得妥妥的了。

最近项目使用 Hibernate 3.5.6 vs DBCP，发布测试版后，有一两天，大概碰到服务器端有网络中断后，会碰到下面的ERROR，导致系统完全无法再使用了。

{% highlight bash %}
2015-05-27 21:42:24,958 [qtp1793329556-17] DEBUG org.springframework.orm.hibernate3.SessionFactoryUtils - Could not close Hibernate Session
org.hibernate.exception.GenericJDBCException: Cannot release connection
        at org.hibernate.exception.SQLStateConverter.handledNonSpecificException(SQLStateConverter.java:140)
        at org.hibernate.exception.SQLStateConverter.convert(SQLStateConverter.java:128)
        at org.hibernate.exception.JDBCExceptionHelper.convert(JDBCExceptionHelper.java:66)
        at org.hibernate.exception.JDBCExceptionHelper.convert(JDBCExceptionHelper.java:52)
        at org.hibernate.jdbc.ConnectionManager.closeConnection(ConnectionManager.java:478)
        at org.hibernate.jdbc.ConnectionManager.cleanup(ConnectionManager.java:408)
        at org.hibernate.jdbc.ConnectionManager.close(ConnectionManager.java:347)
        at org.hibernate.impl.SessionImpl.close(SessionImpl.java:343)
        ...
        Caused by: java.sql.SQLException: Already closed.
        at org.apache.commons.dbcp.PoolableConnection.close(PoolableConnection.java:114)
        at org.apache.commons.dbcp.PoolingDataSource$PoolGuardConnectionWrapper.close(PoolingDataSource.java:191)
        at org.springframework.jdbc.datasource.DataSourceUtils.doCloseConnection(DataSourceUtils.java:341)
        at org.springframework.orm.hibernate3.LocalDataSourceConnectionProvider.closeConnection(LocalDataSourceConnectionProvider.java:100)
{% endhighlight %}

先看了一下我们使用的 DBCP1.4，真是吓了一跳，已经是 2010-2-14 发布的老家伙了。Check detail at :[DBCP Release Note](http://commons.apache.org/proper/commons-dbcp/changes-report.html). 大概应该就是从这儿开始，DBCP被骂得很厉害，网上各个地方都在爆发关于 connection pool 的讨论，出现了一大堆被不断提到的项目，C3P0、Proxool、BoneCP、HikariCP ... 就像[这篇贴子](http://stackoverflow.com/questions/520585/connection-pooling-options-with-jdbc-dbcp-vs-c3p0) 

公司层面选Framework当然不能因为效率高就冲上去，项目的稳定性，持续开发能力和背后支持的团体、公司都是很重要的考量。

虽然每个项目都有自己得鼓吹者，其实每个也都可以看到因为无数的Bug而被人唾弃，有人说 DBCP 性能更高，HikariCP更是牛B中的战斗机，有人又说C3P0最稳定，在多个服务器中表现更好 ... 或许有些新项目真的有些技术革新，可惜人需要时间检验。所以我们更看重 DBCP 2.1 和 C3P0 0.9.5 这两个今年发布的最新版。其实并没有什么巨大的差别，如果DBCP不是去年开始又从新发力，那么这个大众情人C3P0，应该是首选了。

而性能上的差异，更多应该是默认配置不同造成的，如果能够正确的配置，理论上他们的Performance应该是相差无几的。在简单的测了两个最新版也后，我们并没有发现巨大差异，所以继续选择了最新版的DBCP。关于无法关闭数据库链接的问题，首先考虑的是配置一下connection的验证。于是关心一下下面几个参数的配置。

{% highlight bash %}
database.testOnBorrow=true
database.testOnReturn=true
database.testWhileIdle=true
database.validationQuery=select 1 from dual
database.validationQueryTimeout=10
{% endhighlight %}

目前测试来看，效果良好，有待继续检验。

References:
[DBCP Configuration Parameters](http://commons.apache.org/proper/commons-dbcp/configuration.html) 

[C3P0 Configuration Properties](http://www.mchange.com/projects/c3p0/#configuration_properties)

[Battle of the Connection Pools](http://blog.trustiv.co.uk/2014/06/battle-connection-pools)


                                                                                                                      