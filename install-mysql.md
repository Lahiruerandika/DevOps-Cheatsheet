# How to Install MySQL on Ubuntu Server

MySQL is a popular open-source relational database management system that allows you to store and manage large amounts of data efficiently. This guide will walk you through the process of installing MySQL on an Ubuntu server.

## Prerequisites

Before you begin, make sure you have the following:

- An Ubuntu server with a non-root user with sudo privileges.
- Ubuntu server running a supported version (e.g., Ubuntu 20.04).
- Internet connectivity on your server.

## Table of Contents

- [Update System Packages](#update-system-packages)
- [Installing MySQL](#installing-mysql)
- [Configuring MySQL](#configuring-mysql)
- [Testing MySQL](#testing-mysql)


<a name="update-system-packages"></a>
## Update System Packages

Let’s begin by updating the local package

    sudo apt update

<a name="installing-mysql"></a>
## Installing MySQL

To install the mysql-server package, use the following command:
    
    sudo apt install mysql-server

Ensure that the server is running using following command:



    sudo systemctl start mysql.service  

Note: These commands will install and launch MySQL, but they won't ask you to configure it or set a password.
<a name="configuring-mysql"></a>
## Configuring MySQL
To check if MySQL is running properly, use the following command to connect to the MySQL server as the root user:

    sudo mysql
    
You can use following commands to create a new user after you have access to the MySQL prompt.

    
    CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';

**Note**: According to the above command, The host refers to the location from which the user is allowed to connect. 'localhost' means the user can only connect from the same machine where the MySQL server is installed.

After creating your new user, you can grant them the appropriate privileges.
    
    GRANT ALL ON *.* TO username@'localhost';
That command grants all privileges on all databases and tables to a specific user account when connecting from the 'localhost' host.

Below command will free up any memory that the server cached as a result of the preceding CREATE USER and GRANT statements:
    
    FLUSH PRIVILEGES;

Now you can view the privileges were granted successfully by executing the SHOW GRANTS statement for the specific user:

    SHOW GRANTS FOR 'username'@'localhost';


<a name="testing-mysql"></a>
## Testing MySQL

To test this, check its status.:

    sudo systemctl status mysql.service

 Output similar to the following:

    Output
    ● mysql.service - MySQL Community Server
        Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset: enabled)
        Active: active (running) since Tue 2020-04-21 12:56:48 UTC; 6min ago
    Main PID: 10382 (mysqld)
        Status: "Server is operational"
        Tasks: 39 (limit: 1137)
        Memory: 370.0M
        CGroup: /system.slice/mysql.service
                └─10382 /usr/sbin/mysqld

You now have a basic MySQL setup installed on your server.

