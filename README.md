# aws-lambda
Developed an AWS Lambda function to automate the identification and deletion of stale EBS snapshots, optimizing cloud storage and reducing AWS costs through resource management and automation.

AWS Cloud Cost Optimization: Identifying and Deleting Stale EBS Snapshots
This project implements an AWS Lambda function to automate the identification and deletion of stale EBS snapshots that are no longer associated with any active EC2 instance. By doing this, unnecessary storage costs can be eliminated, optimizing cloud resources.

Table of Contents
Project Overview
Architecture
Features
Tech Stack
Installation and Setup
Usage
AWS Cost Savings
License
Project Overview
In cloud environments, EBS snapshots are used for data backup and disaster recovery. However, unused or stale snapshots can pile up over time, increasing storage costs. This project provides an automated solution to:

Identify stale snapshots that are no longer associated with active EC2 instances.
Delete these stale snapshots to reduce AWS storage costs.
Architecture
The project follows a simple architecture using AWS Lambda and Boto3:

AWS Lambda function retrieves all EBS snapshots owned by the AWS account.
It retrieves all active EC2 instances (both running and stopped) to determine which snapshots are in use.
Stale EBS snapshots (those not linked to any EC2 volume) are identified.
The Lambda function automatically deletes these stale snapshots to save on storage costs.
Features
Automated Detection: Automatically fetches and identifies stale EBS snapshots.
Cost Optimization: Helps reduce unnecessary storage costs by deleting unused resources.
Scalable: Can be applied to environments with large numbers of EC2 instances and EBS snapshots.
Cloud-Native: Uses AWS Lambda and Boto3 for seamless integration with AWS services.
Tech Stack
AWS Lambda: For automation and scalability.
Boto3 (AWS SDK for Python): To interact with AWS services like EC2 and EBS.
Amazon EC2: For instance and volume management.
Amazon EBS: For storage management and snapshot handling.
Python: For writing the Lambda function.
Installation and Setup
Prerequisites
AWS Account: Ensure you have an AWS account with the necessary IAM permissions for Lambda, EC2, and EBS.
AWS CLI: Install the AWS CLI and configure it with your account credentials.
Boto3: Make sure the Boto3 library is installed in your Python environment.
Steps
Clone the Repository:

git clone https://github.com/yourusername/aws-cloud-cost-optimization.git
cd aws-cloud-cost-optimization
Create a Lambda Function:

Navigate to AWS Lambda console.
Create a new Lambda function and set the runtime to Python 3.x.
Upload the provided Python script (lambda_function.py) to the Lambda function.
Add Permissions: Ensure your Lambda function has permissions to access EC2 and EBS by attaching an IAM role with the required policies.

Set up Triggers: Optionally, you can set up a CloudWatch trigger to automatically run the function at regular intervals (e.g., daily, weekly).

Usage
Once the Lambda function is set up and deployed, you can invoke it manually or configure it to run periodically. The function will:

Retrieve all snapshots and active EC2 instances.
Check if each snapshot is linked to any active EC2 volumes.
Delete any stale snapshots that are no longer associated with active volumes.
You can monitor the cost savings through the AWS Billing Dashboard and view logs via AWS CloudWatch.

Example Lambda Invocation:
python
Copy code
import boto3

def lambda_handler(event, context):
    ec2 = boto3.client('ec2')
    # Fetch all snapshots
    snapshots = ec2.describe_snapshots(OwnerIds=['self'])['Snapshots']
    
    # Fetch active EC2 instances
    instances = ec2.describe_instances(Filters=[{'Name': 'instance-state-name', 'Values': ['running', 'stopped']}])
    
    # Logic to detect and delete stale snapshots goes here
AWS Cost Savings
By regularly identifying and deleting stale EBS snapshots, this project can result in:

Immediate savings on AWS storage costs.
Continuous cost optimization as old, unused snapshots are cleared automatically.
You can use AWS Cost Explorer to track the reductions in your monthly bill.

License
This project is licensed under the MIT License - see the LICENSE file for details.

How to Customize This:
Replace the repository URL (in the cloning step) with your own GitHub link.
Adjust the description or example code if necessary.
