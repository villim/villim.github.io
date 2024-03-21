---
title: PostgreSQL Partition Existing Tables
layout: post
---

![2024 Resolutions](http://villim.github.io/img/2024/postgresql.jpg)


## 1. Prepare Testing Data

Let's prepare a table for testing first (my testing version is 16):

### 1.1 Install PostgresApp

Download at: [PostgresApp](https://postgresapp.com/)

### 1.2 Create Database

```sql
CREATE DATABASE testdb;
CREATE USER testuser WITH ENCRYPTED PASSWORD 'testpassword';
GRANT ALL PRIVILEGES ON DATABASE testdb TO testuser; 
ALTER DATABASE testdb OWNER TO testuser; -- If cannot access public schema
```

### 1.3 Create Table

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

* Using bigserial will create sequence(payments_payment_id_seq) and index(payments_pkey)
* Change the date of generate_series will control amount of testing data



## 2. Migarate to Partition 

In PostgreSQL we cannot transforma regular table into partitioned, but allows to attach regular table to a partitioned one. Thus, the plan is:

1. Rename table as old
2. Create the table again with partion
3. Append old data to new table as partition table

### 2.1 Rename Old Table

```sql
ALTER TABLE payments RENAME TO payments_old;
ALTER INDEX payments_pkey RENAME TO payments_pkey_old;
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

* We will continue using previous sequence (payments_payment_id_seq)
* Primary key (payments_pkey) cannot be payment_id alone anymore

```
[0A000] ERROR: unique constraint on partitioned table must include all partitioning columns Detail:
PRIMARY KEY constraint on table "payments" lacks column "created" which is part of the partition key.
```

### 2.3 Attach Old Data as Partition

Extract data of 2024-03-01 to 2024-04-01 from old table, and attach as partition.

```sql
CREATE TABLE payments_202403 PARTITION OF payments
    FOR VALUES FROM ('2024-03-01') TO ('2024-04-01');
CREATE INDEX idx_payments_202403 ON payments_202403 (created);

WITH moved_rows AS (
    DELETE FROM payments_old old
        WHERE created >= '2024-03-01' AND created < '2024-04-01'
        RETURNING old.*)
INSERT
INTO payments_202403
SELECT *
FROM moved_rows;
```

## 3. Manage Partition 

But we don't want to manage these Partitions manually, we can use [pg_partman](https://github.com/pgpartman/pg_partman?tab=readme-ov-file#installation) to do it, and setup cron job with [pg_cron](https://github.com/citusdata/pg_cron?tab=readme-ov-file#installing-pg_cron).

We can use pa_partman to do [Partitioning an Existing Table](https://github.com/pgpartman/pg_partman/blob/master/doc/pg_partman_howto.md#partitioning-an-existing-table) directly, and then [Migrating An Existing Partition Set to PG Partition Manager](https://github.com/pgpartman/pg_partman/blob/master/doc/migrate_to_partman.md#migrating-an-existing-partition-set-to-pg-partition-manager), then setup Cronjob with pg_cron.

Amazon AWS RDS has simple & clear instruction as: [Managing PostgreSQL partitions with the pg_partman extension](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL_Partitions.html) and [Scheduling maintenance with the PostgreSQL pg_cron extension]()

## 4. Appendixes:

* [Postgres Partition Conversion: minimal downtime](https://www.kylehailey.com/post/postgres-partition-conversion-minimal-downtime)
* [Partition an existing table on PostgreSQL](https://rodoq.medium.com/partition-an-existing-table-on-postgresql-480b84582e8d)
* [AWS: Managing PostgreSQL partitions with the pg_partman extension](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL_Partitions.html)
* [PostgreSQL Partitioning Made Easy Using pg_partman](https://www.percona.com/blog/postgresql-partitioning-made-easy-using-pg_partman-timebased/)
* [pg_cron official site](https://github.com/citusdata/pg_cron?tab=readme-ov-file#what-is-pg_cron)
* [pg_partman official site](https://github.com/pgpartman/pg_partman?tab=readme-ov-file#postgresql-partition-manager)




