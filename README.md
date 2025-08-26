# Terraform-AWS-2-Tier-Architecture-with-HA-CI-CD
A Terraform module deploying a scalable, highly available 2-tier AWS architecture (VPC, ASG, RDS, ALB) with automated CI/CD via Terraform Cloud.
# Terraform: AWS 2-Tier Highly Available Architecture

This repository contains Terraform code to deploy a **highly available, two-tier web application architecture** on AWS. The infrastructure is defined as code (IaC) using reusable modules and is designed for reliability, security, and scalability.

The deployment is automated through **Terraform Cloud**, integrated with GitHub for CI/CD, ensuring a consistent and repeatable process.

## Architecture Overview

The infrastructure consists of:
- **Web Tier:** Auto Scaling Group of EC2 instances (Apache web servers) distributed across public subnets in two Availability Zones.
- **App/Data Tier:** Amazon RDS MySQL instance deployed in private subnets for isolation and security.
- **Networking:** A custom VPC with public and private subnets, Internet Gateway (IGW), NAT Gateway for outbound traffic, and appropriate route tables.
- **Traffic Management:** An Internet-facing Application Load Balancer (ALB) to distribute traffic to the web tier instances.
- **Security:** Security groups acting as firewalls to control traffic between the ALB, web servers, and database.

![Architecture Diagram](./assets/architecture-diagram.png) *(Note: You should create a simple diagram and add it to an `/assets` folder in your repo)*

## Prerequisites

Before you begin, ensure you have the following:

1.  **AWS Account:** With an IAM user possessing sufficient permissions to create the resources.
2.  **Terraform Cloud Account:** A free account is sufficient.
3.  **GitHub Account:** To host your forked repository.
4.  **Local Environment:**
    - AWS CLI configured with credentials (`aws configure`)
    - Terraform (v1.0+ recommended)
    - Git

## Usage

### 1. Clone and Explore the Repository

```bash
git clone https://github.com/<your-username>/terraform-aws-two-tier.git
cd terraform-aws-two-tier
