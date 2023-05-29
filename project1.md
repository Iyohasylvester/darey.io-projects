# SETTING UP A LAMP STACK WEB SERVER IN THE AWS CLOUD

A LAMP stack web server is a set of frameworks and tools that comprises Linux, Apache server, MySql and PHP. The following are the steps I took in setting up a LAMP stack web server in the AWS cloud:

## STEP 2: Launching A New EC2 Instance in the AWS cloud
With my aws account already setup, I launched a new EC2 Instance of t2.micro family with Ubuntu Server 20.04 LTS (HVM) and downloaded a new private key (.pem file).


![image](https://github.com/Iyohasylvester/darey.io-projects/assets/133134564/d76edd8c-a3c1-4fcc-9ded-8694c038df4c)

STEP 3 — INSTALLING APACHE2 AND UPDATING THE FIREWALL

![image](https://github.com/Iyohasylvester/darey.io-projects/assets/133134564/2e537ccb-c663-471a-9bf4-4e535f26e0d5)

To verify that apache2 is running as a Service in our OS, use following command: 

`sudo systemctl status apache2`

![image](https://github.com/Iyohasylvester/darey.io-projects/assets/133134564/cc6dba3b-a96b-476b-bbf2-c4c8c376cc4d)


To access it locally in my Ubuntu shell; `curl http://localhost:80 or curl http://127.0.0.1:80`

Testing how the Apache HTTP server can respond to requests from the Internet; Pasting my public address in the browser and tapping enter:

![image](https://github.com/Iyohasylvester/darey.io-projects/assets/133134564/33367a93-d20b-4706-9da3-1021cea973e3)

STEP 4 — INSTALLING MYSQL

To acquire and install the software: `sudo apt install mysql-server`

![image](https://github.com/Iyohasylvester/darey.io-projects/assets/133134564/86fdc434-d397-44f6-bbce-1c5bea2921eb)

![image](https://github.com/Iyohasylvester/darey.io-projects/assets/133134564/19162108-8bdc-40be-a70c-e6caa05a33f9)


After a successful installation, it’s recommended that one runs a security script that comes pre-installed with MySQL which removes insecure default settings and lock down access to my database system. The following command is entered: `sudo mysql_secure_installation`

Next is accepting to configure the VALIDATE PASSWORD PLUGIN when prompted, and selecting any of the three levels of the password validation policy and then typing a new password that corresponds to the level of password validation policy selected.

And finally tapping the Y and hitting Enter key at the subsequent prompt that follow after which will remove some anonymous users and the test database, disable remote root logins, and load these new rules so that MySQL immediately respects the changes you have made.


![image](https://github.com/Iyohasylvester/darey.io-projects/assets/133134564/00a58b19-3e07-47b3-96a0-67a0dff5498d)

Testing if I am able to log into MySQL console: `sudo mysql`


STEP 5 — INSTALLING PHP

The following steps are taken to installing PHP in the Instance which will allow us to display dynamic content to the end user:

Installing PHP and two other packages: `sudo apt install php libapache2-mod-php php-mysql`


![image](https://github.com/Iyohasylvester/darey.io-projects/assets/133134564/95db23b0-9fd5-49ed-9af1-b6dcd9e038e7)


To confirm the PHP version installed: `php –v`

![image](https://github.com/Iyohasylvester/darey.io-projects/assets/133134564/cfb7bf81-eed4-48f0-b6e7-c33690bf6f5c)


STEP 6 — CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE

Apache on Ubuntu 20.04 has one server block enabled by default that is configured to serve documents from the /var/www/html directory. The following steps are taken to setting up a virtual host:

Creating a directory called projectLamp as my domain: `sudo mkdir /var/www/projectlamp`

Assigning ownership of the directory with the $USER environment variable, which will reference my current system user: `sudo chown -R $USER:$USER /var/www/projectlamp`

creating and opening a new configuration file in Apache’s sites-available directory: 
`sudo vi /etc/apache2/sites-available/projectlamp.conf`

pasting the following configurations in the file:

``
<VirtualHost *:80>
	    ServerName projectlamp
	    ServerAlias www.projectlamp 
	    ServerAdmin webmaster@localhost
	    DocumentRoot /var/www/projectlamp
	    ErrorLog ${APACHE_LOG_DIR}/error.log
	    CustomLog ${APACHE_LOG_DIR}/access.log combined
	</VirtualHost>
  ``
  
  ![image](https://github.com/Iyohasylvester/darey.io-projects/assets/133134564/ef12a152-5205-429a-9d90-7380da8e4ae6)


Save and quit by hitting esc key and typing :wq and pressing enter key

Enabling the new virtual host:  `sudo a2ensite projectlamp`

Disabling the default website that comes installed with Apache: `sudo a2dissite 000-default`

Ensuring my configuration doesn’t contain any error: ` sudo apache2ctl configtest`

Reloading Apache so these changes take effect: `sudo systemctl reload apache2`

Creating an index.html file in the location of my domain directory inorder to test that the virtual host works as expected : sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.htm


![image](https://github.com/Iyohasylvester/darey.io-projects/assets/133134564/a60f8325-e3b3-474d-a187-06017c7049e1)


Running my IP address on the browser to test if it works as expected

![image](https://github.com/Iyohasylvester/darey.io-projects/assets/133134564/2f739095-936c-4bcc-8c29-e213748dd127)


STEP 7 — ENABLE PHP ON THE WEBSITE

With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php . To change this behavior is to edit the dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive:

Editing the dir.conf file : `sudo vim /etc/apache2/mods-enabled/dir.conf`
```
<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```

Reloading the apache server: $ sudo systemctl reload apache2

Creating an index.php file and adding a PHP script in it to test that PHP is correctly installed and configured on your server: 
`vim /var/www/projectlamp/index.php`

Adding the following PHP script
```
<?php
phpinfo();
```


![image](https://github.com/Iyohasylvester/darey.io-projects/assets/133134564/c4978995-3cd8-4ebd-8938-6ef567fa27a7)

Refreshing my web page

![image](https://github.com/Iyohasylvester/darey.io-projects/assets/133134564/4a263919-a066-4dce-a29d-dcfbed588245)


Removing the php file as it contains sensitive information about your PHP environment and my Ubuntu server 
`sudo rm /var/www/projectlamp/index.php`


