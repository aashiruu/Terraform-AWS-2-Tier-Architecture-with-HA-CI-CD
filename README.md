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
```
### 2. Set Up Terraform Cloud Workspace

1. Sign in to your Terraform Cloud account.
2. Create a new Organization if you haven't already.
3. Click "Create a workspace".
4. Choose "Version control workflow".
5. Connect your GitHub account and select this repository.
6. Configure the workspace:
   · Name: aws-two-tier-app-prod
   · Advanced Options -> Execution Mode: Remote (default)
   · Advanced Options -> Terraform Working Directory: Leave blank if root, or specify if in a subdirectory.
7. Click "Create workspace".

### 3. Configure Environment Variables in Terraform Cloud

In your Terraform Cloud workspace:

1. Navigate to Variables > Environment Variables.
2. Add the following sensitive variables from your AWS IAM user:
```
   · AWS_ACCESS_KEY_ID - (Your Access Key)
   · AWS_SECRET_ACCESS_KEY - (Your Secret Key)
   · AWS_DEFAULT_REGION - (e.g., us-east-1) Mark all three as Sensitive.
```
3. Navigate to Variables > Terraform Variables.
4. Add the following variables for the database credentials:
```
   · db_username - (e.g., admin)
   · db_password - (Choose a strong password) Mark both as Sensitive.
```
### 4. Trigger a Plan and Apply

Terraform Cloud will automatically run terraform plan when you connect the repository. To deploy:

1. From the run screen, review the plan output.
2. If the plan looks correct, click "Confirm & Apply".
3. Type a confirmation comment and click "Confirm Plan".

Terraform Cloud will now run terraform apply to provision the entire infrastructure in your AWS account.

### 5. Test the Deployment

After a successful apply, the ALB DNS name will be available in the Outputs section of the run.

1. Copy the alb_dns_name output value.
2. Paste it into your web browser.
3. You should see the Apache Ubuntu default test page, meaning traffic is successfully flowing through the ALB to your EC2 instances.
