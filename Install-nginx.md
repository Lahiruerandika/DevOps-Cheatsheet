# How to Install Nginx on Ubuntu Server

This guide will provide step-by-step process of installing nginx web server on Ubuntu server.

## Prerequisites

Before you begin, make sure you have the following:

- An Ubuntu server with a non-root user with sudo privileges.
- Internet connectivity on your server.

## Table of Contents

- [Installing Nginx](#installing-nginx)
- [Checking Web Server](#checking-web-server)
- [Nginx Process Management](#nginx-process-management)
- [Setting Up Virtual Hosts](#setting-up-virtual-hosts)

<a name="update-system-packages"></a>
## Update System Packages

Let’s begin by updating the local package

    sudo apt update

<a name="installing-nginx"></a>
## Installing Nginx

To install nginx, use the following command:
    
    sudo apt install nginx

<a name="checking-web-server"></a>
## Checking Web Server

Check with the **systemd** init system to make sure the service is running by typing:

    sudo systemctl status nginx

Output should like that
    Output

    ● nginx.service - A high performance web server and a reverse proxy server
    Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
    Active: active (running) since Fri 2020-04-20 16:08:19 UTC; 3 days ago
        Docs: man:nginx(8)
    Main PID: 2369 (nginx)
        Tasks: 2 (limit: 1153)
    Memory: 3.5M
    CGroup: /system.slice/nginx.service
            ├─2369 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
            └─2380 nginx: worker process

When you have your server’s IP address, enter it into your browser’s address bar, You should receive the default Nginx landing page.

<a name="nginx-process-management"></a>
## Nginx Process Management

To stop your web server, type:

    sudo systemctl stop nginx

To start the web server when it is stopped, type:

    sudo systemctl start nginx

To stop and then start the service again, type:

    sudo systemctl restart nginx

if you are only making configuration changes. Use this command to accomplish this, It will be often reload without dropping connections:

    sudo systemctl reload nginx

<a name="setting-up-virtual-hosts"></a>
## Setting Up Virtual Hosts

In order for Nginx to serve this content, it’s necessary to create a server block with the correct directives.

    sudo nano /etc/nginx/sites-available/your_domain.conf

Paste in the following configuration block inside to /etc/nginx/sites-available//your_domain.conf file and edit correctly according to your server environment.

Ex :- ( your_project_path, your_domain, php version )

    server {

        root /your_project_path/public;
        index index.php index.html index.htm;
        server_name your_domain;
        client_max_body_size 500M;
        location /uploads {
                client_max_body_size 500M;
        }
        location / {
                try_files $uri $uri/ /index.php?$query_string;
        }
        location ~*  \.(jpg|jpeg|png|gif)$1 {
                expires 365d;
        }
        location ~*  \.(ico|css|js)$ {
                expires 365d;
        }
        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php8.1-fpm.sock;
        }
        location ~ /\.ht {
                deny all;
        }

    }

Enable the file with the a2ensite tool:

    sudo ln -s /etc/nginx/sites-available/your_domain.conf /etc/nginx/sites-enabled/

Next, let’s test for configuration errors:

    sudo nginx -t

You should receive the following output:

nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful

Restart nginx to implement your changes:

    sudo systemctl restart nginx



After configuring nginx, your domain name should be successfully served. To test this, you can visit **http://your_domain** in your web browser. 
