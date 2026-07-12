# 🏗️ Solution Architecture

## Overview

The Travel Memory application is deployed on AWS using a multi-instance architecture that improves availability, scalability, and maintainability.

The deployment architecture includes:

- Two Frontend EC2 instances running Nginx and the React production build
- Two Backend EC2 instances running the Node.js and Express.js application with PM2
- An AWS Application Load Balancer (ALB) for traffic distribution
- MongoDB Atlas as the managed cloud database
- Cloudflare for DNS management and custom domain routing

---

## Architecture Diagram
The following diagram illustrates the deployment architecture and the communication flow between AWS components.

<img width="1536" height="1024" alt="AWS architecture daigram" src="https://github.com/user-attachments/assets/cd4383d7-977a-432b-84c1-864f97268ebd" />


---

## Request Flow Daigram

```text

   Internet
      │
      ▼
Cloudflare DNS
      │
      ▼
Application Load Balancer
      │
 ┌────┴────┐
 ▼         ▼
Frontend-1 Frontend-2
    │          │
    ▼          ▼
Backend-1  Backend-2
     │          │
     └────┬─────┘
          ▼
    MongoDB Atlas

```

---

## Components

### Cloudflare (DNS)

- DNS Management
- Custom Domain
- HTTP traffic routing

### Application Load Balancer

- Receives client requests
- Distributes traffic across frontend servers
- Performs health checks

### Frontend EC2 Instances

- Ubuntu Server
- Nginx
- React Production Build

### Backend EC2 Instances

- Ubuntu Server
- Node.js
- Express.js
- PM2

### MongoDB Atlas

- Managed cloud database
- Stores application data

---

## Request Flow

1. User accesses **wheelseyes.in**
2. Cloudflare resolves the domain.
3. The request reaches the AWS Application Load Balancer.
4. The ALB forwards traffic to one of the frontend EC2 instances.
5. The frontend communicates with its corresponding backend EC2 instance.
6. The backend processes the request and interacts with MongoDB Atlas.
7. The response is returned to the user.
