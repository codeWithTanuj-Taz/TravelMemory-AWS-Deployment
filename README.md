# 🌍 Travel Memory - AWS Deployment

## 📌 Project Overview 

A full-stack MERN (MongoDB, Express.js, React, Node.js) web application for managing travel experiences.

This repository demonstrates the deployment of the application on AWS using industry-standard cloud practices, including:

- Application deployment
- Amazon EC2
- Virtual Private Cloud 
- Security group
- Target group
- Load balancing using AWS Application Load Balancer (ALB)
- Reverse proxy configuration with Nginx
- Process management using PM2
- Cloud database integration with MongoDB Atlas
- Custom domain configuration using Cloudflare

---

## ✨ Application Features

- Add travel memories
- View travel experiences
- RESTful API using Express.js
- MongoDB Atlas integration
- Responsive React frontend

## ☁️ Deployment Features

- AWS EC2 deployment
- AWS Application Load Balancer
- Nginx reverse proxy
- PM2 process management
- Cloudflare DNS
- Custom domain integration
---

## 🛠 Tech Stack

| Layer | Technology |
|--------|------------|
| Frontend | React |
| Backend | Node.js, Express.js |
| Database | MongoDB Atlas |
| Web Server | Nginx |
| Process Manager | PM2 |
| Cloud | AWS EC2 |
| Load Balancer | AWS Application Load Balancer |
| DNS | Cloudflare |
| Domain Registrar | GoDaddy |

---

## 📂 Project Structure

```
TravelMemory-AWS-Deployment/
│
├── frontend/                 # React application
├── backend/                  # Node.js + Express API
├── README.md
├── LICENSE
└── .gitignore
```

---

## ☁️ AWS Deployment Architecture

```
                         🌐 Internet
                                │
                                ▼
                    ☁️ Cloudflare (DNS/CDN)
                                │
                                ▼
          ⚖️ AWS Application Load Balancer (HTTP :80)
                                │
               ┌────────────────┴────────────────┐
               │                                 │
               ▼                                 ▼
      🖥️ Frontend EC2 - 1                🖥️ Frontend EC2 - 2
            Ubuntu                             Ubuntu
             Nginx                              Nginx
          React Build                       React Build
               │                                 │
               │ API Calls                       │ API Calls
               ▼                                 ▼
      ⚙️ Backend EC2 - 1                 ⚙️ Backend EC2 - 2
            Ubuntu                             Ubuntu
         Node.js + PM2                     Node.js + PM2
               │                                 │
               └───────────────┬─────────────────┘
                               │
                               ▼
                    🍃 MongoDB Atlas (Cloud)
```
---

## 📖 Deployment Guide

A detailed deployment guide with screenshots is available in the **docs/** directory.

| Guide | Description |
|--------|-------------|
| 01-Architecture | AWS architecture overview |
| 02-EC2-Setup | EC2 instance creation and configuration |
| 03-Backend-Setup | Deploying the backend |
| 04-Frontend-Setup | Deploying the frontend |
| 05-Nginx-Configuration | Configuring Nginx |
| 06-PM2-Configuration | Running backend with PM2 |
| 07-Load-Balancer | ALB setup and target groups |
| 08-Cloudflare-Domain | Domain and DNS configuration |
| 09-Troubleshooting | Common deployment issues and fixes |
