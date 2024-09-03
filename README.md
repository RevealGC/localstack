# localstack

## 1. Install Docker

LocalStack runs as a Docker container, so you need Docker installed on your system.

- **Install Docker Desktop**: If you haven't already, download and install [Docker Desktop](https://docs.docker.com/desktop/install/windows-install/). 

## 2. Install LocalStack
You can install LocalStack using pip if you're using Python, or directly pull the Docker image. 

    pip install localstack

## 3. Setup a virtual environment

    python3 -m venv .venv
    .\.venv\Scripts\activate
    pip install -r requirements.txt

## 5. start localstack
You can start LocalStack with Docker Compose from your terminal in VS Code.

    docker-compose up

when you are done with your localstack,you can remove it to reclaim resources by using the follwing command in your terminal
    docker-compose down

## 6. validate your localstack instance is running
    python -m localstack.cli.main config validate

## 7. create and set credentials to profile (powershell)

### Step 1: Create a New Profile

Open a terminal or command prompt and run the following command:

    aws configure --profile localstack
You'll be prompted to enter the following information:

 - AWS Access Key ID: test (or any placeholder value)
 - AWS Secret Access Key: test (or any placeholder value)
 - Default region name: us-east-1 (or any region you prefer)
 - Default output format: json (or text, yaml, etc.)

### Step 2: Set Up the LocalStack Endpoint
After creating the profile, you'll need to edit the AWS CLI configuration file to point to the LocalStack endpoint.

Edit the **~/.aws/config** file (on Linux/Mac) or **C:\Users\YourUsername\.aws\config** file (on Windows) to add the following under the [profile localstack] section:

    [profile localstack]
    region = us-east-1
    output = json
    endpoint_url = http://localhost:4566
This tells the AWS CLI to use the LocalStack endpoint at **http://localhost:4566** for all AWS service calls made using the '**localstack**' profile.

### Step 3: Verify the Configuration

You can verify that the AWS CLI is properly configured to use LocalStack by running a simple command like listing S3 buckets:

    aws s3 ls --profile localstack --endpoint-url=http://localhost:4566
If everything is set up correctly, you should see an empty list or a list of buckets you've created in LocalStack.

## 8. Use the Profile in Your Code
When using SDKs like Boto3 in Python, you can specify the profile to use:

    import boto3

    session = boto3.Session(profile_name='localstack')
    s3 = session.client('s3', endpoint_url='http://localhost:4566')
This setup should have you ready to work with LocalStack using the AWS CLI!

# AWS Services covered
below is a list of AWS services that can be emulated using the community edition of localstack - additional services are available for pro users. For more inforamtion on the extent of emulation, please see the [localstack docs on feature coverage](https://docs.localstack.cloud/user-guide/aws/feature-coverage/).

 - AWS Certificate Manager (ACM)
 - API Gateway
 - CloudFormation
 - CloudWatch
 - Config
 - DynamoDB
 - DynamoDB Streams
 - Elastic Compute Cloud (EC2)
 - Elasticsearch Service (ES)
 - EventBridge (Events)
 - EventBridge Pipes (Pipes)
 - Identity and Access Management (IAM)
 - Kinesis
 - Key Management Service (KMS)
 - Lambda
 - Logs
 - OpenSearch Service
 - Resource Groups
 - Resource Groups Tagging API
 - Route53
 - Route53 Resolver
 - Simple Storage Service (S3)
 - Simple Storage Service (S3) Control
 - SecretsManager
 - Simple Email Service (SES)
 - Simple Notification Service (SNS)
 - Simple Queue Service (SQS)
 - Systems Manager (SSM)
 - Systems Manager (SSM)
 - Security Token Service (STS)
 - Support
 - Simple Workflow Service (SWF)
