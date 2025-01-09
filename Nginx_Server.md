# Nginx Server Installation and Configuration on Ubuntu 24.04

## Overview
Nginx is a high-performance web server and reverse proxy server known for its scalability, efficient resource usage, and ability to handle high traffic loads. It supports features like load balancing, caching, and SSL/TLS.

---

## Features of Nginx
- **HTTP Server**: Serves static files and supports HTTP/HTTPS.
- **Reverse Proxy**: Handles backend server requests.
- **Load Balancing**: Distributes traffic across servers.
- **Caching**: Speeds up content delivery.
- **SSL/TLS Support**: Ensures secure communication.
- **Highly Configurable**: Offers custom routing rules.

---

## Installation Steps

### 1. Update Package List
```bash
sudo apt update
sudo apt upgrade -y
```
### 2. Install Nginx
```bash
sudo apt install nginx -y
```
### 3. Verify Nginx Service
```bash
sudo systemctl status nginx
```
### 4. Configure Firewall
```bash
sudo ufw allow 'Nginx Full'
sudo ufw enable
sudo ufw status
```


