# Nginx Reverse Proxy Configuration

## What is a Reverse Proxy?
A reverse proxy is a server that sits between client devices and backend servers. It handles client requests by forwarding them to appropriate backend servers and then sending the server's response back to the client.

### Benefits of Using a Reverse Proxy:
- **Load Balancing**: Distributes traffic across multiple servers to ensure availability and performance.
- **SSL Termination**: Offloads SSL encryption and decryption tasks from backend servers.
- **Caching**: Stores responses to reduce load on backend servers and improve response times.
- **Security**: Hides backend server details and filters malicious traffic.

---

## Installation of Nginx
1. **Install Nginx on Ubuntu**:
   ```bash
   sudo apt update
   sudo apt install nginx
2. **Enable and Start Nginx**:
   ```bash
   sudo systemctl enable nginx
   sudo systemctl start nginx
3. **Check Status**:
   ```bash
   sudo systemctl status nginx
   ```

## Basic Reverse Proxy Configuration
#### File Location:
Nginx configuration files are typically located in` /etc/nginx/`

* **Open Nginx Configuration**: Edit the main configuration file or create a new one in` /etc/nginx/sites-available/`
  ```
  sudo vim /etc/nginx/sites-available/reverse-proxy
  ```
  



