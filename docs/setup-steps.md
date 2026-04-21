# 🚀 Secure AWS VPC Network Lab – Setup Guide

## 🧭 Project Overview

This project demonstrates how to design and implement a secure multi-tier network architecture in AWS.

The architecture simulates a real-world environment:

- 🏢 Public Layer → Web Server (Internet-facing)
- 🔒 Private Layer → Database Server (Restricted access)
- 🚪 Security Controls → Security Groups & Network ACLs

---

## 🪜 Step 1: Create VPC (Virtual Private Cloud)

### What is a VPC?
A VPC is a logically isolated network in AWS where you can launch resources securely.

### Configuration:
- Name: `secure-vpc-lab`
- CIDR Block: `10.0.0.0/16`

### Outcome:
A private network space to host cloud resources.

---

## 🪜 Step 2: Create Subnets

Subnets divide the VPC into smaller network segments.

### Public Subnet:
- Name: `public-subnet`
- CIDR: `10.0.1.0/24`
- Purpose: Host internet-facing resources

### Private Subnet:
- Name: `private-subnet`
- CIDR: `10.0.2.0/24`
- Purpose: Host internal resources (e.g., database)

---

## 🪜 Step 3: Configure Internet Gateway

### Purpose:
Enables communication between the VPC and the internet.

### Steps:
- Create Internet Gateway: `igw-secure-lab`
- Attach to VPC: `secure-vpc-lab`

---

## 🪜 Step 4: Configure Route Tables

### Public Route Table:
- Name: `public-rt`
- Route:
  - `0.0.0.0/0 → Internet Gateway`
- Associated with: `public-subnet`

### Private Route Table:
- Name: `private-rt`
- No internet route configured (isolated subnet)

---

## 🪜 Step 5: Launch Web Server (Public EC2)

### Configuration:
- Instance Name: `web-server`
- AMI: Amazon Linux
- Subnet: `public-subnet`
- Public IP: Enabled

### Security Group Rules:
| Type | Port | Source |
|------|------|--------|
| SSH  | 22   | Your IP |
| HTTP | 80   | 0.0.0.0/0 |

### Purpose:
Allows external users to access the web application.

---

## 🪜 Step 6: Launch Database Server (Private EC2)

### Configuration:
- Instance Name: `db-server`
- Subnet: `private-subnet`
- Public IP: Disabled

### Security Group Rules:
| Type  | Port | Source |
|-------|------|--------|
| MySQL | 3306 | Web Server Security Group |

### Purpose:
Restricts database access to only the web server.

---

## 🪜 Step 7: Validation Tests

### Test 1:
- Access web server via public IP → ✅ Expected: Success

### Test 2:
- Attempt direct access to database → ❌ Expected: Denied

---

## 🧪 Step 8: Troubleshooting Lab (Break & Fix)

### Scenario 1: HTTP Access Failure
- Issue: Removed HTTP (port 80) from security group
- Impact: Website inaccessible
- Fix: Re-add HTTP rule

---

### Scenario 2: No Internet Access
- Issue: Removed route to Internet Gateway
- Impact: No external connectivity
- Fix: Restore route `0.0.0.0/0 → IGW`

---

### Scenario 3: Database Connectivity Failure
- Issue: Misconfigured database security group
- Impact: Web server cannot connect to DB
- Fix: Allow MySQL access only from web server SG

---

## 🧠 Key Learnings

- VPC network segmentation (public vs private)
- Firewall configuration using Security Groups
- Importance of routing in connectivity
- Troubleshooting cloud network issues
- Applying least-privilege security principles
