---
title: PostgreSQL Sequence Cache 
layout: post
---

We are migrating from Oracle to PostgreSQL 15. The schema is automatically converted. While testing, one strange issue found is our ID field is not increasing in sequence anymore, it increased 1000 each time! 

![PostgreSQL](http://villim.github.io/img/2022/postgres.png)

After a closed look, it was caused by SEQUENCE CACHE = 1000.

```sql
SQL> CREATE SEQUENCE dts_seq
  2          INCREMENT BY 1
  3          CACHE 1000;
```

## 1. Sequence Caching Differences between Oracle vs PostgreSQL

In Oracle, the sequence cache is a global pool which all sessions access the same cache. However in PostgreSQL, each session gets its own cache! [you can find following description in official document of PostgreSQL 15](https://www.postgresql.org/docs/current/sql-createsequence.html):

<span style="color:blue">*Unexpected results might be obtained if a cache setting greater than one is used for a sequence object that will be used concurrently by multiple sessions. Each session will allocate and cache successive sequence values during one access to the sequence object and increase the sequence object's last_value accordingly. Then, the next cache-1 uses of nextval within that session simply return the preallocated values without touching the sequence object. So, any numbers allocated but not used within a session will be lost when that session ends, resulting in “holes” in the sequence.*</span>

<span style="color:blue">*Furthermore, although multiple sessions are guaranteed to allocate distinct sequence values, the values might be generated out of sequence when all the sessions are considered. For example, with a cache setting of 10, session A might reserve values 1..10 and return nextval=1, then session B might reserve values 11..20 and return nextval=11 before session A has generated nextval=2. Thus, with a cache setting of one it is safe to assume that nextval values are generated sequentially; with a cache setting greater than one you should only assume that the nextval values are all distinct, not that they are generated purely sequentially. Also, last_value will reflect the latest value reserved by any session, whether or not it has yet been returned by nextval.*</span>

Read the more about the differece at: [Sequence Caching: Oracle vs. PostgreSQL](https://seiler.us/2018-10-02-sequence-caching-oracle-vs-postgresql/)


## 2. Performance Testing of PostgreSQL

The main idea for using Sequence Cache is to provide better performance, less DB access by storing these data into memory. So what is the performance for PostgreSQL, I tested with my local DB instance and one AWS instance which have better performance.

First, let's create a test table:

```sql
CREATE TABLE test_table
(
    id          bigserial NOT NULL,
    description varchar(1024),
    PRIMARY KEY (id)
);
alter sequence test_table_id_seq cache 1;
```

Let's try insert 100,000 rows:

```sql
do
$$
    begin
        for i in 1 .. 100000
            loop
                insert into test_table_1 values (nextval('test_table_id_seq'), i);
            end loop;
        --commit;
    end
$$
;
```
Then let's change the Sequence Cache to 1000 and run the insert again:

```sql
alter sequence test_table_id_seq cache 1000;
```
The result is quite intresting:

| DB Instance | Cache Size | Insert Rows Number | Time Cost |
| ---- | -- | ------- | -------- | 
| local | 1 |  100,000 |  3 s 314 ms | 
| local | 1000 |  100,000 |  2 s 692 ms | 
| AWS | 1 |  100,000 |  2 s 463 ms | 
| AWS | 1000 |  100,000 |  2 s 456 ms | 
| AWS | 1 |  900,000 |  17 s 816 ms | 
| AWS | 1000 |  1900,000 |  17 s 410 ms | 

It's quite clear, when Cache=1 is not a real problem at all !

## 3. Conclusion

* PostgreSQL Sequence Cache is binding to session, not gloabal sharing as Oracle
* PostgreSQL Sequence Cache set to 1 is not a big performcne issue at all. Keep the default value as 1 if you don't have a good reason.
* Only special scenarios you need change PostgreSQL sequence Cache greater than 1