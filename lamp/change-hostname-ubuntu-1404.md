How to Change Hostname (Computer Name) in Ubuntu 14.04 
======================================================

1. Edit the /etc/hostname file. Enter the new name you want for your server. 

```
sudo vi /etc/hostname
```

```

  1 new-hostname

```

2. Edit the /etc/hosts file. Replace all reference to the old hostname with your new hostname. 

```

sudo vi /etc/hosts

```

```
127.0.0.1 localhost
127.0.0.1 new-hostname
11.111.111.111  new-hostname

```

3. Reboot the server 

```

sudo reboot 

```