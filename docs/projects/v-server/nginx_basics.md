---
sidebar_position: 10
---

import TOCInline from '@theme/TOCInline';

# Nginx Basic Setup

Setting Up and Configuring a Basic Nginx Web Server

## TOC

<TOCInline toc={toc} />

## Quickstart

### Setting Up Nginx with a Custom HTML Page

1. **Update package lists:**
   Run the following command to update your system's package database:

```bash
sudo apt update
```

2. **Install Nginx:**
   Install the Nginx web server (add `-y` to skip manual confirmation):

```bash
sudo apt install -y nginx
```

3. **Verify Nginx service status:**
   Check if Nginx was automatically started after installation:

```bash
systemctl status nginx
```

4. **Verify initial web server function:**
   Open your browser and navigate to `<your_ip>`. You should see the default "Welcome to nginx!" landing page.
5. **Create a custom directory and HTML page:**
   Standard web assets are typically served from `/var/www/html/` (e.g., the default `/var/www/html/index.nginx-debian.html`). To host custom content, create a separate directory structure:

- Create a new directory for your custom website:

```bash
sudo mkdir /var/www/alternatives/
```

- Create a custom HTML file:

```bash
sudo touch /var/www/alternatives/alternate-index.html
```

- Edit the file (e.g., using `sudo nano /var/www/alternatives/alternate-index.html`) and add your custom content (e.g., `<h1>Hello World! <Name> was here.</h1>`).

6. **Configure Nginx for custom port hosting:**
   Configuration files are located in `/etc/nginx/sites-enabled/`. Create a dedicated configuration file named `alternatives`:

```bash
sudo nano /etc/nginx/sites-enabled/alternatives
```

Add the following server block configuration:

```nginx
server {
    listen 8081; # Listens for incoming IPv4 connections on port 8081 instead of default port 80
    listen [::]:8081; # Listens for incoming IPv6 connections on port 8081

    root /var/www/alternatives; # Defines the root directory for request handling
    index alternate-index.html; # Defines the default file served when accessing the root domain

    location / { # Handles request routing matching the root path
        try_files $uri $uri/ =404; # Checks for file or folder existence; returns HTTP 404 if not found
    }
}
```

- **Test and reload configuration:**
  Always validate syntax before restarting the service:

```bash
sudo nginx -t  # Tests if sytax is correct
sudo service nginx restart
systemctl status nginx
```

- **Verify access:**
  Access your custom page via `<your_ip>:8081`. Accessing an undefined path (e.g., `<your_ip>:8081/non-existent-path`) will trigger the `404 Not Found` response.

7. **Override the default main page on Port 80:**
   To make your custom page the main homepage (served directly via `<your_ip>` on port 80):

- Open the default site configuration:

```bash
sudo nano /etc/nginx/sites-available/default
```

- Modify the `root` path:
- **From:** `root /var/www/html;`
- **To:** `root /var/www/alternatives;`

- Modify the `index` priority list:
- **From:** `index index.html index.htm index.nginx-debian.html;`
- **To:** `index alternate-index.html;`

- Test and reload Nginx:

```bash
sudo nginx -t
sudo systemctl reload nginx
systemctl status nginx
```

---

## Description

### Why Use Nginx as a Web Server?

- **High Performance & Concurrency:** Nginx uses an asynchronous, event-driven architecture, allowing it to handle thousands of simultaneous connections with minimal memory overhead.
- **Flexibility:** Works seamlessly as a standalone HTTP server, reverse proxy, or load balancer for modern applications.
- **Modular Configuration:** Modular configuration files in `sites-available` and `sites-enabled` allow hosting multiple sites cleanly on a single server.

---

## Further References

- [Nginx Official Documentation](https://nginx.org/en/docs/)
