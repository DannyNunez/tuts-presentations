Create a Ubuntu 14.04 Server on your favorite Could Hosting Provider 
====================================================================

1. ssh into the server as root with the password provided. 
2. cd into usr/locl/bin and create a file called *devadd*
3. Enter the following code into the file. 

```
#!/bin/bash

USER="$1"
KEY="$2"

if [ $# -ne 2 ]
then
        echo "Usage: $0 {user} {key}"
        exit 1
fi

if [ "$(getent passwd $1)" ]
then
        echo "User already exists"
        exit 1
fi

useradd -d /home/"$USER" -s /bin/bash -m "$USER"
mkdir /home/"$USER"/.ssh
echo "$KEY" > /home/"$USER"/.ssh/authorized_keys
chmod 600 /home/"$USER"/.ssh/authorized_keys
chown -R "$USER":"$USER" /home/"$USER"/.ssh
usermod -a -G www-data "$USER"
echo "$USER ALL = NOPASSWD : ALL" >> /etc/sudoers
echo "umask 002" >> /home/"$USER"/.bashrc
```

4. Add Executable permissions for the file:

```
chmod +x devadd
```

5. Add new users with ssh keys with the following command.

```
/usr/local/bin/devadd username "ssh-rsa [ssh public key] username" 
```

6. Disable root login. Edit the /etc/ssh/sshd_config file. 

```
 26 # Authentication:
 27 LoginGraceTime 120 
 28 PermitRootLogin no # change this line to no to disable root login
 29 StrictModes yes
```

7. Disable password login. Edit the /etc/ssh/sshd_config file. 

```
 51 # Change to no to disable tunnelled clear text passwords
 52 PasswordAuthentication no
```

8. restart sshd 
```
service ssh restart
```
9. Logout and test if you can login as root. If you can't great.

```
Permission denied (publickey). # this should be returned when trying to ssh in as root
```

10. Try logging in as a user using a password. If you can't great. 


Install LAMP SERVER
===================

1. shh into the server as the new user you created and enter the commands below.

```
sudo apt-get update
sudo apt-get install -y vim
sudo apt-get install -y build-essential
sudo apt-get install -y python-software-properties
sudo apt-get install -y apache2
sudo apt-get install -y libapache2-mod-php5
sudo apt-get install  php5 php5-curl php5-gd php5-mcrypt php5-cli php5-common php5-json php-pear php5-dev php5-xdebug -y
sudo php5enmod json
sudo php5enmod mcrypt
sudo apt-get install  mysql-server php5-mysql -y
```

Set the 'ServerName' directive globally
========================================

Edit /etc/apache2/apache2.conf add "ServerName localhost" to the end of the file.


Secure the Mysql Server
=======================
```
sudo apt-get install  mysql-server 
sudo mysql_install_db
sudo mysql_secure_installation
```

Follow the prompts

1. Enter your root password created when you installed mysql-server

```
    Enter current password for root (enter for none): 
    OK, successfully used password, moving on...
```

2. Do not change your root password. Enter n on the prompt. 

```
You already have a root password set, so you can safely answer 'n'.
Change the root password? [Y/n] n
```

3. Remove Anonymous user. Enter Y at the prompt. 

```
Remove anonymous users? [Y/n] Y
 ... Success!
```

4. Disallow root login. Enter Y at the prompt.

```
Disallow root login remotely? [Y/n] Y
 ... Success!
```
5. Remote the test database. Enter Y at the prompt. 

```
Remove test database and access to it? [Y/n] Y
 ... Success!
```
6. Reload the privileges table. Enter Y at the prompt. 
```
Reload privilege tables now? [Y/n] Y
 ... Success!
```
Secure Apache2
==============

Change ServerTokens to prod. Edit /etc/apache2/conf.d/security

```
 18 #
 19 # ServerTokens
 20 # This directive configures what you return as the Server HTTP response
 21 # Header. The default is 'Full' which sends information about the OS-Type
 22 # and compiled in modules.
 23 # Set to one of:  Full | OS | Minimal | Minor | Major | Prod
 24 # where Full conveys the most information, and Prod the least.
 25 #
 26 #ServerTokens Minimal
 27 #ServerTokens OS
 28 #ServerTokens Full
 29 ServerTokens Prod
```


Turn the server signature off. Edit /etc/apache2/conf.d/security

```
 31 #
 32 # Optionally add a line containing the server version and virtual host
 33 # name to server-generated pages (internal error documents, FTP directory
 34 # listings, mod_status and mod_info output etc., but not CGI generated
 35 # documents or custom error documents).
 36 # Set to "EMail" to also include a mailto: link to the ServerAdmin.
 37 # Set to one of:  On | Off | EMail
 38 #
 39 ServerSignature Off
 40 #ServerSignature On
```

PHP.INI changes for Security
============================

Edit the /etc/php5/apache2/php.ini file. 

```
sudo vim /etc/php5/apache2/php.ini
```

Turn expose php off. Edit /etc/php5/apache2/php.ini

```
 363 ; Decides whether PHP may expose the fact that it is installed on the server
 364 ; (e.g. by adding its signature to the Web server header).  It is no security
 365 ; threat in any way, but it makes it possible to determine whether you use PHP
 366 ; on your server or not.
 367 ; http://php.net/expose-php
 368 expose_php = off
```

If you want php errors to displagt during development turn display_errors to On. Edit 

```
 456 ; This directive controls whether or not and where PHP will output errors,
 457 ; notices and warnings too. Error output is very useful during development, but
 458 ; it could be very dangerous in production environments. Depending on the code
 459 ; which is triggering the error, sensitive information could potentially leak
 460 ; out of your application such as database usernames and passwords or worse.
 461 ; It's recommended that errors be logged on production servers rather than
 462 ; having the errors sent to STDOUT.
 463 ; Possible Values:
 464 ;   Off = Do not display any errors
 465 ;   stderr = Display errors to STDERR (affects only CGI/CLI binaries!)
 466 ;   On or stdout = Display errors to STDOUT
 467 ; Default Value: On
 468 ; Development Value: On
 469 ; Production Value: Off
 470 ; http://php.net/display-errors
 471 display_errors = Off
 ```
 
Increase the file upload size. 

```
 791 ; Maximum allowed size for uploaded files.
 792 ; http://php.net/upload-max-filesize
 793 upload_max_filesize = 8M
```


Enable mod-rewrite and restart the apache server.
========================================

```
sudo a2enmod rewrite
sudo service apache2 restart
```

Install git
===================


```
sudo apt-get install -y git-core
sudo git config --global user.name "YOUR NAME"
git config --global user.email "YOUR EMAIL ADDRESS"

```

Set up your SSH Keys
====================

https://help.github.com/articles/generating-ssh-keys/


Set up permissions for Apache
=============================

```
sudo chown -R www-data:www-data /var/www
sudo chmod -R g+rw /var/www
```


Add your user to the www-data group
==================================

```
sudo usermod -g www-data [user name goes here]
```