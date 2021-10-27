---
title: Create AWS RDS Postgres Database
layout: post
---

Just need a AWS Postgres Database for testing. 

If you choose **RDS -> Create Database -> Engine type: PostgreSQL**, it will cost around 100$. Another way is, we can choose **Engine Type: Amazon Aurora**, Aurora has 2 version,  PostgreSQL-Compatible Edition can satisfy my requirement. 

To create, just following official document : [Creating a DB cluster and connecting to a database on an Aurora PostgreSQL DB cluster](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_GettingStartedAurora.CreatingConnecting.AuroraPostgreSQL.html).  Only one thing don't forget, fill database name in : **Additional configuration -> Initial database name**, otherwise you have to create manually. 

![create-aws-rds-postgres-db-1](http://villim.github.io/img/2021/create-aws-rds-postgres-db-1.png)

Finally, it will looks like follwing picture.

![create-aws-rds-postgres-db-2](http://villim.github.io/img/2021/create-aws-rds-postgres-db-2.png)

* Hostname is: Connectivity & security -> Endpoint
* Port is:  Connectivity & security -> Port
* Database is: Configuration -> DB name
* User name and Password was filled in when creating DB.


I was creating with default configuration, when I trying to connect, encountered a error:
```
	AWS RDS [08001] The connection attempt failed. The connection attempt failed.
```

First, it could be not allowd to access publicly. Make sure **Connectivity & security -> Publicly accessible**  is **YES**.

Secound, It could be **VPC Security Group** configuration issue.  Please go to:

1. Connectivity & security -> VPC security groups
2. Click the link : default (sg-xxxxxxxxxxxxxx)
3. Go to tab Security Groups -> Inbound Rules -> Edit inbound rules
4. Add one rule for Postgres: Type: PostgreSQL allow incoing address or just your own IP address

![create-aws-rds-postgres-db-3](http://villim.github.io/img/2021/create-aws-rds-postgres-db-3.png)

