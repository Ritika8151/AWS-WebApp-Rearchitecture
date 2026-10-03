# AWS Web Application Re-Architecture

## Project Overview

This project demonstrates the re-architecture of a web application on AWS Cloud using managed AWS services.

The application is deployed using AWS Elastic Beanstalk with an Application Load Balancer and Auto Scaling.

## Architecture

User
↓
Route 53
↓
CloudFront
↓
Application Load Balancer
↓
Elastic Beanstalk
↓
Auto Scaling EC2 Instances
↓
Apache Tomcat
↓
Web Application

Supporting AWS Services:

- Amazon RDS (MySQL) – Database
- Amazon ElastiCache – Caching
- Amazon MQ – Messaging
- Amazon S3 – Application Artifacts
- Amazon CloudWatch – Monitoring

## AWS Services Used

| AWS Service | Purpose |
|---|---|
| Route 53 | DNS management |
| CloudFront | Content delivery |
| Application Load Balancer | Traffic distribution |
| Elastic Beanstalk | Application deployment |
| EC2 | Application compute |
| Auto Scaling | Automatic scaling |
| RDS | MySQL database |
| ElastiCache | Caching |
| Amazon MQ | Messaging |
| S3 | Application artifact storage |
| CloudWatch | Monitoring and logs |

## Key Concepts

- AWS Cloud Architecture
- Application Deployment
- Load Balancing
- Auto Scaling
- Managed Database
- Caching
- Messaging
- Object Storage
- Monitoring
- DNS
- Content Delivery

## Project Outcome

The web application was re-architected and deployed on AWS using managed cloud services.

The architecture integrates application deployment, load balancing, auto scaling, database, caching, messaging, artifact storage, content delivery and monitoring services.

## Technologies

- AWS
- Elastic Beanstalk
- EC2
- Application Load Balancer
- RDS MySQL
- ElastiCache
- Amazon MQ
- S3
- CloudFront
- Route 53
- CloudWatch
