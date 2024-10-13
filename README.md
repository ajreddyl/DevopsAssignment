# DevOps Assignment: OpenSupports Deployment

This project demonstrates how to set up the infrastructure for the OpenSupports application using AWS CloudFormation and how to deploy the application across multiple environments using a CI/CD pipeline.

## Table of Contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [CloudFormation Setup](#cloudformation-setup)
- [Infrastructure Resources](#infrastructure-resources)
- [Deploying with CloudFormation](#deploying-with-cloudformation)
- [CI/CD Pipeline](#ci-cd-pipeline)
- [Pipeline Flow](#pipeline-flow)
- [Pipeline Setup](#pipeline-setup)
- [Deploying OpenSupports Application](#deploying-opensupports-application)
- [Security Best Practices](#security-best-practices)
- [Cost Optimization](#cost-optimization)
- [Conclusion](#conclusion)

## Overview
This project involves:
- Setting up infrastructure using AWS CloudFormation for the OpenSupports application (a ticketing system).
- Deploying the application across three environments: development, staging, and production.
- Implementing a CI/CD pipeline to automate deployments and promotions between environments.
- Ensuring security best practices and cost optimizations.

![Architecture Overview](path_to_your_image)  <!-- Replace with actual image path -->

## Prerequisites
Before starting, ensure you have the following:
- **AWS Account:** For provisioning resources like EC2, RDS, S3, etc.
- **AWS CLI:** To interact with AWS from the command line.
- **Terraform:** If you plan to manage infrastructure through Terraform.
- **GitHub:** For version control and CI/CD setup (e.g., GitHub Actions).
- **Docker:** For containerized application deployments (optional).

## Tools and Technologies Used
- **AWS CloudFormation:** Infrastructure as Code (IaC) to provision resources.
- **AWS CodePipeline:** For automating deployments.
- **EC2, RDS, S3:** Core AWS services for hosting and storing application data.
- **CloudWatch:** For monitoring infrastructure and application performance.

## Project Structure          
- **DevOpsAssignment/                                                                    **  
- **├── cloudformation/            # CloudFormation templates for provisioning resources **
- **│   ├── vpc.yaml               # VPC, subnets, security groups, and IAM roles        **
- **│   ├── ec2.yaml               # EC2 instances setup                                 **
- **│   ├── rds.yaml               # RDS (MySQL) setup                                   **
- **│   ├── s3.yaml                # S3 bucket for static files                          **
- **│   └── cloudwatch.yaml        # CloudWatch monitoring setup                         **
- **├── .aws/                      # AWS CodePipeline configuration                      **
- **│   └── codepipeline.yml           # CodePipeline configuration file                 **
- **├── opensupports/              # Forked OpenSupports application code                **
- **├── README.md                  # Project documentation                               **
- **└── LICENSE                    # License for the project                             **
																						 **
## CloudFormation Setup
Infrastructure Resources:
The following AWS resources will be provisioned using CloudFormation templates:

- **EC2 Instances:** Hosts the OpenSupports application.
- **RDS (MySQL):** Manages the application’s database.
- **S3 Bucket:** Stores static files (images, documents).
- **VPC, Subnets, and Security Groups:** Ensures network isolation and security.
- **IAM Roles:** Manages secure access for EC2 and RDS.
- **CloudWatch:** For application and infrastructure monitoring.
