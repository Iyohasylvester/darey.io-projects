SETTING UP A LEMP STACK WEB SERVER ON AWS CLOUD

A LEMP stack is a set of tools used to deploying a web application. Similar to the LAMP stack project covered in the project1 of my repository but with an alternative Web Server called NGINX, which is also very popular and widely used by many websites. The following are the steps I took to setting up a LEMP stack:

STEP 1: Launching an EC2 Instance


I created a new EC2 Instance of t2.nano family with Ubuntu Server 20.04 LTS (HVM) image from my aws account. After a successful launch of the EC2 instance(ubuntu server), I connected to the EC2 instance from my Git bash (as a windows user) terminal with my private key(.pem file) by entering these command in the terminal:    

`ssh -i <Your-private-key.pem> ubuntu@<EC2-Public-IP-address>` which looks like this:



Step 2: Installing the Nginx Web Server


In order to display web pages to the site,  A high performance web server (Nginx) has to be employed. After a successful connection to the EC2 machine, the following command is entered:

- Updating the server’s package: ` sudo apt update `


- Installing Nginx: ` sudo apt install nginx ` 





