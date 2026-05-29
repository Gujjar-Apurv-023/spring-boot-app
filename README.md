<img width="1408" height="768" alt="Gemini_Generated_Image_1i4c9o1i4c9o1i4c" src="https://github.com/user-attachments/assets/7eeeb1f7-7da4-4534-99c0-b48c7992d363" />

# springboot-example
Spring Boot Example Application


API Endpoint: http://localhost:8080/
# 🚀 Spring Boot AWS Deployment Guide (RDS + ECR + ECS Fargate + CI/CD)

This project demonstrates deployment of a Spring Boot application using AWS services:
- AWS RDS (MySQL Database)
- AWS ECR (Docker Image Repository)
- AWS ECS Fargate (Container Deployment)
- GitHub Actions (CI/CD Pipeline)

---

# 🏗️ Architecture Flow

GitHub → GitHub Actions → Docker Build → Push to ECR → ECS Fargate → RDS MySQL → Spring Boot App

---

# 🗄️ 1. AWS RDS Setup (MySQL)

## Steps:

1. Go to AWS RDS Console → Create Database
2. Select:
   - Engine: MySQL
   - Template: Free Tier
3. Configuration:
   - DB Name: `usermanagement`
   - Initial Database Name: `user_management`
   - Public Access: Yes
4. Set credentials:
   - Username: your choice
   - Password: your secure password
5. Networking:
   - Use default VPC
   - Open port `3306` in security group

---

# 📦 2. AWS ECR Setup

## Steps:

1. Go to AWS ECR Console
2. Create Repository:
   - Name: `springboot-example`
   - Visibility: Private

---

## Docker Image Push:

```bash
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <account-id>.dkr.ecr.<region>.amazonaws.com

docker build -t springboot-example .

docker tag springboot-example:latest <ECR_URI>:latest

docker push <ECR_URI>:latest