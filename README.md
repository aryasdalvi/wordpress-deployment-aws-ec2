# WordPress Deployment on AWS EC2

## Introduction

This project demonstrates the deployment of a WordPress website on an AWS EC2 instance running Amazon Linux 2023. The deployment uses Apache HTTP Server, PHP, and MariaDB/MySQL to host and manage a WordPress website.

## Objectives

- Configure an AWS EC2 instance for WordPress deployment.
- Install Apache, PHP, and MariaDB.
- Automate service installation and configuration using a shell script.
- Download and extract WordPress.
- Create a database for WordPress.
- Configure file ownership and complete the WordPress installation.

## Architecture

**Application Flow:**

<img width="1774" height="887" alt="image" src="https://github.com/user-attachments/assets/7cf37194-d189-455d-bd3a-629a908b2d62" />



User / Browser → Internet → AWS EC2 Instance → Apache HTTP Server → PHP → WordPress Application → MariaDB Database

The EC2 instance hosts the WordPress application. Apache handles HTTP requests, PHP executes WordPress code, and MariaDB stores website content and settings.



## Technologies Used

| Technology | Purpose |
|---|---|
| AWS EC2 | Cloud server hosting |
| Amazon Linux 2023 | Operating system |
| Apache HTTP Server | Web server |
| PHP | WordPress application runtime |
| MariaDB/MySQL | Database management |
| WordPress | Content management system |
| Bash | Shell scripting and automation |
| Linux | Server administration |

## Deployment Steps

### 1. Create the LAMP Shell Script

Created a shell script named `lamp.sh`:

```bash
sudo vim lamp.sh
```

Added the installation and service commands:

```bash
sudo yum update
sudo yum install httpd mariadb105-server php -y
sudo systemctl start httpd mariadb php-fpm
sudo systemctl enable httpd mariadb php-fpm
```

Executed the script:

```bash
sudo bash lamp.sh
```

### 2. Download WordPress

Navigated to the web server directory:

```bash
cd /var/www/html/
```

Downloaded the WordPress archive:

```bash
sudo wget https://wordpress.org/latest.tar.gz
```

Extracted the archive:

```bash
sudo tar -xzvf latest.tar.gz -C /var/www/html/
```

The extracted WordPress files were available in the `wordpress` directory.

### 3. Install the PHP Database Connector

Installed the PHP MySQL connector:

```bash
sudo yum install php8.5-mysqlnd -y
```

The package version depends on the PHP version and the packages available in the configured repositories.

### 4. Create the WordPress Database

Opened the MariaDB/MySQL command line:

```bash
sudo mysql
```

Created the database:

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'root';
CREATE DATABASE wordpressdb;
EXIT;
```

The `wordpressdb` database was created for the WordPress installation.

### 5. Configure WordPress Directory Ownership

Changed ownership of the WordPress directory:

```bash
sudo chown -R apache:apache /var/www/html/wordpress
```

This assigns ownership of the WordPress files and directories to the Apache service account.

### 6. Complete WordPress Setup

Opened the WordPress installation page in a browser:

**Website URL:** [http://18.209.48.75/wordpress](http://18.209.48.75/wordpress)

Entered the database connection details and completed the WordPress installation.

### 7. Configure the Website

After installation, accessed the WordPress site and customized the website appearance using the WordPress interface.

## Screenshots

- Wordpress File Terminal:
<img width="1389" height="727" alt="Screenshot 2026-10-23 193843" src="https://github.com/user-attachments/assets/b01ef87f-e9d3-4e28-87da-8a8d68338b85" />

— EC2 instance details:
<img width="1888" height="639" alt="Screenshot 2026-10-23 193513" src="https://github.com/user-attachments/assets/4df3892e-62a0-4141-9f6f-98eed4ce9b21" />

- Deployed WordPress website in the browser:
<img width="1907" height="942" alt="Screenshot 2026-10-23 193645" src="https://github.com/user-attachments/assets/263211e3-f889-4de5-aff0-c068894f0a6b" />


## Key Learnings

- AWS EC2 provisioning and Linux server administration
- LAMP stack installation and service management
- Shell scripting for installation tasks
- WordPress download and deployment
- MariaDB database creation
- Linux file ownership and permissions
- WordPress database configuration and browser-based setup


## Summary

Deployed a WordPress website on AWS EC2 using Apache, PHP, and MariaDB. Used a shell script to install required services, downloaded WordPress, created its database, configured directory ownership, and completed the browser-based setup.

