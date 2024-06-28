# Hosted-a-WordPress-Website
This repository contains the README file for my WordPress website hosted on AWS EC2.

---


# AWS WordPress Website Setup on EC2

Welcome to my AWS WordPress project repository! This project demonstrates how I successfully hosted a WordPress application using an AWS EC2 instance. Below, I'll walk you through the detailed steps I took to set up and configure the necessary components: Apache2, PHP, and MySQL.

## Prerequisites

Before we dive into the setup, make sure you have the following:

- An AWS account
- An EC2 instance running Ubuntu 22.04
- SSH access to the EC2 instance

## Step 1: Update the System

First, I updated the system to ensure all packages were up-to-date. This helps in avoiding any potential issues with outdated software.

```bash
sudo apt update
```

## Step 2: Install Apache2

Next, I installed Apache2, the web server that will host the WordPress site. Apache2 is a reliable and widely-used web server.

```bash
sudo apt install apache2 -y
```

To verify that Apache2 was installed correctly, I opened a web browser and entered the public IP address of my EC2 instance. This displayed the Apache2 default welcome page, confirming the successful installation.

## Step 3: Install PHP and Extensions

WordPress requires PHP to run, so the next step was to install PHP along with the necessary extensions.

```bash
sudo apt update
sudo apt install php libapache2-mod-php php-mysql -y
sudo apt install php-mbstring php-bcmath php-intl php-soap php-zip php-gd php-curl php-cli php-xml php-xmlrpc php-gmp php-common -y
```

After installing PHP, I verified the installation by checking the PHP version with the following command:

```bash
php -v
```

## Step 4: Install MySQL

For the database, I installed MySQL. WordPress uses MySQL to store its data, so this was a crucial step.

```bash
sudo apt install mysql-server -y
```

After installing MySQL, I secured the installation and set a root password to ensure the database was protected.

```bash
sudo mysql

# In the MySQL shell, I ran the following commands
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_password';
exit
```

Then, I created a database and a user specifically for WordPress. This step is important for managing WordPress data separately and securely.

```bash
sudo mysql -u root -p

# In the MySQL shell, I ran the following commands
CREATE DATABASE wordpress;
CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpressuser'@'localhost';
FLUSH PRIVILEGES;
exit
```

## Step 5: Restart Apache Service

After creating the WordPress database, I restarted the Apache service to ensure all changes took effect.

```bash
sudo systemctl restart apache2
```

## Step 6: Set Up WordPress

Next, I navigated to the HTML directory and removed the default `index.html` file.

```bash
cd /var/www/html/
sudo rm -f index.html
```

Then, I downloaded the latest version of WordPress.

```bash
sudo wget https://wordpress.org/latest.zip
sudo unzip latest.zip
sudo rm -rf latest.zip
```

I moved the WordPress files to the HTML directory.

```bash
cd wordpress/
sudo cp -rvf * /var/www/html/
cd ..
sudo rm -rf wordpress/
```

## Step 7: Configure WordPress

I opened a web browser, entered the public IPv4 address of my EC2 instance, and followed the WordPress setup instructions. I entered the database name (`wordpress`), the database username, and password, then clicked submit. WordPress provided a configuration script (`wp-config.php`), which I copied.

Back in the EC2 instance, I edited the `wp-config.php` file to include the configuration details.

```bash
sudo nano /var/www/html/wp-config.php
```

I pasted the content and saved the file.

## Step 8: Complete WordPress Installation

Returning to the WordPress setup page, I ran the installation. I entered the site title, admin username, and password, then logged in to the WordPress dashboard.

## Final Result

Here are some screenshots of the final WordPress setup:

**WordPress Dashboard:**

![WordPress Dashboard](images/Hosted a wordpress App in AWS using EC2.png)

**WordPress Site:**

![WordPress Site](images/the hosed of wordpress app.png)

## Conclusion

By following these steps, I successfully set up Apache2, PHP, and MySQL on my AWS EC2 instance. With the server environment ready, the next step would be to download and configure WordPress, bringing the application to life.

This project demonstrates my ability to manage server infrastructure and deploy web applications on cloud platforms, showcasing both my technical skills and my attention to detail.


---
