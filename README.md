# IAM-Project-1 Cloud Security Fundamentals Project
I practiced a scenario where  I was tasked with auditing and improving the AWS security posture for a fictional startup (StartupCo) that had launched a fitness tracking application under tight deadlines.

Their initial setup prioritized speed over security — a common pattern in early-stage startups — which led to serious security gaps that needed to be addressed.

## 🧠 Problem Overview

When I began, the environment was structured as follows:

- All 10 team members used the **root account** (shared credentials via chat)
- **No MFA** or password policies enforced
- **No role separation or IAM users**
- AWS services deployed: EC2, S3, RDS, CloudWatch for both dev and prod

This shows immediate risks including accidental deletion, compromised credentials, lack of auditability, and no least-privilege enforcement.

## 🔧 My Solution Strategy

I focused on **foundational cloud security** best practices, balancing AWS Free Tier limits and real-world IAM design principles.

### Key goals:
- Eliminate root usage for daily operations
- Define IAM roles using groups and scoped policies
- Apply least privilege access
- Introduce MFA and a strong password policy
- Document everything clearly for future audits or handoffs
## 🏗️ Architecture Diagram

[Architecture] architecture-diagram

This reflects the same EC2-S3-RDS-CloudWatch environment, but now with identity separation and secure boundaries between roles.

## 👥 IAM Users & Groups

I created four IAM groups based on functional responsibilities:

| Group        | Purpose                                      | Users |
|--------------|----------------------------------------------|-------|
| Developers   | EC2 + S3 access, CloudWatch read-only        | 4     |
| Operations   | Full EC2, RDS, Systems Manager, monitoring   | 2     |
| Finance      | Billing, Budgets, Cost Explorer              | 1     |
| Analysts     | Read-only S3 and RDS access                  | 3     |

Each group has a custom IAM policy using JSON besides the Operations, All users were assigned to their group and instructed to use IAM login links instead of root.

## 🔐 Security Enhancements

### ✅ MFA
Enabled for the admin account and demonstrated setup on one user. In a real org, I’d enforce MFA on all accounts with conditional policies or AWS SSO.

### ✅ Password Policy
Set minimum requirements:
- At least 12 characters
- Require uppercase, lowercase, number, symbol
- Password rotation every 90 days
- it wasn't selected the time of screenshot but also to prevent password reuse

### ✅ Least Privilege
Each policy was manually crafted to only allow the **exact actions** needed for each group. Wildcards were avoided unless scoped to known resources.

## 📌 Lessons Learned

- IAM should always be the **first** thing configured in a production-ready AWS account.
- MFA and scoped access are low-effort wins that provide major security posture improvements.
- Even mock environments benefit from well-documented role access and lifecycle policies.
- Teaching least privilege through practical IAM exercises is the best way to learn how AWS enforces access at every layer.

This project was built using only the AWS Free Tier and IAM console access (no root login). The goal was to simulate what a real remediation project would look like at an early-stage startup with minimal cloud governance in place.