# aws-lab3-ec2-rds-security
Hands-on: EC2 &amp; RDS Security Group setup and troubleshooting (Lab 3)
Lab 3: Secure AWS EC2 and RDS with Security Groups

Description

This repository contains the outcome of Lab 3 where we configure and secure AWS EC2 and RDS instances using least-privilege Security Group rules. You will find setup scripts, configuration notes, and screenshots illustrating the process and troubleshooting steps.

Repository Structure

README.md                     # This file
screenshots/                  # Folder containing all lab screenshots
  ├─ 01-instance-connect-denied.png
  ├─ 02-rds-db-created.png
  ├─ 03-ssh-timeout.png
  ├─ 04-ec2-sg-inbound.png
  ├─ 05-rds-sg-inbound.png
  └─ 06-sg-rules-confirm.png
scripts/                      # (Optional) any helper scripts or Terraform files

Prerequisites

An AWS account with permissions to create EC2 instances, RDS databases, and modify Security Groups.

AWS CLI installed and configured (or access via the AWS Console).

SSH key pair available for EC2 access.

MySQL client installed locally (or available on the EC2 instance).

Setup and Configuration

Launch an EC2 instance in a public subnet.

Configure launch-wizard-1 Security Group:

Allow SSH (TCP 22) only from your IP address.

Save rules.

Create an RDS MySQL instance (ime-rds-db).

Configure ime-ben-rds-sg Security Group:

Allow MySQL/Aurora (TCP 3306) only from your IP address (or from the EC2 SG for tighter security).

Save rules.

Testing Connectivity

SSH Test:

ssh -i /path/to/key.pem ec2-user@<EC2_PUBLIC_IP>

MySQL Test:

mysql -h <RDS_ENDPOINT> -P 3306 -u <DB_USER> -p

Screenshots

The screenshots/ folder includes key moments:

Instance Connect Denied: IAM-based EC2 Instance Connect failure due to missing permissions.

RDS DB Created: Confirmation of ime-rds-db availability.

SSH Timeout: Initial TCP 22 timeout before SG changes.

EC2 SG Inbound Rules: SSH rule locked to your IP.

RDS SG Inbound Rules: MySQL rule locked to your IP.

Security Group Confirmation: Green banners showing successful rule modifications.

Known Challenges

EC2 Instance Connect requires an IAM policy allowing ec2-instance-connect:SendSSHPublicKey.

Public IP rotation: Stopping/starting EC2 without an Elastic IP can change the address.

RDS non-SSH access: RDS endpoints do not accept SSH, only database connections.

Cleanup

Remember to terminate your EC2 instance, delete the RDS instance, and remove any custom Security Groups to avoid ongoing costs.

License

This lab exercise is provided under the MIT License. See LICENSE for details.

