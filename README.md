# 🚀 AWS Web Application Re-Architecture (vprofile)

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white)
![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=for-the-badge&logo=rabbitmq&logoColor=white)

## 📌 Project Overview
This project demonstrates the **re-architecture and cloud migration** of a multi-tier web application (`vprofile`) onto AWS using fully managed, scalable, and highly available AWS services. The target architecture replaces self-hosted services with managed Cloud infrastructure to ensure reliability, auto-scaling, and operational efficiency.

---

## 🛠️ AWS Services & Infrastructure Setup

### 1. Database Layer (Amazon RDS)
Provisioned a Multi-AZ **MySQL Community Edition** instance in isolated private subnets.
![Amazon RDS Status](rearchitecture/rds.png)

### 2. Caching Layer (Amazon ElastiCache)
Configured a **Memcached** cluster to cache database queries and user session states.
![Amazon ElastiCache Status](rearchitecture/memcache.png)

### 3. Messaging Layer (Amazon MQ)
Deployed a managed **RabbitMQ** broker to enable asynchronous processing between application services.
![Amazon MQ Status](rearchitecture/mq.png)

### 4. Application Layer (AWS Elastic Beanstalk)
Deployed the Java application stack on **Apache Tomcat** with Auto Scaling policies.
![Elastic Beanstalk Status](rearchitecture/beanstalk.png)
![EC2 Instance Status](rearchitecture/ec2.png)

### 5. Content Delivery & DNS Management
- **Amazon CloudFront**: Configured CDN distribution pointing to the Beanstalk Load Balancer.
- **Amazon Route 53**: Managed internal routing using a Private Hosted Zone (`vprofile.in`).
![CloudFront Distribution](rearchitecture/cloudfront.png)
![Route 53 Hosted Zone](rearchitecture/route53.png)

### 6. Artifact Storage (Amazon S3)
Created secure S3 buckets for storing application build files (`.war` artifacts).
![Amazon S3 Bucket](rearchitecture/bucket.png)

---

## 🎯 Key Benefits Realized
- **High Availability**: Multi-AZ deployments for RDS and Load Balancing across availability zones.
- **Auto-Scaling**: Automatic horizontal scaling of application nodes based on traffic volume.
- **Performance Optimization**: Reduced DB load using ElastiCache and CloudFront CDN caching.
- **Managed Operations**: Offloaded database and broker maintenance to AWS managed services.
