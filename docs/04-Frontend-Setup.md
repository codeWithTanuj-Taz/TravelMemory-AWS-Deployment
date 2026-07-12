# 🌐 Frontend Setup

## Overview

This section describes the deployment and configuration of the React frontend application on an AWS EC2 instance.

The frontend application is served using **Nginx** after creating an optimized production build.

## Prerequisites

Before deploying the frontend application, ensure the following software is installed on the Frontend EC2 instance:

- Node.js
- npm
- Git
- Nginx

> **Note:** The detailed installation procedure for Node.js and Git is covered in **03-Backend-Setup.md**.
> The same installation steps apply to the frontend EC2 instance.

## Step 1 – Connect to the Frontend EC2 Instance

Connect to the backend EC2 instance using an SSH client such as **MobaXterm**.
...


## Step 2 – Clone the Repository

```bash
git clone https://github.com/codeWithTanuj-Taz/TravelMemory-AWS-Deployment.git
cd ~/TravelMemory/frontend
```

### Screenshot
<img width="725" height="52" alt="image" src="https://github.com/user-attachments/assets/9a6ea004-75c5-41f9-89e5-8acf92c08b2a" />

## Step 3 – Install Frontend Dependencies

```bash
npm install
```
### Screenshot

<img width="713" height="136" alt="image" src="https://github.com/user-attachments/assets/9ad73af4-d75d-4679-98c7-b09d24b41505" />


## Step 4 – Configure the Environment File & url.js file 
```bash
 nano .env
# REACT_APP_BACKEND_URL=http://<Ec2-backend-public-ip>:3000
 nano src/url.js
# export const baseUrl = process. env. REACT_APP_BACKEND_URL | | "http://<Ec2-backend-public-ip>:3000";
```
### Screenshot

<img width="559" height="29" alt="image" src="https://github.com/user-attachments/assets/2b582568-02ea-4240-b69c-b11f237cdbf2" />
<img width="775" height="197" alt="Screenshot 2026-07-12 202139" src="https://github.com/user-attachments/assets/dc288a3b-de6a-486b-a7bb-8c3893dc0013" />
<img width="605" height="55" alt="image" src="https://github.com/user-attachments/assets/03a291d6-18ec-4038-b8b3-826a002dbfb4" />
<img width="749" height="157" alt="image" src="https://github.com/user-attachments/assets/4cb04eb5-afe3-4aaa-b6e1-c03769ebc579" />


## Step 5 – Build the React Application

```bash
npm run build
```
### Screenshot
<img width="502" height="347" alt="image" src="https://github.com/user-attachments/assets/88d92f62-4c5b-4c27-a39f-cf32d47eb025" />

---
## Step 6 – Copy file to Nginix & Configure Nginx
```bash
sudo rm -rf /var/www/html/*
sudo cp -r build/* /var/www/html/
# open file
sudo nano /etc/nginx/sites-available/default
# Replace the content 
```
### Screenshot
<img width="568" height="77" alt="Screenshot 2026-07-12 203322" src="https://github.com/user-attachments/assets/3f811ccd-56cb-430e-a4d0-406a8ce92e56" />
<img width="578" height="34" alt="image" src="https://github.com/user-attachments/assets/116be678-6b83-4773-b983-a2c384a3f50c" />
<img width="592" height="256" alt="Screenshot 2026-07-12 203800" src="https://github.com/user-attachments/assets/613c64d2-6db3-4794-9605-3bd31a3d5e79" />

...

## Step 7 – Test and Restart Ngnix

```bash
sudo nginx -t
# Expected output
# syntax is ok test is successful
sudo systemctl restart nginx
```
### Screenshot
<img width="667" height="74" alt="Screenshot 2026-07-12 204618" src="https://github.com/user-attachments/assets/eefddc45-9eef-4c46-8671-5b4367120e86" />


## Step 8 – Verify the Deployment
```bash
curl http://localhost
# It should return the value shown in Screenshot below
```
### Screenshot
<img width="758" height="112" alt="Screenshot 2026-07-12 204809" src="https://github.com/user-attachments/assets/6a3b126a-3565-41cc-8c57-55200c69a93c" />

## Test from your browser
```bash
Open in browser. Your  TravelMemory application should launch 
http://<Frontend-EC2-1-Public-IP>
```
### Screenshot
<img width="437" height="416" alt="Screenshot 2026-07-08 140531" src="https://github.com/user-attachments/assets/d7f655e0-63f4-4a76-90b5-dd7d77937fd3" />

## Summary

The React frontend has been successfully deployed on AWS EC2 and is served using Nginx. 
The next step is to configure the AWS Application Load Balancer and route traffic to the frontend instances.
Repeat the same step to setup 2nd frontend ec2 Instance
