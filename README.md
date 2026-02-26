🔐 Secure AWS Multi-Tier Architecture & Threat Monitoring
📌 Project Overview

This project demonstrates the design and implementation of a secure multi-tier cloud architecture on Amazon Web Services (AWS) with integrated monitoring capabilities to detect unauthorized access attempts.

The architecture applies defense-in-depth principles by combining network isolation, secure storage, identity-based access control, and centralized audit logging.

Two simulated attack scenarios were performed using an unprivileged IAM user to validate the effectiveness of the implemented security controls.

🎯 Objectives

Design an isolated virtual network using AWS VPC

Implement public and private subnets

Control internet exposure using routing mechanisms

Secure storage using encryption and access restrictions

Apply the Principle of Least Privilege using IAM

Enable activity monitoring using AWS CloudTrail

Simulate unauthorized access attempts

Verify detection through audit logs

🧱 Architecture Overview

Internet → Internet Gateway → Public Subnet (Web Tier)
         → Private Subnet (Secure Backend Tier)
         → Encrypted S3 Storage
         → CloudTrail Logs (Monitoring & Audit)


⚙️ Implementation Details
1. Virtual Private Cloud (VPC)

A custom VPC was created to isolate resources from the default AWS network.

Configuration:

CIDR Block: 10.0.0.0/16

Tenancy: Default

VPC details showing CIDR block
![Screenshot1](https://github.com/user-attachments/assets/5fe0abc5-d0c0-4081-b8de-c6f2490faa7b)

2. Subnet Configuration

Two subnets were deployed within the VPC to separate public and secure resources.

Public Subnet

CIDR: 10.0.1.0/24

Auto-assign public IP enabled

Intended for internet-accessible components

Private Subnet

CIDR: 10.0.2.0/24

No direct internet route

Intended for sensitive backend resources

Subnets list showing both subnets
![Screenshot2](https://github.com/user-attachments/assets/274a765c-2c56-44d2-aeee-6f3b0d18cb5b)

3. Internet Gateway & Routing

An Internet Gateway (IGW) was attached to provide external connectivity to the VPC.

Public Route Table

Route: 0.0.0.0/0 → Internet Gateway

Associated with Public Subnet

Private Route Table

No internet route configured

Associated with Private Subnet

Public Route Table showing IGW route
![Screenshot3](https://github.com/user-attachments/assets/d986020d-9266-411a-97c6-b8acf8b89451)

4. Secure S3 Storage

An Amazon S3 bucket was configured for secure data storage.

Security Measures Implemented:

Block all public access enabled

Server-side encryption using SSE-S3

Access restricted via IAM policies only

Bucket permissions page showing public access blocked
![Screenshot4](https://github.com/user-attachments/assets/00afa532-9246-4c78-8b0b-6ab2da8997ed)

5. IAM Least Privilege Policy

A custom IAM policy was created granting minimal permissions:

s3:GetObject

s3:PutObject

This policy demonstrates controlled access according to the Principle of Least Privilege.

IAM policy JSON or permission summary
![Screenshot5](https://github.com/user-attachments/assets/1ace8bcd-d468-4d05-84bb-40592106af66)

6. CloudTrail Monitoring Setup

AWS CloudTrail was enabled to capture all management API activity.

Configuration:

Management events enabled

Read and Write events enabled

Logs stored in a dedicated S3 bucket

Log file validation enabled

CloudTrail trail overview page
![Screenshot6](https://github.com/user-attachments/assets/ddf70ac8-5ba3-439b-983c-1b60f85ada63)

🚨 Security Incident Simulation

To validate the effectiveness of the implemented security controls, an unprivileged IAM user named attacker-user was created with zero permissions.

Two unauthorized access attempts were performed.

Attack Scenario 1 — Unauthorized S3 Access

Action Attempted:

The attacker attempted to access and enumerate S3 buckets.

Result:

Access denied due to lack of permissions

Bucket listing blocked by IAM

Sensitive storage remained protected

Access Denied message from attacker account (S3 page)
![Screenshot](https://github.com/user-attachments/assets/7aa68d73-6b7c-4665-86f4-da98d1391cc6)

Attack Scenario 2 — Unauthorized EC2 Access

Action Attempted:

The attacker attempted to view EC2 instances and resources.

Result:

Access denied by IAM

EC2 resources remained inaccessible

No infrastructure exposure occurred

Access Denied message from EC2 console
![Screenshot](https://github.com/user-attachments/assets/399b899a-9eed-4742-9be0-93390a409355)

🔍 Log Verification Using CloudTrail

CloudTrail logs confirmed both unauthorized access attempts.

The logs captured detailed forensic information, including:

Event name (e.g., ListBuckets, DescribeInstances)

Timestamp of activity

Source IP address

Identity of the caller (attacker-user)

Error code: AccessDenied

CloudTrail event history showing denied events
![Screenshot](https://github.com/user-attachments/assets/e32d5700-e97d-4083-a411-7cf64761efcc)

![Screenshot](https://github.com/user-attachments/assets/9477aa96-820e-4ec3-b942-248bbd65fccc)

🛡️ Security Controls Implemented

Network segmentation using VPC

Controlled internet exposure via routing

Encryption of stored data

Identity-based access control (IAM)

Principle of Least Privilege enforcement

Comprehensive audit logging

Detection of unauthorized activities

✅ Results

The architecture successfully prevented unauthorized access attempts to both storage and compute resources.

All malicious actions performed by the unprivileged user were:

Blocked by IAM policies

Logged by CloudTrail

Traceable for forensic analysis

🏆 Key Learnings

Importance of network isolation in cloud security

Effective use of IAM for access control

Role of audit logs in incident response

Defense-in-depth architecture principles

Real-world simulation of unauthorized access scenarios

🔮 Possible Enhancements

Future improvements could include:

NAT Gateway for controlled private subnet internet access

AWS GuardDuty for advanced threat intelligence

AWS WAF for web application protection

Security Groups and Network ACL hardening

Integration with SIEM tools for centralized monitoring

📌 Conclusion

This project demonstrates how a secure multi-tier architecture can be implemented in AWS using core security services. By combining network isolation, strict IAM policies, encrypted storage, and activity monitoring, the system effectively prevents and detects unauthorized access attempts.

Such architectures form the foundation of enterprise-grade cloud security deployments.

👨‍💻 Author

Aman Lodha
Cloud Security
