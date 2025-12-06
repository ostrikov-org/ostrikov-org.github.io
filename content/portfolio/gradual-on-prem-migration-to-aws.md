---
title: Gradual on-prem migration to AWS
tags:
  - aws
  - serverless
  - cdn
  - kafka
  - ecs
  - portfolio
---
# Client Story
The client needed a phased migration from an aging on-premise environment to AWS **without disrupting day-to-day operations**, while **keep growing the existing product**.

The goal was to *move the database*, *application services*, and *scheduled processing tasks* *gradually*, **ensuring compatibility**, **security**, and **minimal downtime throughout the transition**.
# Solution Used
- **Migrated the on-prem MS SQL database to Amazon Aurora using AWS DMS**.
- **Utilized write-through cache with Redis (ElastiCache) to speed up queries**
- Containerized and deployed application services with **Docker** on **ECS Fargate**.
- **Rebuilt supporting logic as AWS Lambda functions** where appropriate.
- Exposed external functionality through **HTTP API Gateway with AD JWT authorizers**.
- **Secured all entry points** using *CloudFront*, *AWS WAF*, and *edge protections (CF Functions, Lambda@Edge)*.
- Implemented scheduled data-processing tasks with **AWS Glue Jobs**.
- Published WAL (Write Ahead Log) changes to a **Kafka** using *logical replication*
# Architecture Overview
## Code Organization
The main stack was written with **Python**, infrastructure mainly in **Terraform** and bits of **CDK (CloudFormation)**. I later *moved* the CDK bits into terraform so that our stack is entirely managed with it, instead of depending on two different technologies.

Regarding a CI/CD pipeline, two *business critical* requirements were issued:
1. **No untested code must be shipped to a production**
2. Developments must be **agile and quick**, with a [trunk-based development](https://trunkbaseddevelopment.com/) approach

The main part of the application was located in the monorepository so the CI/CD pipeline was built with those requirements in mind.
