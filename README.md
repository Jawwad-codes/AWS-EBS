AWS EBS Snapshot Cleanup Automation (DevOps Project)

Project Description

This project is a simple DevOps automation that removes unused EBS snapshots in AWS to reduce unnecessary storage costs.

As a DevOps fresher, this project helped me understand:

 AWS Lambda automation
 EC2 and EBS management
 IAM permissions
 Cost optimization practices in cloud environments
 Using Python with AWS SDK (boto3)

The automation scans all snapshots in the AWS account and deletes snapshots that are no longer associated with active resources.


Problem Statement

In many AWS environments, developers create EBS snapshots for backup or testing but forget to delete them. Over time, these unused snapshots accumulate and increase AWS storage costs.

This project automatically identifies and deletes such unused snapshots.


Solution Overview

A serverless automation using AWS Lambda that:

1. Retrieves all EBS snapshots owned by the account
2. Checks active EC2 instances
3. Identifies snapshots linked to deleted or unused volumes
4. Deletes those snapshots automatically


Architecture

CloudWatch Event / Manual Trigger
            |
            v
       AWS Lambda
            |
            v
        Boto3 SDK
            |
            v
   Amazon EC2 & EBS APIs
            |
            v
Delete Unused Snapshots


Services Used

This project uses the following AWS services:

 AWS Lambda
 Amazon EC2
 Amazon Elastic Block Store (EBS)
 AWS IAM
 Amazon CloudWatch (for logs)


How the Script Works

The Lambda function performs the following steps:

1. Connects to AWS EC2 service using boto3
2. Retrieves all EBS snapshots owned by the account
3. Retrieves all currently running EC2 instances
4. For each snapshot:

    Checks if the snapshot has an associated volume
    If the volume does not exist → delete snapshot
    If the volume exists but is not attached to a running instance → delete snapshot

This ensures only useful snapshots remain in the system.


IAM Permissions Required

The Lambda execution role needs the following permissions:

```json
{
  "Effect": "Allow",
  "Action": [
    "ec2:DescribeSnapshots",
    "ec2:DescribeInstances",
    "ec2:DescribeVolumes",
    "ec2:DeleteSnapshot"
  ],
  "Resource": "*"
}
```


Deployment Steps

1. Create an AWS Lambda function
2. Choose Python runtime
3. Upload the Python script
4. Attach an IAM role with EC2 permissions
5. Test the function with a sample event
6. (Optional) Schedule using EventBridge


Learning Outcomes

Through this project I learned:

 How to automate infrastructure tasks using AWS Lambda* How to interact with AWS services using boto3
 How IAM roles control access permissions
 How DevOps engineers reduce cloud costs through automation
 How to debug AWS Lambda permission errors


Future Improvements

Possible improvements to this project:

 Delete only snapshots older than 30 days
 Add tagging system to protect important snapshots
 Send alerts before deleting snapshots
 Add Slack or email notifications
 Implement Terraform for infrastructure automation




