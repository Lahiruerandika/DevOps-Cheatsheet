# How to Install Apache2 on Ubuntu Server

This guide will walk you through the step-by-step process of installing Apache2 web server on Ubuntu server.

## Prerequisites

Before you begin, make sure you have the following:

- An Ubuntu server with a non-root user with sudo privileges.
- Internet connectivity on your server.

## Table of Contents

- [Update System Packages](#update-system-packages)
- [Installing Apache](#installing-apache)
- [Checking Web Server](#checking-web-server)
- [Apache Process Management](#apache-process-management)
- [Setting Up Virtual Hosts](#setting-up-virtual-hosts)

<a name="update-system-packages"></a>
## Update System Packages

Let’s begin by updating the local package

    sudo apt update

<a name="installing-apache"></a>
## Installing Apache

To install Apache2, use the following command:
    
    sudo apt install apache2

<a name="checking-web-server"></a>
## Checking Web Server

Check with the **systemd** init system to make sure the service is running by typing:

    sudo systemctl status apache2

Output should be like that
    
    Output
    ● apache2.service - The Apache HTTP Server
        Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
        Active: active (running) since Thu 2020-04-23 22:36:30 UTC; 20h ago
        Docs: https://httpd.apache.org/docs/2.4/
    Main PID: 29435 (apache2)
        Tasks: 55 (limit: 1137)
        Memory: 8.0M
        CGroup: /system.slice/apache2.service
                ├─29435 /usr/sbin/apache2 -k start
                ├─29437 /usr/sbin/apache2 -k start
                └─29438 /usr/sbin/apache2 -k start
<a name="apache-process-management"></a>
## Apache Process Management

To stop your web server, type:

    sudo systemctl stop apache2

To start the web server when it is stopped, type:

    sudo systemctl start apache2

To stop and then start the service again, type:

    sudo systemctl restart apache2

if you are only making configuration changes. Use this command to accomplish this, It will be often reload without dropping connections:

    sudo systemctl reload apache2

<a name="setting-up-virtual-hosts"></a>
## Setting Up Virtual Hosts

In order for Apache to serve this content, it’s necessary to create a virtual host file with the correct directives.

    sudo nano /etc/apache2/sites-available/your_domain.conf

Paste in the following configuration block inside to /etc/apache2/sites-available/your_domain.conf file and edit correctly according to your server environment.

Ex :- ( your_project_path, your_domain )

    <VirtualHost *:80>
    ServerName your_domain
    DocumentRoot /path_to_your_project/public
    <Directory /path_to_your_project/public>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>
    RewriteEngine on
    RewriteCond %{SERVER_NAME} =your_domain
    RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
    </VirtualHost>

Enable the file with the a2ensite tool:

    sudo a2ensite your_domain.conf

Next, let’s test for configuration errors:

    sudo apache2ctl configtest

You should receive the following output:

    Output
    Syntax OK

Restart Apache to implement your changes:

    sudo systemctl restart apache2



After configuring Apache, your domain name should be successfully served. To test this, you can visit **http://your_domain** in your web browser. 
