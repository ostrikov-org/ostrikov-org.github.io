---
tags:
  - kafka
  - aws
  - terraform
  - portfolio
  - "#gitlab"
  - ecs
title: Kafka Based Event-Driven Enterprise Service Bus (ESB)
---
# Client Story
In this project the client required an ESB capable of handling **thousands of real-time messages per second** across **fully isolated environments**.

Because **the data included sensitive** and potentially **PII-level information**, they needed *strict*, *granular access controls* and *end-to-end security*, including *encryption at-rest and in-transit*.

They also demanded a platform with *minimal manual upkeep*, **automated incident detection**, and **alerting robust enough to maintain strict SLAs**. The system had to be **highly scalable**, **fault-tolerant**, *auditable*, and supported by *compliant*, *isolated* build and access workflows.
# Solution used
- **AWS MSK (Kafka)** - based ESB connecting **isolated AWS accounts** via **cross-account IAM roles**.
- **Terraform** for infrastructure and granular per-topic **IAM access control**.
- **Jira Service Desk + Automation** for self-service access management.
- **CloudTrail**, **S3**, **GuardDuty**, **Athena** for centralized audit and security logging.
- **Kafka-UI** for topic inspection, message tracing, and debugging.
- **CloudWatch**, **Prometheus**, **Grafana** for monitoring and alerting (integrated with **Jira Alerts**) with SRE shifts to reach desired SLA level.
- **GitLab CI** pipelines with **self-hosted runners** for compliance and isolated execution.
- End-to-end encryption and AWS-managed services for **scalability**, **resilience**, and **low maintenance**.
- **Glue schema registry** for storing **Avro schemas**
# Architecture Overview
## Code Organization
The code is hosted on GitLab with GitLab CI pipelines. The main repo with infrastructure is written with **terraform** and protected with **pre-commit** (trivy, tfsec, tf-lint, etc), **SonarQube** to manage the code quality
## Infrastructure Chart
![[kafka-based-event-driven-enterprise-service-bus.png]]