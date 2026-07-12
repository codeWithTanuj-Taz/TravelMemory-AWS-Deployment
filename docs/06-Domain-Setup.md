# 🌐 Domain Setup

## Overview

This section describes the configuration of the custom domain **wheelseyes.in** using GoDaddy and Cloudflare.

The domain is managed through Cloudflare, which provides DNS management, while traffic is routed to the AWS Application Load Balancer.

---

## Step 1 – Purchase the Domain

The custom domain **wheelseyes.in** was registered 

### Screenshot

<img width="951" height="470" alt="Screenshot 2026-07-12 215011" src="https://github.com/user-attachments/assets/55aac147-85d4-4728-9f8c-26ec18f2a722" />

---

## Step 2 – Add the Domain to Cloudflare

Add the domain to Cloudflare 

### Screenshot
<img width="872" height="313" alt="image" src="https://github.com/user-attachments/assets/cba06b66-cf87-49e3-b32a-77230dfead42" />
<img width="917" height="513" alt="image" src="https://github.com/user-attachments/assets/edfc12f7-f68d-44a1-bf11-7ff6907e57cb" />

---

## Step 3 – Update GoDaddy Nameservers

Replace the default GoDaddy nameservers with the Cloudflare nameservers provided during onboarding.
The cloudflare will manage DNS after adding Servername
### Screenshot

<img width="666" height="442" alt="image" src="https://github.com/user-attachments/assets/7b02298b-4aee-4a61-bd62-2d8e116d9796" />
Server name updated 
<img width="655" height="244" alt="image" src="https://github.com/user-attachments/assets/e3f6b0b8-14c9-4370-940c-f6cfcb0a6855" />

---

## Step 4 – Configure DNS Records

Create the required DNS records in Cloudflare.

| Type | Name | Value |
|------|------|-------|
| CNAME | @ | ALB DNS Name |
| CNAME | www | ALB DNS Name |

### Screenshot
Added ALB DNS NAme 
<img width="872" height="481" alt="image" src="https://github.com/user-attachments/assets/d74bc00a-a859-481f-8260-8da55732ed5a" />
<img width="757" height="344" alt="image" src="https://github.com/user-attachments/assets/a551b623-d688-4669-a983-3000f701293d" />

---

## Step 5 – Verify Domain Resolution

Verify that the domain resolves to the AWS Application Load Balancer.

Example:

```bash
nslookup wheelseyes.in
```

```bash
curl -I http://wheelseyes.in
```

## Step 6 – Verify the Website

Open the application using:

- http://wheelseyes.in
- http://www.wheelseyes.in

### Screenshot

<img width="665" height="533" alt="image" src="https://github.com/user-attachments/assets/1ffdb6f4-f7d8-484d-8ea7-e4b3546447fd" />
(Insert browser screenshot.)*

---

## Summary

The custom domain has been successfully configured using GoDaddy and Cloudflare. User requests are routed through Cloudflare to the AWS Application Load Balancer, which distributes traffic to the frontend EC2 instances.

---
