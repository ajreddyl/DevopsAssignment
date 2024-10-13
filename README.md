# OpenSupports AWS Deployment

This repository contains AWS CloudFormation templates and a CI/CD pipeline to deploy the OpenSupports application across Development, Staging, and Production environments using AWS CodePipeline.

## Table of Contents
1. [Overview](#overview)
2. [Infrastructure Components](#infrastructure-components)
3. [CI/CD Pipeline](#cicd-pipeline)
4. [Cost Optimization](#cost-optimization)
5. [Security Best Practices](#security-best-practices)
6. [Prerequisites](#prerequisites)
7. [Deployment Steps](#deployment-steps)
8. [Monitoring and Logging](#monitoring-and-logging)
9. [Flow Diagram](#flow-diagram)
10. [Future Improvements](#future-improvements)

## Overview
This project uses AWS CloudFormation to manage and provision the infrastructure required to run OpenSupports across multiple environments. The application is deployed in the Development, Staging, and Production environments, with a CI/CD pipeline automating the process.

## Infrastructure Components
The CloudFormation templates in this repository set up the following components:
- **EC2 Instances**: Amazon Linux 2 instances to host the OpenSupports application. Spot instances are used in Development and Staging for cost savings, while On-Demand instances are used for Production.
- **RDS (MySQL)**: Relational database used by OpenSupports. Each environment has an isolated RDS instance.
- **S3 Bucket**: A single S3 bucket for storing static files, shared across all environments.
- **VPC, Subnets, and Security Groups**: Secure networking components with public subnets for the web servers and private subnets for the databases.
- **IAM Roles**: IAM roles with least-privilege access for the EC2 instances and pipeline to interact with other AWS services.
- **CloudWatch**: For monitoring application performance, logs, and setting alarms for high CPU utilization.

## CI/CD Pipeline
We use AWS CodePipeline to automate the deployment process. The pipeline stages are as follows:
1. **Source**: Pulls the source code from the OpenSupports GitHub repository.
2. **Build**: (Optional) If needed, builds the application using AWS CodeBuild.
3. **Deploy to Development**: Deploys the application and infrastructure for the Development environment using CloudFormation.
4. **Staging Approval**: After successful deployment to Development, manual approval is required to promote to Staging.
5. **Deploy to Staging**: Deploys the application and infrastructure for the Staging environment.
6. **Production Approval**: After successful deployment and testing in Staging, manual approval is required to promote to Production.
7. **Deploy to Production**: Deploys the application and infrastructure for the Production environment.

## Pipeline Flow Diagram
Here’s an illustration of the CI/CD pipeline:

```mermaid
graph TD
    A[Source] --> B[Build]
    B --> C[Deploy to Development]
    C --> D[Manual Approval for Staging]
    D --> E[Deploy to Staging]
    E --> F[Manual Approval for Production]
    F --> G[Deploy to Production]

## Architecture Diagram
Below is the architecture diagram for the OpenSupports application infrastructure.

![Architecture Diagram](assets/architecture-diagram.png)

## Deployment Process
1. **Fork the Repository**: Fork the [OpenSupports](https://github.com/opensupports/opensupports) repository to your GitHub account.
2. **Create CloudFormation Templates**: Develop templates for EC2 instances, RDS, S3, VPC, and CloudWatch.
3. **Set Up Multiple Environments**: Use CloudFormation for Development, Staging, and Production environments.
4. **CI/CD Pipeline Setup**: Automate deployments and promote changes across environments.

## CI/CD Pipeline
The CI/CD pipeline utilizes AWS CodePipeline to automate the deployment process. It includes stages for source, build, and deployment, with manual approval steps for promotions.

## Usage Instructions
To deploy the application:
- Clone the repository.
- Update parameters in the CloudFormation templates.
- Deploy using AWS Management Console or AWS CLI.

## Contributing
If you'd like to contribute, please fork the repo and submit a pull request with your changes.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
