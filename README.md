# OpenSupports Application Deployment

## Table of Contents
1. [Overview](#overview)
2. [Architecture Diagram](#architecture-diagram)
3. [Deployment Process](#deployment-process)
4. [CI/CD Pipeline](#cicd-pipeline)
5. [Usage Instructions](#usage-instructions)
6. [Contributing](#contributing)
7. [License](#license)

## Overview
This repository contains AWS CloudFormation templates and a CI/CD pipeline setup for deploying the OpenSupports application across multiple environments (Development, Staging, Production).

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
