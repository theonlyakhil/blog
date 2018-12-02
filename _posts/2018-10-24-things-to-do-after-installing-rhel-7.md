---
title:  "Things to do after installing RHEL 7"
search: true
categories: 
  - Linux
  - RHEL
last_modified_at: 2018-10-24T08:05:34-05:00
header:
  teaser: /assets/images/blog/things-to-do-after-installing-rhel-7.png
---
![RHEL7](/assets/images/blog/things-to-do-after-installing-rhel-7.png)

The RHEL is RedHat Enterprise Linux,  a server distribution of Linux. RHEL is not like other Linux distribution because you have to pay money for the company's services. But, the Operating System is free to use. The latest version of RHEL is RHEL 7.
The following things where the first things I did, after install RHEL 7 on my virtual machine.
First, we have to do is enable RedHat subscription. I subscribed for a developer account through the RedHat website and developer subscription is free. Our machine should be registered for doing anything. This registration can be done using a package called subscription manager. Follow the steps to register your machine.

```yaml
$ subscription-manager register --username your_username --password your_password --auto-attach
$ subscription-manager list --available
$ subscription-manager list
$ subscription-manager service-level --list
$ subscription-manager service-level --set=self-support
```

Now, we need to enable yum repositories to install any applications via the repo list. The following steps will enable yum repositories.

```yaml
$ subscription-manager repos --list
$ yum repolist all
$ yum repolist
$ vi /etc/yum.repos.d/redhat.repo
```
Uncomment all the repositories you need for your system.

```yaml
$ yum repolist all
```
Let's update your RHEL 7 system.

```yaml
$ yum update
```

Now, we need to change the system's hostname. If you have done it during your RHEL 7 installation, then this step is not necessary.

```yaml
$ echo hostname
$ nano /etc/hostname
```

Change the name to any name and save it. Just reboot the system to see the changes in your hostname.
We will now install an interesting application, this application can be used to view websites via the terminal. The view won't be appealing but can be used for basic needs. To install links, type the following command.

```yaml
$ yum install links
```

Now we will set up a local server in your system. To do that, we will have to install Apache server, PHP and MySQL. I am using PHP 5.6 because many of the functions that I used got deprecated after PHP 5.6 like mcrypt and many more. 
Let's install the Apache server.

```yaml
$ yum install httpd
```

Now, we have to open port in the firewall for the HTTPD in the server.

```yaml
$ firewall-cmd --add-service=http
$ firewall-cmd --permanent --add-port=80/tcp
$ firewall-cmd --reload
```

Now, we will restart and enable HTTPD service.

```yaml
$ systemctl restart httpd.service
$ systemctl start httpd.service
$ systemctl enable httpd.service
```

Now let's check if the server is up.

```yaml
$ links <your_ip_address>
```

If you see apache server page, then your server is up and running.
Now, we will enable indexing in the server.
```yaml
$ nano /etc/httpd/conf.d/welcome.conf
```

In the file, search for set -indexes and change it to set +indexes. If it is commented, then uncomment it by removing # from it.

Now we will restart apache to apply the changes.

```yaml
$ systemctl restart httpd
```

Now we will install PHP 5.6.

```yaml
$ yum search php
$ rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
$ rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
$ yum install -y php56w php56w-opcache php56w-xml php56w-mcrypt php56w-gd php56w-devel php56w-mysql php56w-intl php56w-mbstring
```

We will check, if PHP is working on our system or not.

```yaml
$ echo -e "<?php\nphpinfo();\n?>" >> /var/www/html/phpinfo.php
```

To check if the php file is working, just type:-

```yaml
$ links http://<ip_address>/phpinfo.php
```

Now, we will install mariaDB.

```yaml
$ yum install mariadb-server mariadb
```

Now, we will start mariaDB service.

```yaml
$ systemctl start mariadb.service
$ systemctl enable mariadb.service
```

To access the database via the terminal (I dont prefer phpmyadmin).

```yaml
$ mysql -u root -p
```

Now, lets install gcc (C++ compiler) in the system.

```yaml
$ yum install gcc
```
Now, let's install java.

```yaml
$ yum install java
```

Now, we will install Apache Tomcat.

```yaml
$ yum install tomcat
```

Now, let's start tomcat.

```yaml
$ systemctl start tomcat
$ systemctl enable tomcat.service
```

We have to open a port on our firewall. To do that:-

```yaml
$ firewall-cmd --zone=public --add-port=8080/tcp --permanent
$ firewall-cmd --reload
```

Now, let's install nmap. The nmap is an open-source security scanner.

```yaml
$ yum install nmap
```

To download files from the internet, we use wget. We will now install wget.

```yaml
$ yum install wget
```

To unzip files, we need unzip. To install unzip, do the following:-

```yaml
$ yum install unzip
```

Now, we will install an exploit and backdoor scanner called rootkit hunter.

```yaml
$ yum install rkhunter
```

To start the scanner, just type.

```yaml
$ rkhunter --check
```

When you have a server, you need to have a web panel. We will install a Webmin for satisfying that purpose.

```yaml
$ wget http://prdownloads.sourceforge.net/webadmin/webmin-1.740-1.noarch.rpm
$ rpm -ivh webmin-1.740-1.noarch.rpm
```

Now, we have to open the port for accessing it remotely via a web browser.

```yaml
$ firewall-cmd --zone=public --add-port=10000/tcp --permanent
$ firewall-cmd --reload
```