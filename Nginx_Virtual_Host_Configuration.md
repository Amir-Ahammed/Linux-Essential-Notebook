
```nginx
# HTTP Server Block (Redirect to HTTPS):

server {
    listen 80;
    listen [::]:80; # Listen on IPv6 as well
    server_name example.com [www.example.com](https://www.example.com);

    # Redirect all HTTP requests to HTTPS
    return 301 https://$host$request_uri;
}

# HTTPS Server Block:

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
---

## 2. HTTPS Server Block

```nginx
server {
    listen 443 ssl default_server;
    server_name example.com [www.example.com](https://www.example.com);

    # Optimized SSL Settings
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_prefer_server_ciphers on;
    ssl_ciphers 'EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH';
    ssl_ecdh_curve secp384r1;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 10m;
    ssl_stapling on;
    ssl_stapling_verify on;

    ssl_certificate /path/to/your/certificate.crt;
    ssl_certificate_key /path/to/your/private.key;

    # Client-Side Caching Configuration
    location ~* \.(jpg|jpeg|png|gif|ico|css|js|txt|pdf|svg|woff|woff2|ttf|eot)$ {
        expires 30d;
        add_header Cache-Control "public";
        add_header Vary "Accept-Encoding";
    }

    location / {
        try_files $uri <span class="math-inline">uri/ \=404;
\}
location \~ \\\.php</span> {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.4-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }

    deny 192.168.1.100;

    # Logging
    access_log /var/log/nginx/example.com.access.log;
    error_log /var/log/nginx/example.com.error.log;
}
```

# Nginx Virtual Host Configuration Breakdown (HTTPS Server Block)

This section delves into the HTTPS server block within a typical Nginx virtual host configuration. This block handles secure HTTPS traffic on port 443, ensuring encrypted communication between your website and users' browsers.

**Components:**

* **`listen 443 ssl default_server;`:**
    * **`listen 443`**: Instructs Nginx to listen for incoming HTTPS connections on port 443, the standard port for secure HTTP traffic.
    * **`ssl`**: Enables SSL/TLS encryption for this server block, safeguarding data transmission.
    * **`default_server`**: Designates this block as the default server for HTTPS connections on port 443. This is crucial when Server Name Indication (SNI) is not available or for handling requests for unknown hosts.
* **`server_name example.com www.example.com;`:** Specifies the domain names that this server block should handle. Requests to `example.com` or `www.example.com` will be processed by this block. **Remember to replace these placeholders with your actual domain names.**

**Optimized SSL Settings:**

* `ssl_protocols TLSv1.2 TLSv1.3;`: Defines the allowed SSL/TLS protocols. For enhanced security, it's recommended to use only TLSv1.2 and TLSv1.3.
* `ssl_prefer_server_ciphers on;`: Informs Nginx to prioritize its own cipher suite over the client's preference.
* `ssl_ciphers 'EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH';`: Specifies a robust cipher suite for encryption, ensuring strong data protection.
* `ssl_ecdh_curve secp384r1;`: Enables Perfect Forward Secrecy (PFS) by defining the elliptic curve used for key exchange.
* `ssl_session_cache shared:SSL:10m;`: Establishes a shared SSL session cache to improve performance by reusing existing SSL sessions.
* `ssl_session_timeout 10m;`: Sets the timeout duration for SSL sessions.
* `ssl_stapling on;`: Enables OCSP (Online Certificate Status Protocol) stapling, which allows the server to provide certificate revocation information to clients, enhancing performance and user trust.
* `ssl_stapling_verify on;`: Instructs Nginx to verify the validity of OCSP responses received from the certificate authority.
* `ssl_certificate /path/to/your/certificate.crt;` and `ssl_certificate_key /path/to/your/private.key;`:
    * Replace `/path/to/your/certificate.crt` with the actual path to your SSL certificate file.
    * Replace `/path/to/your/private.key` with the actual path to your private key file.** These files are essential for establishing a secure HTTPS connection.

**Additional Features:**

* Client-Side Caching:
    * `location ~* \.(jpg|jpeg|png|gif|ico|css|js|txt|pdf|svg|woff|woff2|ttf|eot)$`: Targets common static file types (images, stylesheets, JavaScript, etc.) using a regular expression for efficient matching.
    * `expires 30d;`: Sets the `Expires` header, instructing browsers to cache these static files for 30 days, reducing server load and improving website performance.
    * `add_header Cache-Control "public";`: Enables public caching, allowing browsers and intermediate caches to store these static files for future use.
    * `add_header Vary "Accept-Encoding";`: Crucial for Gzip compression; informs caches that the response can vary based on the `Accept-Encoding` header sent by the client's browser, enabling efficient content delivery.
* **Default Location:**
    * `location /`: Catches all requests that don't match any other location block within this server block.
    * `try_files $uri $uri/ =404;`: Attempts to serve the requested file (`$uri`) or directory (`$uri/`). If neither is found, a 404 (Not Found) error is returned.
* **PHP Handling:**
    * `location ~ \.php$`: Matches requests for files with the `.php` extension, indicating PHP scripts.
    * `include snippets/fastcgi-php.conf;`: Includes a separate configuration file (likely `snippets/fastcgi

* **Hidden Files:**
    * `location ~ /\.ht`: This location block targets files or directories that begin with a dot (`.`) followed by "ht" (e.g., `.htaccess`). These files are often used for configuration purposes and are typically hidden from web browsers.
    * `deny all;`: This directive denies access to any requests that match this location block. This prevents users from directly accessing hidden configuration files, enhancing website security.

* **IP Blocking:**
    * `deny 192.168.1.100;`: This line blocks access requests originating from the IP address `192.168.1.100`. You can replace this with the specific IP address you want to restrict. This can be useful for mitigating brute-force attacks or blocking malicious traffic.

* **Logging:**
    * `access_log /var/log/nginx/example.com.access.log;`: This directive configures Nginx to log access information for this server block. The log file will be stored at `/var/log/nginx/example.com.access.log`. This log can be helpful for troubleshooting errors, analyzing website traffic patterns, and identifying security threats.
    * `error_log /var/log/nginx/example.com.error.log;`: This directive specifies the path for the error log file, which will record any errors encountered by Nginx while processing requests for this server block. The log file will be located at `/var/log/nginx/example.com.error.log`. Examining the error log can aid in debugging configuration issues and server malfunctions.
  

**Remember to replace placeholders like `/path/to/your/certificate.crt` and `example.com` with your actual values.**

By incorporating these additional features, you can enhance the security, performance, and manageability of your Nginx virtual host configuration.



