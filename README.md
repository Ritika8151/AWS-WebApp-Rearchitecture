# 🚀 AWS Web Application Re-Architecture (vprofile)

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white)
![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=for-the-badge&logo=rabbitmq&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green.svg)

## 📌 Project Overview
This project demonstrates the **re-architecture and cloud migration** of a multi-tier Java web application (`vprofile`) onto Amazon Web Services (AWS). 

The primary goal was to transition from a legacy local/VM-hosted setup to a modern, fully managed, highly available, and auto-scaling AWS Cloud infrastructure. By substituting self-managed backend components with AWS PaaS/SaaS services, operational complexity and single points of failure were completely eliminated.

---

## ⚡ How the Architecture Works

1. **User Request Routing**: Inbound HTTP/HTTPS requests are globally routed via **Amazon CloudFront CDN** for edge-location caching, minimizing physical network latency.
2. **Traffic Distribution**: CloudFront proxies dynamic requests to an **Application Load Balancer (ALB)**, which evenly distributes traffic across active EC2 instances managed by **AWS Elastic Beanstalk**.
3. **Auto-Scaling Strategy**: Elastic Beanstalk monitors system metrics (CPU utilization and target request count) to automatically scale EC2 capacity up or down.
4. **Session & Query Caching**: To prevent database bottlenecks, session data and recurring query results are cached in memory using **Amazon ElastiCache (Memcached)**.
5. **Asynchronous Processing**: Background jobs, tasks, and inter-service messaging are handled reliably via an **Amazon MQ (RabbitMQ)** broker.
6. **Data Persistence**: Core application data is stored in **Amazon RDS (MySQL)** configured with Multi-AZ replication for automated backups and seamless failover.
7. **Internal Domain Resolution**: **Amazon Route 53** Private Hosted Zones resolve internal endpoints (`db01.vprofile.in`, `mc01.vprofile.in`, `rmq01.vprofile.in`) securely inside the VPC.

---

## 🔒 Security Notes & Best Practices

- **Network Isolation**: Backend databases (RDS), caches (ElastiCache), and message queues (Amazon MQ) are placed in strict **Private Subnets** with no internet access.
- **Least-Privilege Security Groups**: Ingress rules strictly restrict traffic:
  - RDS accepts traffic *only* on port `3306` from Elastic Beanstalk instances.
  - ElastiCache accepts traffic *only* on port `11211` from app instances.
  - Amazon MQ accepts traffic *only* on port `5672` from app instances.
- **IAM & Secrets Management**: Database credentials and AWS API access are controlled using IAM roles and secure environment variables rather than hardcoded keys in the codebase.
- **Data Encryption**: Encryption in transit via HTTPS/TLS and encryption at rest enabled for S3 build storage and RDS database volumes.

---

## 🛠 Technology Stack & Services Used

| Category | Component / AWS Service | Purpose |
| :--- | :--- | :--- |
| **Application Stack** | Java, Apache Tomcat, Spring | Core web application stack (`vprofile`) |
| **Compute & Deploy** | AWS Elastic Beanstalk | Managed application provisioning & Auto Scaling |
| **Database** | Amazon RDS (MySQL) | Multi-AZ relational database management |
| **Caching Layer** | Amazon ElastiCache (Memcached) | In-memory key-value cache for session management |
| **Message Broker** | Amazon MQ (RabbitMQ) | Asynchronous messaging queue |
| **Content Delivery** | Amazon CloudFront | Global Content Delivery Network (CDN) |
| **DNS Management** | Amazon Route 53 | Internal private hosted zone resolution |
| **Storage & Build** | Amazon S3 | Artifact storage (`.war` deployment files) |
| **Security & Network**| AWS VPC, Security Groups | Network isolation & access control |

---

## 📂 Implementation & Service Verification Screenshots

### 1. Database Layer (Amazon RDS)
Provisioned a Multi-AZ **MySQL** instance in private subnets with continuous automated backups.
![Amazon RDS Status](rearchitecture/rds.png)

### 2. In-Memory Caching Layer (Amazon ElastiCache)
Deployed a **Memcached** cluster to lower query response times and handle user session storage.
![Amazon ElastiCache Status](rearchitecture/memcache.png)

### 3. Asynchronous Messaging Broker (Amazon MQ)
Configured a managed **RabbitMQ** broker instance for decoupled task queueing.
![Amazon MQ Status](rearchitecture/mq.png)

### 4. Application Deployment & Auto Scaling (Elastic Beanstalk)
Provisioned **Apache Tomcat** app environments with target-tracking scaling rules and ALB health checks.
![Elastic Beanstalk Status](rearchitecture/beanstalk.png)
![EC2 Instance Status](rearchitecture/ec2.png)

### 5. Content Delivery & Internal DNS Configuration
- **CloudFront Distribution**: Edge caching enabled for fast user-facing asset delivery.
- **Route 53 Hosted Zone**: Private DNS records linking internal endpoints securely.
![CloudFront Distribution](rearchitecture/cloudfront.png)
![Route 53 Hosted Zone](rearchitecture/route53.png)

### 6. Artifact Storage (Amazon S3)
Configured bucket access policies to manage versioned `.war` build files.
![Amazon S3 Bucket](rearchitecture/bucket.png)

---

## 🎯 Key Learning Outcomes

Through building and deploying this re-architecture project, the following core Cloud Engineering concepts were mastered:
- Designing **Multi-Tier Fault-Tolerant Architectures** on AWS.
- Migrating monolithic/VM applications to **AWS Managed PaaS Services**.
- Implementing **Private Subnet Security Schemes** and DB connection isolation.
- Decoupling web applications using **In-Memory Caching** and **Message Queues**.
- Managing DNS and Edge Caching using **Route 53 & CloudFront Integration**.

---

## 🚦 Project Status

- [x] AWS VPC & Network Infrastructure Setup
- [x] Multi-AZ Database & Cache Layer Provisioning
- [x] Application Build & Deployment via Elastic Beanstalk
- [x] CDN & Custom Private DNS Routing
- [x] High-Availability & Load Tests Verified

**Current Status:** `COMPLETED` 🟢 (Production-Ready Architecture)

---

## 📝 How to Replicate
1. Clone this repository:
   ```bash
   git clone [https://github.com/Ritika8151/AWS-WebApp-Rearchitecture.git](https://github.com/Ritika8151/AWS-WebApp-Rearchitecture.git)
