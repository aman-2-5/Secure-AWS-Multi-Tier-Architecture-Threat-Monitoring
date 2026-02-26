🔐 Secure AWS Multi-Tier Architecture & Threat Monitoring
📌 Project Overview
This project demonstrates the design and implementation of a secure multi-tier cloud architecture on Amazon Web Services (AWS) with integrated monitoring capabilities to detect unauthorized access attempts.
The architecture emphasizes defense-in-depth by combining network isolation, secure storage, identity-based access control, and centralized audit logging.
Two simulated attack scenarios were performed using an unprivileged IAM user to validate the effectiveness of the security controls.
________________________________________
🎯 Objectives
•	Design an isolated virtual network using AWS VPC
•	Implement public and private subnets
•	Control internet exposure using routing mechanisms
•	Secure storage using encryption and access restrictions
•	Apply the Principle of Least Privilege with IAM
•	Enable activity monitoring using AWS CloudTrail
•	Simulate unauthorized access attempts
•	Verify detection through audit logs
________________________________________
🧱 Architecture Overview
The system follows a multi-tier network model:
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
________________________________________
⚙️ Implementation Details
🔹 1. Virtual Private Cloud (VPC)
A custom VPC was created to isolate resources from the default AWS network.
Configuration:
•	CIDR Block: 10.0.0.0/16
•	Tenancy: Default
📸 Screenshot: VPC details showing CIDR block
 
________________________________________
🔹 2. Subnet Configuration
Two subnets were deployed within the VPC to separate public and secure resources.
🌐 Public Subnet
•	CIDR: 10.0.1.0/24
•	Auto-assign public IP enabled
•	Intended for internet-accessible components
🔒 Private Subnet
•	CIDR: 10.0.2.0/24
•	No direct internet route
•	Intended for sensitive backend resources
📸 Screenshot: Subnets list showing both subnets
 
________________________________________
🔹 3. Internet Gateway & Routing
An Internet Gateway (IGW) was attached to provide external connectivity to the VPC.
Public Route Table
•	Route: 0.0.0.0/0 → Internet Gateway
•	Associated with Public Subnet
Private Route Table
•	No internet route configured
•	Associated with Private Subnet
📸 Screenshot: Public Route Table showing IGW route
 
________________________________________
🔹 4. Secure S3 Storage
An Amazon S3 bucket was configured for secure data storage.
Security Measures Implemented:
•	Block all public access enabled
•	Server-side encryption using SSE-S3
•	Access restricted via IAM policies only
📸 Screenshot: Bucket permissions page showing public access blocked
 
________________________________________
🔹 5. IAM Least Privilege Policy
A custom IAM policy was created granting minimal permissions:
•	s3:GetObject
•	s3:PutObject
This policy demonstrates controlled access according to the Principle of Least Privilege.
📸 Screenshot: IAM policy JSON or permission summary
 
________________________________________
🔹 6. CloudTrail Monitoring Setup
AWS CloudTrail was enabled to capture all management API activity.
Configuration:
•	Management events enabled
•	Read and Write events enabled
•	Logs stored in a dedicated S3 bucket
•	Log file validation enabled
📸 Screenshot: CloudTrail trail overview page
 
________________________________________
🚨 Security Incident Simulation
To validate the effectiveness of the implemented security controls, an unprivileged IAM user named attacker-user was created with zero permissions.
Two unauthorized access attempts were performed.
________________________________________
🔴 Attack Scenario 1 — Unauthorized S3 Access
Action Attempted:
The attacker attempted to access and enumerate S3 buckets.
Result:
•	Access denied due to lack of permissions
•	Bucket listing blocked by IAM
•	Sensitive storage remained protected
📸 Screenshot: Access Denied message from attacker account (S3 page)
 
________________________________________
🔴 Attack Scenario 2 — Unauthorized EC2 Access
Action Attempted:
The attacker attempted to view EC2 instances and resources.
Result:
•	Access denied by IAM
•	EC2 resources remained inaccessible
•	No infrastructure exposure occurred
📸 Screenshot: Access Denied message from EC2 console
 
________________________________________
🔍 Log Verification Using CloudTrail
CloudTrail logs confirmed both unauthorized access attempts.
The logs captured detailed forensic information, including:
•	Event name (e.g., ListBuckets, DescribeInstances)
•	Timestamp of activity
•	Source IP address
•	Identity of the caller (attacker-user)
•	Error code: AccessDenied
📸 Screenshot: CloudTrail event history showing denied events
 
 
________________________________________
🛡️ Security Controls Implemented
•	Network segmentation using VPC
•	Controlled internet exposure via routing
•	Encryption of stored data
•	Identity-based access control (IAM)
•	Principle of Least Privilege enforcement
•	Comprehensive audit logging
•	Detection of unauthorized activities
________________________________________
✅ Results
The architecture successfully prevented unauthorized access attempts to both storage and compute resources.
All malicious actions performed by the unprivileged user were:
•	Blocked by IAM policies
•	Logged by CloudTrail
•	Traceable for forensic analysis
________________________________________
🏆 Key Learnings
•	Importance of network isolation in cloud security
•	Effective use of IAM for access control
•	Role of audit logs in incident response
•	Defense-in-depth architecture principles
•	Real-world simulation of unauthorized access scenarios
________________________________________
🔮 Possible Enhancements
Future improvements could include:
•	NAT Gateway for controlled private subnet internet access
•	AWS GuardDuty for advanced threat intelligence
•	AWS WAF for web application protection
•	Security Groups and Network ACL hardening
•	Integration with SIEM tools for centralized monitoring
________________________________________
📌 Conclusion
This project demonstrates how a secure multi-tier architecture can be implemented in AWS using core security services. By combining network isolation, strict IAM policies, encrypted storage, and activity monitoring, the system effectively prevents and detects unauthorized access attempts.
Such architectures form the foundation of enterprise-grade cloud security deployments.
________________________________________
👨‍💻 Author
Aman Lodha
Cloud Security Project — AWS Multi-Tier Architecture

