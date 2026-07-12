# ⚙️ Backend Setup

## Overview

This section describes the deployment and configuration of the backend application on AWS EC2.

The backend application is built using **Node.js** and **Express.js** and is managed using **PM2** to ensure high availability and automatic process recovery.

---

## Step 1 – Connect to the Backend EC2 Instance

Connect to the backend EC2 instance using an SSH client such as **MobaXterm**.

### Procedure

1. Open **MobaXterm**.
2. Click **Session** → **SSH**.
3. Enter the **Public IPv4 Address** of the backend EC2 instance.
4. Select the key pair already downloaded
5. Select **Specify username** and enter:

```text
ubuntu
```
### Screenshot

> <img width="688" height="428" alt="image" src="https://github.com/user-attachments/assets/843c97f5-40a3-41d9-9984-512500107574" />
<img width="515" height="237" alt="image" src="https://github.com/user-attachments/assets/50967215-0b1d-47ca-a6f9-d1a6d7f9b12f" />
Login as Username ubuntu
> <img width="470" height="431" alt="image" src="https://github.com/user-attachments/assets/6dbb704e-727c-494b-983e-ffba66b35f8d" />
UPdate the
---
## Step 2 – Update the Package Repository

Update the Ubuntu package repository to ensure the latest package information is available.

```bash
sudo apt update
sudo apt upgrade -y
```

### Screenshot

<img width="592" height="35" alt="Screenshot 2026-07-08 125813" src="https://github.com/user-attachments/assets/6d344698-b1f7-4be3-bb4e-d1a37b683d71" />
<img width="389" height="42" alt="Screenshot 2026-07-08 125719" src="https://github.com/user-attachments/assets/3e355c09-df1e-4e6a-8ef5-009273fc517a" />

## Step 3 – Install Dependencies

```bash
curl -fsSL https://deb.nodesource.com/setup_18.x
sudo -E bash
sudo apt install -y nodejs git nginx
sudo npm install -g pm2
```
### Screenshot
<img width="643" height="83" alt="Screenshot 2026-07-08 132806" src="https://github.com/user-attachments/assets/fe00caca-3188-4145-8fd0-a79bc376eb44" />


## Step 4 – Clone the Repository

Clone the GitHub repository to the EC2 instance.

```bash
git clone https://github.com/UnpredictablePrashant/TravelMemory.git
```

### Screenshot

> <img width="625" height="40" alt="image" src="https://github.com/user-attachments/assets/95b31091-87c6-44c0-acb4-0de82766ec14" />

---

## Step 5 – Configure Environment Variables

Create the `.env` file in backend folder and configure the required environment variables.

```bash
 cd TravelMemory/backend 
 nano .env
```

Example:

| Variable | Description |
|----------|-------------|
| PORT | Backend server port |
| MONGO_URI | MongoDB Atlas connection string |

> **Note:** Never commit actual credentials to GitHub.

### Screenshot

> <img width="821" height="56" alt="Screenshot 2026-07-12 170100" src="https://github.com/user-attachments/assets/98f668d7-c16c-4590-b144-2a7234a86e33" />

---

## Step 6 – Install Backend Dependencies

Navigate to the **backend** directory of the cloned repository on the backend EC2 instance.

```bash
cd ~/TravelMemory/backend
```

Install all required Node.js dependencies.

```bash
sudo apt install nodejs
sudo apt intall npm
node -v
npm -v
After verifying
npm install
```

After the installation completes successfully, the backend application is ready to be configured.

### Screenshot

<img width="646" height="31" alt="Screenshot 2026-07-12 173544" src="https://github.com/user-attachments/assets/4de6dbec-d2f4-422c-bd57-45901cfb0a15" />
<img width="518" height="36" alt="Screenshot 2026-07-12 173659" src="https://github.com/user-attachments/assets/f702d650-8573-4642-b471-7aeeab277b3d" />
<img width="477" height="53" alt="Screenshot 2026-07-12 173729" src="https://github.com/user-attachments/assets/daafdfda-bb86-4ff2-beb2-73b51344637c" />


---

## Step 7 – Start the Backend Application

Start the backend application using PM2.

```bash
pm2 start index.js --name travelmemory-backend
```

Verify that the application is running.

```bash
pm2 status
# It will show online
```

### Screenshot
<img width="526" height="324" alt="image" src="https://github.com/user-attachments/assets/5761a342-92b7-4942-bc49-103e2f037104" />
<img width="656" height="135" alt="image" src="https://github.com/user-attachments/assets/05bccbc9-1f20-4669-abc2-b279598c9e8b" />
<img width="530" height="115" alt="image" src="https://github.com/user-attachments/assets/65f1efe5-430a-4b6c-8b02-fa272a7ca125" />

---

## Step 9 – Configure PM2 Startup

Configure PM2 to automatically restart the backend application whenever the EC2 instance reboots.

Generate the startup command.

```bash
pm2 startup
```
Execute the generated command.

```bash
sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu
```

Save the current PM2 process list.

```bash
pm2 save
```

### Screenshot

<img width="824" height="131" alt="image" src="https://github.com/user-attachments/assets/1d4a2b5a-29c0-4437-a115-99aa020bf232" />
<img width="542" height="148" alt="image" src="https://github.com/user-attachments/assets/14a98018-25c7-42bf-a0b2-151d8b174f34" />


## Step 9 – Configure Nginx

Edit the default site configuration.

```bash
sudo nano /etc/nginx/sites-available/default
Replace the content with

server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;

        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
sudo nginx -t Should show successfull
sudo systemctl restart nginx
```
### Screenshot
<img width="674" height="26" alt="image" src="https://github.com/user-attachments/assets/4b02c9e1-fade-471d-9991-6eb17c517379" />
<img width="608" height="319" alt="Screenshot 2026-07-12 182732" src="https://github.com/user-attachments/assets/cefe138e-7f25-4f5c-9fcd-a6aa4bd08524" />
<img width="601" height="41" alt="image" src="https://github.com/user-attachments/assets/872f14b5-6c7a-4012-ab07-5a1105a6b556" />
<img width="508" height="43" alt="image" src="https://github.com/user-attachments/assets/ffe143b0-151c-489a-9b27-86356964c5e8" />

---

## Step 7 – Verify the Backend

Verify that the backend service is running successfully.

Checks performed:

- PM2 process status
- Check on the browser the http://<Ec2-instance -public ip>

### Screenshot

> <img width="815" height="146" alt="image" src="https://github.com/user-attachments/assets/4f950ce0-6af1-4e9d-baec-99027829546a" />
<img width="869" height="143" alt="image" src="https://github.com/user-attachments/assets/853a3597-047d-4376-a56f-3cbc4d9e2ef0" />


---

## Summary

The backend application is now successfully deployed and managed by PM2.

The next step is to deploy the React frontend using Nginx.
