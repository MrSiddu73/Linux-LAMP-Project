\# Setup Instructions – Linux LAMP Project



This guide will help you set up the LAMP stack (Linux, Nginx, MariaDB, PHP) on an AWS EC2 instance and deploy a sample signup form application.



---



\## 🟠 Step 1 – Update the System



```bash

sudo yum update -y



\## 🟠 Step 2 – Install Required Packages

sudo yum install nginx -y

sudo yum install mariadb105-server -y

sudo yum install php -y



Verify installations:



which nginx

which mariadb

which php



\## 🟠 Step 3 – Navigate to Web Directory

cd /usr/share/nginx/html/



Create the PHP files:

sudo vim sample.php

sudo vim submit.php

Paste the provided code for sample.php and submit.php into their respective files.



\## 🟠 Step 4 – Start Services

sudo systemctl start nginx

sudo systemctl start mariadb

sudo systemctl start php-fpm



\## 🟠 Step 5 – Configure the Database

Login to MariaDB:

sudo mysql

Run the following commands inside the MariaDB prompt:



ALTER USER 'root'@'localhost' IDENTIFIED BY 'root';

CREATE DATABASE facebook;

USE facebook;



CREATE TABLE users (

&nbsp;   id INT(11) AUTO\_INCREMENT PRIMARY KEY,

&nbsp;   name VARCHAR(100),

&nbsp;   email VARCHAR(100),

&nbsp;   website VARCHAR(100),

&nbsp;   comment TEXT,

&nbsp;   gender VARCHAR(10)

);

Press Ctrl + D to exit the database prompt.



\## 🟠 Step 6 – Configure Security Group

Go to your EC2 instance settings in AWS.



Edit the Inbound rules.



Add a rule to allow HTTP traffic:



Type: HTTP



Protocol: TCP



Port range: 80



Source: Anywhere IPV4 (0.0.0.0/0)



\## 🟠 Step 7 – Test the Application

Open your browser and go to:



http://<your-ec2-public-ip>/sample.php

The signup form should appear.



Fill in the details and submit the form.



It will display the submitted data on the screen.



\## 🟠 Step 8 – Verify Database Entries

Return to the terminal of your EC2 instance.



Enter the database again:



sudo mysql -u root -p

Enter the password root and run:



USE facebook;

SELECT \* FROM users;

You will see the records submitted through the form.



✅ Notes

Make sure port 80 is open in the security group.



Keep database credentials secure.



This project is intended for learning purposes and should not be used in production without proper security measures.



You're all set to run your LAMP-based web application on AWS EC2!

