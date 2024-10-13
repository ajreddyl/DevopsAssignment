DevOps Assignment: OpenSupports Deployment
This project demonstrates how to set up the infrastructure for the OpenSupports application using AWS CloudFormation and how to deploy the application across multiple environments using a CI/CD pipeline.

Table of Contents
Overview
Prerequisites
Project Structure
CloudFormation Setup
Infrastructure Resources
Deploying with CloudFormation
CI/CD Pipeline
Pipeline Flow
Pipeline Setup
Deploying OpenSupports Application
Security Best Practices
Cost Optimization
Conclusion
Overview
This project involves:

Setting up infrastructure using AWS CloudFormation for the OpenSupports application (a ticketing system).
Deploying the application across three environments: development, staging, and production.
Implementing a CI/CD pipeline to automate deployments and promotions between environments.
Ensuring security best practices and cost optimizations.

Above: Architecture overview for the OpenSupports multi-environment deployment.

Prerequisites
Before starting, ensure you have the following:

AWS Account: For provisioning resources like EC2, RDS, S3, etc.
AWS CLI: To interact with AWS from the command line.
Terraform: If you plan to manage infrastructure through Terraform.
GitHub: For version control and CI/CD setup (e.g., GitHub Actions).
Docker: For containerized application deployments (optional).
Tools and Technologies Used:
AWS CloudFormation: Infrastructure as Code (IaC) to provision resources.
GitHub Actions / AWS CodePipeline: For automating deployments.
EC2, RDS, S3: Core AWS services for hosting and storing application data.
CloudWatch: For monitoring infrastructure and application performance.
Project Structure

DevOpsAssignment/
├── cloudformation/            # CloudFormation templates for provisioning resources
│   ├── vpc.yaml               # VPC, subnets, security groups, and IAM roles
│   ├── ec2.yaml               # EC2 instances setup
│   ├── rds.yaml               # RDS (MySQL) setup
│   ├── s3.yaml                # S3 bucket for static files
│   └── cloudwatch.yaml        # CloudWatch monitoring setup
├── .github/
│   └── workflows/
│       └── deploy.yml         # GitHub Actions pipeline for CI/CD
├── opensupports/              # Forked OpenSupports application code
├── README.md                  # Project documentation
└── LICENSE
CloudFormation Setup
Infrastructure Resources
The following AWS resources will be provisioned using CloudFormation templates:

EC2 Instances: Hosts the OpenSupports application.
RDS (MySQL): Manages the application’s database.
S3 Bucket: Stores static files (images, documents).
VPC, Subnets, and Security Groups: Ensures network isolation and security.
IAM Roles: Manages secure access for EC2 and RDS.
CloudWatch: For application and infrastructure monitoring.

Above: AWS Resources provisioned using CloudFormation templates.

Deploying with CloudFormation
Clone the repository:

bash
Copy code
git clone https://github.com/ajreddyl/DevopsAssignment.git
cd DevopsAssignment
Deploy VPC (network layer):

bash
Copy code
aws cloudformation create-stack --stack-name OpenSupportsVPC --template-body file://cloudformation/vpc.yaml --parameters file://cloudformation/vpc-params.json
Deploy EC2 instances:

bash
Copy code
aws cloudformation create-stack --stack-name OpenSupportsEC2 --template-body file://cloudformation/ec2.yaml --parameters file://cloudformation/ec2-params.json

Above: EC2 instances deployed through CloudFormation.

CI/CD Pipeline
Pipeline Flow
The CI/CD pipeline automates the following steps:

Deploys the OpenSupports application to the development environment.
Runs tests and verifies the deployment.
Promotes the application to the staging environment after passing tests.
If tests pass in staging, the application is promoted to production.

Above: CI/CD pipeline flow from development to production.

Pipeline Setup
If using GitHub Actions, the pipeline configuration file (deploy.yml) is located in .github/workflows/.

Create Environment Secrets in GitHub:

AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
ENV (development, staging, production)
Configure GitHub Actions: The workflow (deploy.yml) automatically deploys the application to the respective environments based on the defined branches:

dev branch: Deploys to development.
staging branch: Deploys to staging.
main branch: Deploys to production.
Example workflow step:

yaml
Copy code
- name: Deploy to EC2
  run: |
    aws cloudformation update-stack --stack-name OpenSupportsEC2 --template-body file://cloudformation/ec2.yaml
Deploying OpenSupports Application
Deploy to Development:

Ensure the dev branch has the latest code changes.
Push changes to trigger the pipeline and deploy to the development environment.
Promote to Staging:

Once deployment is verified, push the code to the staging branch to trigger promotion to the staging environment.
Promote to Production:

After successfully testing in staging, push to the main branch to deploy the application to the production environment.
Security Best Practices
Use IAM Roles with the least privilege necessary for EC2, RDS, and S3 access.
Enable encryption for S3 buckets and RDS databases.
Set up security groups to limit access to EC2 instances and databases.
Use CloudWatch alarms to monitor resource utilization and downtime.

Above: Example security best practices for AWS resources.

Cost Optimization
Use Auto Scaling for EC2 instances to scale resources based on demand.
Consider using Spot Instances in non-production environments (development, staging) to reduce costs.
Set up S3 Lifecycle Policies to manage and reduce storage costs for old data.
Conclusion
This project demonstrates a scalable, secure, and automated way to deploy and manage the OpenSupports application across multiple environments using AWS CloudFormation and CI/CD pipelines.
