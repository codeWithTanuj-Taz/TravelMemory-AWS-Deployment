# 🚀 EC2 Infrastructure Setup

## Overview

This section describes the AWS infrastructure created to host the Travel Memory application.

The deployment uses multiple EC2 instances to separate the frontend and backend services, providing better scalability and maintainability.

---

## AWS Infrastructure

The following AWS resources were created:

- Virtual Private Cloud (VPC)
- Security Groups
- Four EC2 Instances
  - Frontend EC2 - 1
  - Frontend EC2 - 2
  - Backend EC2 - 1
  - Backend EC2 - 2
- Key Pair

---

## Step 1 – Create a VPC

A dedicated Virtual Private Cloud (VPC) was created to isolate the application resources.

### Configuration

| Property | Value |
|----------|-------|
| IPv4 CIDR | 10.0.0.0/16 |
| Tenancy | Default |

### Screenshot

Created dedicated VPC TravelMemory01 for the project

> <img width="394" height="421" alt="image" src="https://github.com/user-attachments/assets/48f5d947-cce8-43dd-a565-e6b52cd4fe7a" />
Select atleast 2 Availiblity zones
> <img width="285" height="250" alt="image" src="https://github.com/user-attachments/assets/c565c945-d7b0-40d8-8063-aff1b0258c1e" />
VPC dashboard should show the created VPC
> <img width="778" height="179" alt="image" src="https://github.com/user-attachments/assets/91176d76-40e8-426b-b92c-f4487d45acad" />

---

## Step 2 – Create Security Groups

Security Groups were configured to control inbound and outbound network traffic.
Add port 22 -SSH and HTTP port 80 in Inbound rule 
<img width="772" height="178" alt="image" src="https://github.com/user-attachments/assets/82daf730-343c-4e19-88fe-0d7e0bbdbc86" />
<img width="775" height="254" alt="image" src="https://github.com/user-attachments/assets/eab4378e-d8ce-4612-a70c-bac954e84dd8" />
Also configure atleast one outbound rule
<img width="767" height="133" alt="image" src="https://github.com/user-attachments/assets/1195c7b3-13fd-4fda-a34d-5a9ab673ffda" />

---

## Step 3 – Launch EC2 Instances

Four Ubuntu EC2 instances were launched.

| Instance | Purpose |
|----------|----------|
| Frontend EC2 - 1 | React + Nginx |
| Frontend EC2 - 2 | React + Nginx |
| Backend EC2 - 1 | Node.js + PM2 |
| Backend EC2 - 2 | Node.js + PM2 |

### EC2 Configuration

| Property | Value |
|----------|-------|
| AMI | Ubuntu Server 24.04 LTS |
| Instance Type | t2.micro |
| Storage | 8 GB gp3 |
| Authentication | AWS Key Pair |
| VPC | TravelMemory01|
|Subnet |Travelmemory01-subnet-public1-us-east-1a|(for 2 Ec2 Instances) |
|Subnet |Travelmemory01-subnet-public2-us-east-1a|(for rest 2 Ec2 Instances) |
|Security group|Select the same SG created for the VPC -TravelMemory01 |
|Auto-assign public IP|Enable|


### Screenshot

> <img width="943" height="406" alt="Screenshot 2026-07-12 155357" src="https://github.com/user-attachments/assets/5d03ecc1-c592-417b-abe7-624b4cb517b7" />
<img width="927" height="353" alt="image" src="https://github.com/user-attachments/assets/6194ac0d-3428-4390-af4a-60489e293425" />
<img width="932" height="361" alt="image" src="https://github.com/user-attachments/assets/e7747d97-f40b-4954-8907-bee1c7c5c9e1" />
<img width="912" height="395" alt="image" src="https://github.com/user-attachments/assets/4227d554-89bb-43e2-afa4-ff816f18cd72" />

---

## Step 4 – Verify Running Instances

After launching the instances, verify that all EC2 instances are in the **Running** state.

<img width="755" height="157" alt="Screenshot 2026-07-08 125845" src="https://github.com/user-attachments/assets/eddad886-f063-428a-bc61-67f6a253ae79" />


### Screenshot


## Summary

The AWS infrastructure is now ready for application deployment.

The next step is to configure and deploy the backend application.
