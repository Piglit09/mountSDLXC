# Mount Shared Drives Script 

Made this script to mount shared drives in multiple LXC's in Proxmox instead of typing all the commands multiple times

# NOTE

This will only work in privileged LXC's

IT IS NO RECOMENDED TO EXPOSE PRIVLAGED LXC'S TO THE INTERNET 

# Create script file 
```ruby
Nano /etc/mount.sh
```
this will create a new empty file named <code>mount.sh</code>

# Script Code

change the following in the code:

<code> [share name] </code> to your share folder or drive

<code> [username] </code> and <code> [password] </code> to an admin level account on host machine

<code> [ip address] </code> to host ip address 

to find ip address run <code> ipconfig </code> for windows or <code> ip add </code> for linux 


```ruby
#!/usr/bin/env bash

apt update
apt upgrade -y
apt-get install -y cifs-utils

mkdir /mnt/[share name]
mkdir /mnt/[share name]
mkdir /mnt/[share name]

echo "username=[username]
password=[password]" >/etc/cifs-credentials

chmod 600 /etc/cifs-credentials

echo "//[ip address]/[share name] /mnt/[share name] cifs credentials=/etc/cifs-credentials 0 0
//[ip address]/[share name] /mnt/[share name] cifs credentials=/etc/cifs-credentials 0 0
//[ip address]/[share name] /mnt/[share name] cifs credentials=/etc/cifs-credentials 0 0" >/etc/fstab

systemctl daemon-reload

 mount -a
```

copy updated code to <code>mount.sh</code>
 
# Change file perms 
```ruby
chmod +x /etc/mount.sh
```
# Run script 
```ruby
/etc/mount.sh
```

# Final thoughts

Alternitivly you could just copy each line into terminal one by one making the needed changes

These commands also work in Ubuntu or any debian linux distro


# Issues
 
 In proxmox if you run into  <code> mount error(1): Operation not permitted </code> you are running an unprivileged container

