# AWS Multi-Region Disaster Recovery Architecture

A production-grade, multi-region disaster recovery (DR) solution on AWS, deployed through Infrastructure as Code (Terraform). Demonstrates automated failover, cross-region data replication, and resilience engineering.

## Overview

Highly available web application across two AWS regions with automated failover. If the primary region fails, traffic reroutes to the secondary region with minimal downtime.

- **Primary Region:** us-east-1 (active)
- **Secondary Region:** us-west-2 (warm standby)

## Architecture

![Architecture Diagram](docs/architecture.png)

1. Route 53 failover routing with health checks directs traffic to the healthy region.
2. Application Load Balancers distribute traffic across EC2 Auto Scaling Groups in multiple AZs.
3. RDS runs Multi-AZ in primary, async-replicated to a read replica in secondary.
4. S3 Cross-Region Replication keeps data in sync.
5. On failure, CloudWatch + SNS trigger a Lambda that promotes the RDS replica; Route 53 reroutes traffic.

## Tech Stack

Terraform | EC2 | Auto Scaling | VPC | ALB | Route 53 | RDS | S3 | Lambda | CloudWatch | SNS

## Recovery Objectives

- **RTO:** TBD after failover testing
- **RPO:** TBD after failover testing

## Project Status

In active development.

## License

MIT
