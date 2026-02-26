🔐 Secure AWS Multi-Tier Architecture & Threat Monitoring

An industry-style secure cloud architecture built on Amazon Web Services (AWS) demonstrating network isolation, secure storage, least-privilege access control, and activity monitoring.
The project simulates unauthorized access attempts and verifies detection using audit logs.

🚀 Key Features
🌐 Network Isolation (VPC)

Custom Virtual Private Cloud (VPC)

Public and Private subnet architecture

Controlled internet exposure

Segmented network design to reduce attack surface

🔒 Secure Storage

Encrypted Amazon S3 bucket

Block all public access enabled

Access restricted via IAM policies

Protection against data exposure

👤 Identity & Access Management

Custom least-privilege IAM policy

Role-based access control

Unauthorized users denied by default

📜 Audit Logging & Monitoring

AWS CloudTrail enabled for API activity tracking

Read and Write management events captured

Dedicated log storage bucket

Log file integrity validation enabled

🚨 Intrusion Simulation

Creation of unprivileged attacker IAM user

Unauthorized access attempts to resources

Security controls validated through denial of access

Activity recorded for forensic analysis

🧠 Technology Stack

Cloud Platform: Amazon Web Services (AWS)

Networking: VPC, Subnets, Route Tables, Internet Gateway

Storage: Amazon S3

Security: IAM, Encryption (SSE-S3)

Monitoring: AWS CloudTrail

🏗️ Architecture Overview
Internet
   ↓
Internet Gateway
   ↓
Public Subnet (Internet-facing tier)
   ↓
Private Subnet (Secure backend tier)
   ↓
Encrypted S3 Storage
   ↓
CloudTrail Logs (Monitoring & Audit)
⚙️ Implementation Steps
🧱 VPC Creation

Created custom VPC with CIDR block 10.0.0.0/16

Isolated environment from default AWS network

📸 Screenshot: VPC details page showing CIDR block

🌐 Subnet Configuration
Public Subnet

CIDR: 10.0.1.0/24

Auto-assign public IP enabled

Intended for internet-accessible components

Private Subnet

CIDR: 10.0.2.0/24

No direct internet route

Intended for secure backend resources

📸 Screenshot: Subnets list showing both subnets

🌍 Internet Gateway & Routing
Public Route Table

Route: 0.0.0.0/0 → Internet Gateway

Associated with Public Subnet

Private Route Table

No internet route configured

Associated with Private Subnet

📸 Screenshot: Public Route Table showing IGW route

🔐 Secure S3 Storage

Security measures implemented:

Block all public access enabled

Server-side encryption (SSE-S3)

Access restricted through IAM only

📸 Screenshot: Bucket permissions page showing public access blocked

👤 IAM Least Privilege Policy

Custom IAM policy created allowing only:

s3:GetObject

s3:PutObject

Demonstrates strict access control.

📸 Screenshot: IAM policy JSON or permissions summary

📜 CloudTrail Monitoring Setup

CloudTrail configured to record all management API activity.

Management events enabled

Read and Write events enabled

Logs stored in dedicated S3 bucket

Log file validation enabled

📸 Screenshot: CloudTrail trail overview page

🚨 Security Incident Simulation

An unprivileged IAM user named attacker-user was created with zero permissions to simulate malicious activity.

🔴 Attack Scenario 1 — Unauthorized S3 Access

Action Attempted:

Attempt to view and enumerate S3 buckets

Result:

Access denied by IAM policies

Bucket listing blocked

Data remained protected

📸 Screenshot: Access Denied message from S3 console

🔴 Attack Scenario 2 — Unauthorized EC2 Access

Action Attempted:

Attempt to view EC2 instances and infrastructure

Result:

Access denied by IAM

Compute resources inaccessible

Infrastructure remained secure

📸 Screenshot: Access Denied message from EC2 console

🔍 Log Verification Using CloudTrail

CloudTrail logs confirmed both unauthorized attempts.

Captured forensic details include:

Event name (e.g., ListBuckets, DescribeInstances)

Timestamp of activity

Source IP address

Caller identity (attacker-user)

Error code: AccessDenied

📸 Screenshot: CloudTrail event history showing denied events

🛡️ Security Controls Implemented

Network segmentation using VPC

Controlled internet exposure

Encryption of stored data

Identity-based access control

Principle of Least Privilege enforcement

Comprehensive audit logging

Unauthorized activity detection

✅ Results

The architecture successfully prevented unauthorized access to both storage and compute resources.

All malicious actions performed by the unprivileged user were:

Blocked by IAM policies

Logged by CloudTrail

Traceable for forensic investigation

🧪 Use Cases

Cloud security demonstrations

Network architecture studies

IAM policy testing

Incident response practice

Educational projects

Cybersecurity portfolio project

🔮 Possible Enhancements

NAT Gateway for private subnet internet access

AWS GuardDuty for advanced threat detection

AWS WAF for web application protection

Security Groups and Network ACL hardening

SIEM integration for centralized monitoring

⚠️ Disclaimer

This project is intended for educational and authorized testing purposes only.
All activities were performed within a controlled AWS environment owned by the project author.

👨‍💻 Author

AMAN LODHA
Cloud Security 
