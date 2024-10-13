                                                                                   OpenSupports AWS Deployment

This repository contains AWS CloudFormation templates and a CI/CD pipeline to deploy the OpenSupports application across Development, Staging, and Production environments using AWS CodePipeline.

Table of Contents
Overview
Infrastructure Components
CI/CD Pipeline
Cost Optimization
Security Best Practices
Prerequisites
Deployment Steps
Monitoring and Logging
Flow Diagram
Future Improvements
Overview
This project uses AWS CloudFormation to manage and provision the infrastructure required to run OpenSupports across multiple environments. The application is deployed in the Development, Staging, and Production environments, with a CI/CD pipeline automating the process.

Infrastructure Components
The CloudFormation templates in this repository set up the following components:

EC2 Instances: Amazon Linux 2 instances to host the OpenSupports application. Spot instances are used in Development and Staging for cost savings, while On-Demand instances are used for Production.
RDS (MySQL): Relational database used by OpenSupports. Each environment has an isolated RDS instance.
S3 Bucket: A single S3 bucket for storing static files, shared across all environments.
VPC, Subnets, and Security Groups: Secure networking components with public subnets for the web servers and private subnets for the databases.
IAM Roles: IAM roles with least-privilege access for the EC2 instances and pipeline to interact with other AWS services.
CloudWatch: For monitoring application performance, logs, and setting alarms for high CPU utilization.
CI/CD Pipeline
We use AWS CodePipeline to automate the deployment process. The pipeline stages are as follows:

Source: Pulls the source code from the OpenSupports GitHub repository.
Build: (Optional) If needed, builds the application using AWS CodeBuild.
Deploy to Development: Deploys the application and infrastructure for the Development environment using CloudFormation.
Staging Approval: After successful deployment to Development, manual approval is required to promote to Staging.
Deploy to Staging: Deploys the application and infrastructure for the Staging environment.
Production Approval: After successful deployment and testing in Staging, manual approval is required to promote to Production.
Deploy to Production: Deploys the application and infrastructure for the Production environment.
Pipeline Flow Diagram
Here’s an illustration of the CI/CD pipeline:

mermaid
Copy code
graph TD
    A[Source] --> B[Build]
    B --> C[Deploy to Development]
    C --> D[Manual Approval for Staging]
    D --> E[Deploy to Staging]
    E --> F[Manual Approval for Production]
    F --> G[Deploy to Production]
    
Cost Optimization
Spot Instances: For Development and Staging, the CloudFormation template provisions EC2 Spot Instances to reduce costs.
Right-Sizing Resources: Each environment uses different instance types (e.g., t2.micro for Dev/Staging, t3.medium for Production) to match the environment's needs.
S3: One centralized S3 bucket is used across all environments for efficient storage and cost savings.
Security Best Practices
IAM Roles with Least Privilege: IAM roles are scoped with minimum permissions to interact with AWS resources.
Security Groups: Security groups are designed to restrict traffic. For instance, SSH access is only allowed from specific IP ranges.
Encryption: S3 buckets use server-side encryption (SSE-S3), and RDS instances have encryption at rest enabled.
Prerequisites
AWS account with the necessary permissions to create EC2, RDS, S3, CloudFormation, and IAM resources.
AWS CLI installed and configured.
GitHub repository forked to your account.
GitHub personal access token for AWS CodePipeline integration.
Deployment Steps
Fork the Repository:

Fork the OpenSupports GitHub repository.
Clone Your Fork:

bash
Copy code
git clone https://github.com/<your-username>/opensupports.git
cd opensupports
Deploy CloudFormation Templates:

Use AWS CloudFormation to deploy the vpc.yaml, ec2.yaml, rds.yaml, and other templates.
Modify the parameters for each environment (dev, staging, prod) as needed.
Set Up the CI/CD Pipeline:

Modify and deploy the codepipeline.yaml template to automate the deployment process.
Promote the Application:

After deploying to Development, test the application.
Use CodePipeline to promote the application to Staging and Production.
Monitoring and Logging
CloudWatch:
CloudWatch alarms are set up to monitor the CPU utilization of EC2 instances.
Logs from EC2 instances are sent to CloudWatch Logs for easier debugging.
Flow Diagram
Below is the infrastructure flow diagram showing how different AWS services integrate:



Future Improvements
Auto Scaling: Implement auto-scaling for Production to handle increased load.
Enhanced Security: Use AWS WAF for web application security, restricting access to unwanted traffic.
Testing in CI/CD: Add integration tests to the CI/CD pipeline.
