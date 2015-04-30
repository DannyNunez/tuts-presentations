Installing HHVM on Ubuntu 14.04
===============================

sudo apt-get install nginx 

```
sudo apt-get install  mysql-server 
sudo mysql_install_db
sudo mysql_secure_installation
```


********************************************************************
* HHVM is installed.
* 
* Running PHP web scripts with HHVM is done by having your webserver talk to HHVM
* over FastCGI. Install nginx or Apache, and then:
* $ sudo /usr/share/hhvm/install_fastcgi.sh
* $ sudo /etc/init.d/hhvm restart
* (if using nginx)  $ sudo /etc/init.d/nginx restart
* (if using apache) $ sudo /etc/init.d/apache restart
* 
* Detailed FastCGI directions are online at:
* https://github.com/facebook/hhvm/wiki/FastCGI
* 
* If you're using HHVM to run web scripts, you probably want it to start at boot:
* $ sudo update-rc.d hhvm defaults
* 
* Running command-line scripts with HHVM requires no special setup:
* $ hhvm whatever.php
* 
* You can use HHVM for /usr/bin/php even if you have php-cli installed:
* $ sudo /usr/bin/update-alternatives --install /usr/bin/php php /usr/bin/hhvm 60