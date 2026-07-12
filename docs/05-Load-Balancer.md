# ⚖️ Application Load Balancer Setup

## Overview

This section describes the configuration of the AWS Application Load Balancer (ALB) used to distribute incoming traffic across multiple frontend EC2 instances.

The ALB improves application availability by routing requests to healthy frontend instances.

---

## Architecture
The ALB receives requests from Cloudflare and distributes them across two frontend EC2 instances.

## Step 1 – Create a Target Group

Create a target group for the frontend EC2 instances.

### Configuration

| Property | Value |
|----------|-------|
| Target Type | Instances |
| Protocol | HTTP |
| Port | 80 |
| Health Check Path | / |
|ALB| Attach to load balancer

### Screenshot
<img width="797" height="342" alt="image" src="https://github.com/user-attachments/assets/531557c6-b23e-4d69-88df-640fea7ee6e5" />
---

## Step 2 – Register Targets

Register the frontend EC2 instances with the target group.

| Instance | Port |
|----------|------|
| tm-frontend EC2-1 | 80 |
| tm-frontend EC2-2 | 80 |
| Status| Healthy|


### Screenshot

Select as pending below 

<img width="783" height="428" alt="Screenshot 2026-07-08 152034" src="https://github.com/user-attachments/assets/342772da-abdc-4484-a60f-83e5d930400f" />

## Step 3 – Create the Application Load Balancer

Configure the ALB.

### Configuration

| Property | Value |
|----------|-------|
| Type | Internet-facing |
| Scheme | Internet-facing |
| Listener | HTTP :80 |
| VPC | Your VPC |
| Availability Zones | Multiple |

### Screenshot
<img width="803" height="378" alt="image" src="https://github.com/user-attachments/assets/c9ea5f98-48d1-4249-9bd0-1a19c499e464" />
<img width="935" height="411" alt="image" src="https://github.com/user-attachments/assets/c9a0ced5-48ee-4d54-a63c-259d4beb2b82" />**
<img width="845" height="398" alt="image" src="https://github.com/user-attachments/assets/4d5d86aa-5161-4a1b-98cf-4b53cc5ea0ee" />
<img width="808" height="419" alt="image" src="https://github.com/user-attachments/assets/86425042-0c59-46ba-acfe-e63b72bf7dfd" />

---

## Step 4 – Configure the Listener

Create an HTTP listener on port 80 and forward traffic to the frontend target group.

### Screenshot

<img width="780" height="164" alt="image" src="https://github.com/user-attachments/assets/156bac88-ceee-40fb-806a-db6f485a3c4d" />

---

## Step 5 – Verify Target Health

Verify that all registered frontend instances are healthy.

### Screenshot

<img width="783" height="428" alt="Screenshot 2026-07-08 152034" src="https://github.com/user-attachments/assets/10df870d-707a-48ad-aa16-7758a76b9c2c" />

---

## Step 6 – Verify the Application

Access the application using the ALB DNS name.

Example:

```
http://tm-alb-xxxxxxxx.us-east-1.elb.amazonaws.com
```

### Screenshot

<img width="548" height="449" alt="Screenshot 2026-07-08 191447" src="https://github.com/user-attachments/assets/2601b2b6-9b0e-4b02-92a8-ebbbeaf35723" />

---

## Summary

The AWS Application Load Balancer has been successfully configured to distribute incoming HTTP traffic across multiple frontend EC2 instances.
