---
title: Test AWS SQS Locally with LocalStack
layout: post
---

![LocalStack](http://villim.github.io/img/2024/localstack.png)

In case we want to use AWS SQS locally, we can try with [LocalStack](https://github.com/localstack/localstack).
 
LocalStack is a cloud software development framework to develop and test your AWS applications locally. But we need notice that, LocalStack just mimic AWS features, cannot guarantee exactly the same function.

## 1. Install Localstack

Just follow the [official document for installation](https://github.com/localstack/localstack?tab=readme-ov-file#installation):

```bash
brew install localstack/tap/localstack-cli
```
if encounter problem, just try reinstall first:

```bash
brew reinstall localstack-cli
```

Once it's installed, we can start it:

```bash
localstack --version
localstack start -d
```


## 2. Install  AWS-CLI or AWSCLI-LOCAL

Install AWS-CLI [from Amazon ](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
or  can choose [AWSCLI-LOCAL ](https://github.com/localstack/awscli-local) which is a thin wrapper around the aws command line interface for use with LocalStack.

Here we just need using SQS, AWS-CLI is satisfied and prefered.

Make sure following 2 configuration files are correct:

2.1 File .aws/config

```text
 [localstack]
 region = us-east-1
 output = json
 endpoint_url = http://localhost:4566
```

2.2 File .aws/credentials

```text
 [localstack]
 aws_access_key_id = test
 aws_secret_access_key = test
```
* [localstack] means we need pass parameter **--profile localstack**
* Change [localstack] to [default] to get rid of --profile parameter

## 3. Quick Start with  SQS

### 3.1  Create Queue

```bash
aws sqs create-queue --queue-name localstack-sqs-test-queue --profile localstack
```
### 3.2 View Queues

```bash
aws sqs list-queues --profile localstack
```
should see response as:

```json
{
    "QueueUrls": [
        "http://sqs.us-east-1.localhost.localstack.cloud:4566/000000000000/localstack-sqs-test-queue"
          ]
}
```

### 3.3 Send & Receive Messages

```bash
aws sqs send-message --queue-url http://sqs.us-east-1.localhost.localstack.cloud:4566/000000000000/localstack-sqs-test-queue --message-body 'testing message'

aws sqs receive-message --queue-url http://sqs.us-east-1.localhost.localstack.cloud:4566/000000000000/localstack-sqs-test-queue
```
