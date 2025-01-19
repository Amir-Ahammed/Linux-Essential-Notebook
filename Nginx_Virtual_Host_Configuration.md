
```nginx
server {
    listen 80;
    listen [::]:80; # Listen on IPv6 as well
    server_name example.com [www.example.com](https://www.example.com);

    # Redirect all HTTP requests to HTTPS
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl default_server;
    server_name example.com www.example.com;

    # Optimized SSL Settings
    ssl_protocols TLSv1.2 TLSv1.3;  # Enable secure protocols
    ssl_prefer_server_ciphers on;     # Use server's preferred ciphers
    ssl_ciphers 'EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH';  # Strong cipher suite
    ssl_ecdh_curve secp384r1;        # Elliptic curve for perfect forward secrecy
    ssl_session_cache shared:SSL:10m;  # Cache SSL sessions for 10 minutes
    ssl_session_timeout 10m;          # Timeout idle SSL sessions after 10 minutes
    ssl_stapling on;                  # Enable OCSP stapling for faster SSL handshakes
    ssl_stapling_verify on;            # Verify OCSP staple

    # Add your SSL certificate and key here (replace with your paths)
    ssl_certificate /path/to/your/certificate.crt;
    ssl_certificate_key /path/to/your/private.key;

    # Client-Side Caching Configuration
    location ~* \.(jpg|jpeg|png|gif|ico|css|js|txt|pdf|svg|woff|woff2|ttf|eot)$ {
        expires 30d;  # Cache static files for 30 days
        add_header Cache-Control "public";
        add_header Vary "Accept-Encoding";  # Important for Gzip
    }

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;  # Include PHP-FPM configuration
        fastcgi_pass unix:/run/php/php7.4-fpm.sock;  # Pass PHP requests to PHP-FPM (adjust path if needed)
    }

    location ~ /\.ht {
        deny all;  # Deny access to hidden files
    }

    # Block a single IP address (replace with the IP you want to block)
    deny 192.168.1.100;

    # Logging
    access_log /var/log/nginx/example.com.access.log;
    error_log /var/log/nginx/example.com.error.log;
}
```
---

# Nginx Virtual Host Configuration Breakdown

This document provides a detailed breakdown of a typical Nginx virtual host configuration for a secure and performant website. This configuration includes an HTTP redirect to HTTPS, optimized SSL settings, client-side caching, PHP handling, security measures, and logging.

## 1. HTTP Server Block (Redirect to HTTPS)

This block handles incoming HTTP requests on port 80 and redirects them to the HTTPS version of the site.

```nginx
server {
    listen 80;
    listen [::]:80; # Listen on IPv6 as well
    server_name example.com [www.example.com](https://www.example.com);

    # Redirect all HTTP requests to HTTPS
    return 301 https://$host$request_uri;
}
```
**Components:**

* `server { ... }`: Defines a server block, which acts as a virtual host on your Nginx server. It allows you to configure how Nginx handles requests for specific domains or subdomains.
* `listen 80;`: Instructs Nginx to listen for incoming HTTP connections on port 80, the standard port for HTTP traffic.
* `listen [::]:80;` (Optional): Enables Nginx to listen for HTTP connections on port 80 over IPv6. This is important for ensuring compatibility with devices and networks that use IPv6 addressing.
* `server_name example.com www.example.com;`: Specifies the domain names that this server block should handle. Requests to `example.com` or `www.example.com` will be processed by this block. **Remember to replace these with your actual domain names.**
* `return 301 https://$host$request_uri;`: Performs a permanent (301) redirect from HTTP to HTTPS. This ensures that users are automatically directed to the secure HTTPS version of your website, improving security and SEO (Search Engine Optimization).
    * `return 301`: Sends a 301 HTTP status code, indicating a permanent redirect.
    * `https://`: The destination protocol (HTTPS).
    * `$host`: An Nginx variable containing the hostname from the client's request (e.g., `example.com` or `www.example.com`).
    * `$request_uri`: Another Nginx variable containing the full URI (Uniform Resource Identifier) of the client's request, including the path and query string (e.g., `/page/about?id=123`). This ensures that the user is redirected to the correct page on the HTTPS site.

**Importance of HTTP to HTTPS Redirect:**

* Enforces HTTPS for all communication between the user's browser and your server, protecting sensitive data from eavesdropping and man-in-the-middle attacks.
* Improves SEO ranking, as search engines generally favor websites that use HTTPS.

By implementing this HTTP server block, you can seamlessly redirect users to the secure HTTPS version of your website, enhancing security and user trust.
