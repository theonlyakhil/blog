---
title:  "Setup Localhost in MacOS"
search: true
categories:
  - Linux 
  - MacOS
last_modified_at: 2018-10-11T08:05:34-05:00
header:
  teaser: /assets/images/blog/localhost-on-mac.jpg
---

![WoLAN](/assets/images/blog/localhost-on-mac.jpg)

I first started developing commerial products using HTML, CSS, Javascript and many more languages that were used to code client-side of a web application. I first encountered server-side languages while having a technical conversation with one of my seniors. This conversation motivated to learn PHP. While surfing the internet, I found we couldn't execute server-side languages like client-side. That is, I couldn't see the output just by executing the code via a browser. To execute server-side languages like PHP, I had to establish a server inside my mac.

The following are the steps I used to setup a localhost on my mac.
On mac, we dont have to install a server, it's already pre-installed. We just have to enable it.

```yaml
   $ sudo apachectl start
```

To check whether the server is not running or not, go to http://localhost on the mac's browser.
PHP is also preinstalled on mac, we just have to enable it.
First, we have to edit the server's config file.

```yaml
   $ sudo nano /etc/apache2/httpd.conf
```

Now, we will search for PHP in this file using ctrl+w
Remove # from the below line.

```yaml
   LoadModule php7_module libexec/apache2/libphp7.so
```

Restart apache server

```yaml
   $ sudo apachectl restart
```

We have a create a folder named "Sites" on the home directory.

```yaml
   $ sudo mkdir /Users/<--your_username-->/Sites
```

Lets save a file named index.php with the following contents.

```yaml
   <?php echo "Hello From Sites Folder!”; phpinfo();?> 
```

We have to add the Sites fold on the config file. Edit the file using the following command.

```yaml
   $ sudo nano /etc/apache2/httpd.conf
```

Inside the file, search for the word "library" using ctrl+w.
Replace /Library/WebServer/Documents with /Users/<--your_username-->/Sites
Now, we need a database and a DBMS for the localhost. Lets download mysql for mac.
First we will download MySQL from [this link](https://dev.mysql.com/downloads/mysql/).
Install MySQL from dmg file.
Now, we will configure MqSQL by opening MySQL from system preferences. Add a password and click legacy password. After this step, just click "start MySQL server".
You can use sql through bash by executing the following command.

```yaml
   $ /usr/local/mysql/bin/mysql -u root -p
```

Or you can use Sequel pro. Sequel pro is an application that can be used to any database remotely. That is, it can be used to connect to localhost and anyother server established on the network.
Now, we will make the server communication encrypted. That is, we will enable SSL/HTTPS on localhost. Execute the following command to edit the config file.

```yaml
   $ sudo nano /etc/apache2/httpd.conf
```

Search for socache_shmcb_module using ctrl+w.
Remove # from the following lines.

```yaml
   socache_shmcb_module libexec/apache2/mod_socache_shmcb.so
```

serach for LoadModule ssl_module libexec/apache2/mod_ssl.so and remove # from it.

```yaml
   LoadModule ssl_module libexec/apache2/mod_ssl.so
```

Delete # from Include /private/etc/apache2/extra/httpd-ssl.conf

```yaml
   /private/etc/apache2/extra/httpd-ssl.conf
```

We have to replace www.example.com:443 with localhost from the below file.

```yaml
   $ sudo nano /etc/apache2/extra/httpd-ssl.conf
```

Replace Library/WebServer/Documents. Replace that with /Users/<--your_username-->/Sites
Add the following lines below <VirtualHost_default_:443>

```yaml
   <Directory "/Users/<--your_username-->/Sites"> 
    Options All 
    MultiviewsMatch Any 
    AllowOverride All 
    Require all granted 
   </Directory>
```

Open the following config file.

```yaml
   $ sudo nano /etc/ssl/openssl.cnf
```

Add the following lines at the end.

```yaml
   [ san ] 
   subjectAltName                  = DNS:localhost
```

Now we generate a key using openSSL.

```yaml
   $ sudo openssl req -extensions san -config /etc/ssl/openssl.cnf -x509 -nodes -newkey rsa:4096 -keyout /private/etc/apache2/server.key -out /private/etc/apache2/server.crt -days 365 -subj "/C=your_country/ST=your_state/L=your_city/O=hostname/CN=localhost"
```

Now we will add the certificate using the following command.

```yaml
   $ sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain /private/etc/apache2/server.crt
```

Now just restart the apache server.

```yaml
   $ sudo apachectl restart
```

We have not successfully established a server inside Mac.