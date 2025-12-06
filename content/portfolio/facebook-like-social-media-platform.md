---
tags:
  - aws
  - kubernetes
  - gitlab
  - terraform
  - portfolio
  - ecs
  - eks
title: Social Media Platform (Facebook-like)
---
# Client story
The client needed a **secure**, **multi-environment social platform** managed across regions with **granular access**, **clear documentation**, **DR readiness**, and **cost visibility**.

They required a **fully automated**, **scalable** application platform with **standardized environments**, **centralized observability**, and **end-to-end CI/CD for backend, serverless, and mobile apps** to support rapid releases.

Finally, they demanded **high production reliability with safe deployments**, **automatic rollbacks**, **real-time alerts**, and *actionable insights to keep a global social app stable*.
# Solution Used
- Multi-environment **AWS** platform management with **granular IAM**, cross-**team access policies**, **documentation**, **DR procedures**, and **cost reporting** for a distributed international team.
- Automated provisioning across several AWS accounts and regions using **Terraform IaC** with **custom modules** (*VPC, Route53, S3, SNS/SQS, SES, OpenVPN, EKS, ECS*) following best practices: **remote state**, **versioning**, **modular design**, and **pipeline-driven deployments**.
- Operated and optimized multiple **EKS** clusters: **Node Groups**, **Karpenter autoscaling**, **Metrics Server**, **Secrets/ConfigMaps**, **NGINX Ingress**, **ALB Ingress**, **CSI drivers**, **AWS Container Insights**, and full observability via **Prometheus**, **Grafana** with **Helm charts**.
- Built end-to-end **CI/CD** pipelines for microservices (**ECS/EKS**), **AWS Lambda**, and mobile apps using *GitLab CI with autoscaled EC2 runners and GitLab-managed macOS runners*: caching, merge trains, release automation, integration testing with Docker, SonarQube, Slack, Jira, Allure integrations, and Helm-based deployments (centralized deployment repo).

Maintained operational reliability of **ECS/EKS microservices** with safe deployments, automated rollbacks, **Slack alerts**, and comprehensive monitoring dashboards (latency, 5XX, JVM metrics) using **Prometheus**, **Grafana**, **CloudWatch** (Dashboards, Log Insights, Alarms), **FluentD** and **FluentBit**, **Istio**, and **Kiali**.
# Architecture Overview
## Code Organization
As I mentioned, there were multiple environments, following the [gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) convention, for automating things, the **Gitlab CI** was used for CI/CD pipelines. The application and microservices followed the [gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) branching and release strategy

For code quality check the **SonarQube** was integrated with the pipeline

The infrastructure was entirely written with **terraform** using a custom modules

On the following chart, for simplicity sake, only production is shown
## Infrastructure Chart
![[Pasted image 20251207000849.png]]