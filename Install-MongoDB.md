# How To Install MongoDB on Ubuntu

MongoDB is a popular open-source NoSQL database that provides scalability, flexibility, and high performance for modern applications. If you're using Ubuntu as your operating system, this guide will walk you through the step-by-step process of installing MongoDB.

## Prerequisites

Before you begin, make sure you have the following:

- An Ubuntu server with a non-root user with sudo privileges.
- Internet connectivity on your server.

## Table of Contents

- [Import the MongoDB GPG Key](#import-the-mongodb-gpg-key)
- [Add the MongoDB Repository](#add-the-mongodb-repository)
- [Update the Package Repository](#update-the-package-repository)
- [Install MongoDB](#install-mongodb)
- [Start and Enable MongoDB](#start-and-enable-mongodb)
- [Verify the MongoDB Installation](#verify-the-mongodb-installation)
- [Managing the MongoDB Service](#managing-the-mongodb-service)

<a name="import-the-mongodb-gpg-key"></a>
## Import the MongoDB GPG Key

Import the MongoDB GPG key using the following command:


    curl -fsSL https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -

**Note**

 If you intend to use a version of MongoDB other than 4.4, be sure to change 4.4 in the URL portion of this command to align with the version you want to install:

<a name="add-the-mongodb-repository"></a>
##  Add the MongoDB Repository

Next, add the MongoDB repository to your system's software sources list by executing the following command:
    
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list

<a name="update-the-package-repository"></a>
## Update the Package Repository

Update the package repository to ensure you get the latest package information by running the following command:

    sudo apt update


<a name="install-mongodb"></a>
## Install MongoDB

Install MongoDB by executing the following command:

    sudo apt install mongodb-org

*This command installs the MongoDB packages, including the MongoDB server, shell, and other tools.*

<a name="start-and-enable-mongodb"></a>
## Start and Enable MongoDB

Start the MongoDB service using the following command:

    sudo systemctl start mongod.service

This command will return output like the following:

    Output
    ● mongod.service - MongoDB Database Server
        Loaded: loaded (/lib/systemd/system/mongod.service; disabled; vendor preset: enabled)
        Active: active (running) since Tue 2020-06-09 12:57:06 UTC; 2s ago
        Docs: https://docs.mongodb.org/manual
    Main PID: 37128 (mongod)
        Memory: 64.8M
        CGroup: /system.slice/mongod.service
                └─37128 /usr/bin/mongod --config /etc/mongod.conf

To ensure that MongoDB starts automatically on system boot, enable the service using this command:

    sudo systemctl enable mongod

<a name="verify-the-mongodb-installation"></a>
## Verify the MongoDB Installation

    mongo

If MongoDB is installed correctly, you should see the MongoDB shell prompt, which looks like this:

    MongoDB shell version v4.4.0
    connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb

Congratulations! You have successfully installed MongoDB on Ubuntu. You can now start using MongoDB for your applications or projects.

<a name="managing-the-mongodb-service"></a>
## Managing the MongoDB Service

To stop the service anytime by typing:

    sudo systemctl stop mongod

To start the service when it’s stopped, run:

    sudo systemctl start mongod


To  restart the server when it’s already running:

    sudo systemctl restart mongod

Now you are already enabled MongoDB to start automatically with the server. If you ever wish to disable this automatic startup, use following commad:

    sudo systemctl disable mongod

Feel free to explore MongoDB's extensive documentation and resources to learn more about its features, best practices, and advanced usage. Happy coding with MongoDB!