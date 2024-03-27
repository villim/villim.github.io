---
title: PostgreSQL Partition Existing Tables
layout: post
---

![2024 Resolutions](http://villim.github.io/img/2024/postgresql.jpg)

Read two brilliant articles about Postgres Partition Tables:  [Postgres Partition Conversion: minimal downtime](https://www.kylehailey.com/post/postgres-partition-conversion-minimal-downtime) and  [Partition an existing table on PostgreSQL](https://rodoq.medium.com/partition-an-existing-table-on-postgresql-480b84582e8d), but not fully satisfy my requirement.  Here is my practise:

## 1. Prepare Testing Data

Let's prepare a table for testing first (my testing version is 16):

### 1.1 Install PostgresApp

Download at: [PostgresApp](https://postgresapp.com/)

### 1.2 Install Postgres Extention pg_partman

pg_partman is an extension to create and manage both time-based and number-based table partition sets. As of version 5.0.1, only built-in, declarative partitioning is supported and the older trigger-based methods have been deprecated.

[pg_partman](https://github.com/pgpartman/pg_partman?tab=readme-ov-file#installation) is not required, but suggested. It will greatly help maintanance work.  Check [install guide](https://github.com/pgpartman/pg_partman?tab=readme-ov-file#installation). If using Amazon RDS, you can [enable pg_partman](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL_Partitions.html) easily.

### 1.3 Create Database

```sql
CREATE DATABASE testdb;
CREATE USER testuser WITH ENCRYPTED PASSWORD 'testpassword';
GRANT ALL PRIVILEGES ON DATABASE testdb TO testuser; 
ALTER DATABASE testdb OWNER TO testuser; -- If cannot access public schema
```

### 1.4 Create Table & Populate Data

```sql
BEGIN;
set search_path = public;

CREATE TABLE payments
(
    payment_id bigserial primary key,
    created    timestamptz NOT NULL,
    updated    timestamptz NOT NULL DEFAULT now(),
    amount     float,
    status     varchar              DEFAULT 'new'
);

-- fill with testing data
INSERT INTO payments (created)
VALUES (generate_series(timestamp '2023-06-01' -- date controls amount
    , now(), interval '1 minutes'));
COMMIT;
```

* Using bigserial will automatically create sequence ( **payments_payment_id_seq** ) and index ( **payments_pkey** )
* Change the date of generate_series will control amount of testing data



## 2. Migarate to Partition 

In PostgreSQL we cannot transforma regular table into partitioned, but it allows to attach regular table to a partitioned one. Thus, the plan is:

1. Rename table as old
2. Create the table again with partion
3. Attach old data to new table as partition table

### 2.1 Rename Old Table

```sql
ALTER INDEX payments_pkey RENAME TO payments_pkey_old;
ALTER TABLE payments RENAME TO payments_old;

```

### 2.2 Create New Table

```sql
CREATE TABLE IF NOT EXISTS payments
(
    payment_id bigint      NOT NULL DEFAULT nextval('public.payments_payment_id_seq'::regclass),
    created    timestamptz NOT NULL,
    updated    timestamptz NOT NULL DEFAULT now(),
    amount     float,
    status     varchar              DEFAULT 'new',
    constraint payments_pkey primary key (payment_id, created)
) PARTITION BY RANGE (created);

```

* We will continue using previous sequence ( **payments_payment_id_seq** ), so using BIGINT rather than BIGSERIAL
* Primary key ( **payments_pkey** ) cannot be payment_id alone anymore, must be ( **payment_id and created** )
* created is part of primary key, thus must be NOT NULL

```
[0A000] ERROR: unique constraint on partitioned table must include all partitioning columns Detail:
PRIMARY KEY constraint on table "payments" lacks column "created" which is part of the partition key.
```

In case, you still want payment_id as BIGSERIAL:

```sql
CREATE TABLE IF NOT EXISTS payments
(
        payment_id bigserial primary key,
        ...
        created    timestamptz NOT NULL,
        ...
}PARTITION BY RANGE (created);
```
Need Rename the auto created sequence and sync the value:

```sql
ALTER SEQUENCE payments_payment_id_seq RENAME TO payments_payment_id_old_seq; -- before create partition table 
SELECT setval('payments_payment_id_seq', nextval('payments_payment_id_old_seq'), true);
```


### 2.3 Attach Old Data as Partition

#### 2.3.1 Manually 

Extract data of 2024-03-01 to 2024-04-01 from old table, and attach as partition.

```sql
CREATE TABLE payments_p2024_03 PARTITION OF payments
    FOR VALUES FROM ('2024-03-01') TO ('2024-04-01');
CREATE INDEX idx_payments_p2024_03 ON payments_p2024_03 (created);

WITH moved_rows AS (
    DELETE FROM payments_old old
        WHERE created >= '2024-03-01' AND created < '2024-04-01'
        RETURNING old.*)
INSERT
INTO payments_p2024_03
SELECT *
FROM moved_rows;
```

#### 2.3.2 Using pg_partman

First, we will create partition tables:

```sql
SELECT partman.create_parent(
               p_parent_table => 'public.payments',
               p_control => 'created',
               p_type => 'native',
               p_interval => 'monthly',
               p_premake => 2,
               p_start_partition => '2024-03-01'
       );
```

* **p_parent_table**: must be **public.payments** rather than **payments**
* **p_premake**: will create partition table: payments_p2024_04 and payments_p2024_05
* **p_start_partition**: If change to 2024-01-01 will create payments_p2024_01 and payments_p2024_02

Then, just copy data from old table, Postgres will handle the data with partition by itsself:

```sql
INSERT INTO payments
SELECT * FROM payments_old
WHERE created >= '2024-03-01';
```

## 3. Maintainance Partition Tables

We need maintainance the partition tables by ourselves. Create new partition table each month and delete outdated partition tables. It would be boring and annoying to do it, if using pg_partman would be much convinient with Postgres procedual:

```sql
CALL partman.run_maintenance_proc()
```

To make it even more convinient, we can use another extention: [pg_cron](https://github.com/citusdata/pg_cron?tab=readme-ov-file#installing-pg_cron) to run the procedual regularly.

```sql
CREATE EXTENSION pg_cron;

UPDATE partman.part_config 
SET infinite_time_partitions = true,
    retention = '3 months', 
    retention_keep_table=true 
WHERE parent_table = 'public.payments';
SELECT cron.schedule('@hourly', $$CALL partman.run_maintenance_proc()$$);
```

## 4. Appendixes:

* [Postgres Partition Conversion: minimal downtime](https://www.kylehailey.com/post/postgres-partition-conversion-minimal-downtime)
* [Partition an existing table on PostgreSQL](https://rodoq.medium.com/partition-an-existing-table-on-postgresql-480b84582e8d)
* [pg_cron official site](https://github.com/citusdata/pg_cron?tab=readme-ov-file#what-is-pg_cron)
* [pg_partman official site](https://github.com/pgpartman/pg_partman?tab=readme-ov-file#postgresql-partition-manager)
* [AWS: Managing PostgreSQL partitions with the pg_partman extension](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL_Partitions.html)
* [PostgreSQL Partitioning Made Easy Using pg_partman](https://www.percona.com/blog/postgresql-partitioning-made-easy-using-pg_partman-timebased/)





