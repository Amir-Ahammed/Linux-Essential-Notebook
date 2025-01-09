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

## Installing Nginx on Ubuntu 24.04

1. **Update Package List** - Run the following command to ensure your package list is up to date:
   ```bash
   sudo apt update
   sudo apt upgrade -y
2. **Install Nginx** - Use the following command to install Nginx:
   ```bash
   sudo apt install nginx -y
   ```
   This will install Nginx and start the service automatically.

3. **Verify Nginx Service** - Verify that the Nginx service is running:
   ```bash
   sudo systemctl status nginx
4. **Configure Firewall** - If a firewall is enabled, allow traffic for Nginx:
   ```bash
   sudo ufw allow 'Nginx Full'
   sudo ufw enable
   sudo ufw status

---

## Basic Configuration of Nginx

1. **Default Configuration File** - 
   The default configuration file for Nginx is located at:
   ```bash
   /etc/nginx/nginx.conf

2. **Configure Server Blocks (Virtual Hosts)** - 
   Nginx uses server blocks to host multiple websites on a single server.
   * Create a new server block configuration file:
     ```bash
     sudo vim /etc/nginx/sites-available/example.com
   * Add the following configuration:
     ```nginx
     server {
         listen 80;
         server_name example.com www.example.com;

         root /var/www/example.com;
         index index.html index.htm;

         location / {
             try_files $uri $uri/ =404;
     
         }
     }
    * Create the root directory for your website:
      ```bash
      sudo mkdir -p /var/www/example.com
      sudo chown -R $USER:$USER /var/www/example.com
    * Enable the configuration by creating a symbolic link:
      ```bash
      sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
    * Test the Nginx configuration:
      ```bash
      sudo nginx -t
    * Reload Nginx:
      ```bash
      sudo systemctl reload nginx

3. **Enable HTTPS with SSL/TLS** - 
Install a free SSL certificate using Let's Encrypt:

   * Install Certbot and the Nginx plugin:
     ```bash
     sudo apt install certbot python3-certbot-nginx -y
   * Obtain and install the certificate:
     ```bash
     sudo certbot --nginx -d example.com -d www.example.com
   * Verify the SSL setup:
     ```bash
     sudo certbot renew --dry-run
---
## Advanced Configuration

* **Load Balancing:** Configure Nginx to distribute traffic among backend servers:
  ```nginx
  upstream backend {
      server backend1.example.com;
      server backend2.example.com;
  }
  
  server {
      
      listen 80;
      location / {
          proxy_pass http://backend;
      }
  }
* **Caching:** Enable caching for static files to improve performance:
  ```ngnix
  location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
      expires 30d;
      access_log off;
  }

---

