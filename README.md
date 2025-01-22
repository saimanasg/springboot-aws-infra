# Full Stack Spring Boot WebApp with AWS and Terraform Integration

This repository is a multi-module project consisting of three submodules:
1. A Spring Boot web application integrated with PostgreSQL and AWS services (SNS, Lambda, S3).
2. Terraform scripts to automate the creation of AWS infrastructure such as S3, SNS, IAM policies, KMS, RDS, Lambda, Load Balancers, Route53, Security Groups, VPC, and Secret Manager.
3. A Python Lambda function that sends an email for user verification upon user creation.

---

## Submodule 1: Spring Boot WebApp with PostgreSQL and AWS Integration

This submodule contains a Spring Boot application that provides several API endpoints for user management, file uploads, and integration with AWS services.

### API Endpoints
1. **Health Check**  
   - Verifies PostgreSQL database connectivity

2. **User Management**  
   - **Create User**: Adds a user to the PostgreSQL database and triggers an AWS SNS notification (which invokes a Lambda function for email verification).  
   - **Edit User**: Updates user details (requires Basic Authentication).

3. **File Upload**  
   - Uploads a profile picture to PostgreSQL and AWS S3 (requires Basic Authentication).  

### GitHub Workflows

#### 1. **Validate Packer Script**
Validates Packer configuration files to ensure they are correctly formatted and functional.

#### 2. **Build and Package Workflow**
This workflow runs when a pull request is merged into the `main` branch, performing the following steps:
1. Sets up a PostgreSQL service for testing.
2. Checks out the code, sets up JDK 21, and caches Maven dependencies.
3. Runs unit tests and packages the Spring Boot application into a JAR.
4. Builds an AMI using Packer.
5. Updates the Auto Scaling Group (ASG) with the new AMI and triggers an instance refresh.

---

## Submodule 2: Terraform Infrastructure Code

This submodule contains Terraform scripts to automate the creation of the following AWS resources:

### Infrastructure Components:
- **S3**: For file storage.
- **SNS**: For message notifications (used by the Spring Boot application).
- **IAM Policies**: For managing access controls.
- **KMS**: For encryption key management.
- **RDS**: For PostgreSQL database.
- **Lambda Function**: For sending user verification emails.
- **Load Balancers**: To distribute traffic.
- **Route53**: To manage DNS records and update A records after importing an SSL certificate into ACM.
- **Security Groups**: For controlling access to resources.
- **VPC**: For isolating the infrastructure network.
- **Secrets Manager**: For managing sensitive information like database credentials.

The Terraform scripts automate the creation of these resources, simplifying infrastructure provisioning.

---

## Submodule 3: Lambda Function for Email Verification

This submodule contains a Python Lambda function that sends an email to the user for email verification upon user creation. The Lambda function is triggered by the AWS SNS topic when a user is created in the Spring Boot application.

### Lambda Function Details:
- **Trigger**: The function is triggered by an SNS notification sent after a new user is created.
- **Action**: Sends a verification email to the user with a verification link.

---


