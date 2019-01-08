---
title:  "PHP and MySQL Installation and Why no need for Web Server"
search: true
categories: 
  - Web
last_modified_at: 2018-11-15T08:05:34-05:00
header:
  teaser: /assets/images/blog/setting-Up-localhost.jpg
---

![setting-up-localhost](/assets/images/blog/setting-Up-localhost.jpg)

# Why setup localhost

PHP: Hypertext Pre-Processor is an open-source server-side scripting language used for web development. If you are reading this blog, it's pretty evident that you know how to use PHP and you are now trying to install PHP in your computer. As PHP is a server-side scripting language, the developer can run any PHP code via the browser.

# Usual PHP installation

Usually, for working on PHP, the developer has to install:-
1. Web Server
2. MySQL (if you are using database)
3. PHP

# Types of Installation

Depending on your operating system, the installatio can be classified into:-
1. MAMP Server (Mac, Apache2, MySQL, PHP)
2. LAMP Server (Linux, Apache2, MySQL, PHP)
3. WAMP Server (Windows, Apache2, MySQL, PHP)
4. X-AMPP Server (Any Operating system, Apache2, MySQL, PHP, Perl)

# Why Install Web Server or Why not Install Web Server

Web server is required if you are setting up a server. If you are setting up for development. You can run your PHP code using the following command.

```
$ php -S 0.0.0.0:8080
```

After executing the command, you can open the address in your browser to open your site.

# Installing MAMP Server

I have already written a blog on how to setup a server on Mac in [this link](https://www.sashwat.in/linux/macos/setup-localhost-mac/). Just skip install web server (Apache) (If for setting up localhost). There is another way to install a MAMP server. There is a application named MAMP server that can be used to activate web server on a click. To install, goto [this link](https://www.mamp.info/en/). Just install the .dmg and follow the instructions to install the MAMP server. 

# Installing LAMP Server

## Fedora

1. First, we will update the system.
```
$ sudo yum update
```

2. Let's install web server (Dont install if for localhost).
```
$ sudo yum install httpd
```

3. Let's start the httpd service.
```
$ sudo service httpd start
```

4. Now, we will install MySQL for working on databases.
```
$ sudo yum install mysql mysql-server
```

5. Now, we will start MySQL service.
```
$ sudo service mysqld start
```

6. Now, we have to setup root password for MySQL.
```
$ sudo /usr/bin/mysql_secure_installation
```

7. Let's install PHP.
```
$ sudo yum install php php-mysql
```

8. Now, we have to configure the server and MySQL service to start automatically after every boot. If for localhost, don't configure the server. Just configure MySQL.
```
$ sudo chkconfig httpd on
$ sudo chkconfig mysqld on
```

9. For server, to check, we will create a PHP file in web home directory.
```
$ sudo nano /var/www/html/info.php
```
10. To check if PHP is working, we will run phpinfo().
```
$ sudo echo "<?php phpinfo(); ?>" >> /var/www/html/info.php
```
11. Open browser and goto localhost/info.php. If PHP not working, you will get a blank page or the php code will be visible.

12. If you want to use phpmyadmin, install phpmyadmin by using the following command. If you are using phpmyadmin, then you have to install web server.
```
$ sudo dnf -y install phpMyAdmin php-mysqlnd php-mcrypt php-php-gettext
```

13. Restart apache server.
```
$ sudo systemctl restart httpd
```

## RHEL / CentOS

1. Update the system.
```
$ sudo yum update
```

2. Install web server.
```
$ sudo yum install httpd
```

3. Add firewall exception to HTTP service.
```
$ firewall-cmd --permanent --add-service=http
```

4. Now, we have to restart firewall to implement changes.
```
$ systemctl restart firewalld
```

5. Now, we open port 80 in firewall.
```
$ firewall-cmd —add-port=80/tcp
```

6. Now, we will install PHP.
```
$ sudo yum install php php-mysql php-pdo php-gd php-mbstring
```

7. We will check if PHP is working by running phpinfo().
```
$ echo "<?php phpinfo(); ?>" >> /var/www/html/info.php 
```
Now check if PHP is working by opening localhost/info.php in your browser.

8. Now, we will install mariaDB for database.
```
$ sudo yum install mariadb-server mariadb
```

9. Start the database service.
```
$ sudo systemctl start mariadb
```

10. Now, we have to setup root password for MySQL.
```
$ mysql_secure_installation
```

11. To install phpmyadmin.
```
$ sudo yum install http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el7.rf.x86_64.rpm
$ sudo yum install phpmyadmin
```

12. We have to edit phpmyadmin configuration file.
```
$ nano /etc/httpd/conf.d/phpmyadmin.conf
```

13. Remove # (comment) from the following lines inside the file.
```
Order Deny,Allow
Deny from all
Allow from 127.0.0.1
```

14. Now we have to enable httpd and mariadb so that they will start automatically after every boot.
```
$ systemctl enable mariadb
$ systemctl enable httpd
```


# Installing WAMPSERVER

1. Download Wampserver using [this link](http://www.wampserver.com/en/#download-wrapper).
2. Open installation file and follow the steps to install it to the system.
3. Open wampserver to enable webserver, database and PHP.
4. To check if wampserver is working, goto http://localhost in the browser.


# Installing XAMPP server

1. Download XAMPP using [this link](https://www.apachefriends.org/index.html). Download the installation file for your operating system.
2. Install it by following the instructions.
3. Open XAMPP to enable apache, mysql and php.