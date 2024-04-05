INSTALL
=======

Download the script (or clone) to `/root/iptableco`
(from now on, this is the working directory implied when a directory is not explicitely cited)

Copy the template to create rules for your server "myserver" with:

```
$ cp iptableco-template.sh iptableco-myserver.sh
```

To facilitate, we will create an optional link:

```
$ ln -s /root/iptableco/iptableco-myserver.sh /root/iptableco/iptableco.sh
```

(from now on, we will refer only to script iptableco.sh)

Copy the script rc.iptableco to the rc.d folder (This is for Slackware. See your distro if this changes)

```
$ cp rc.iptableco /etc/rc.d/
```

Make it executable

```
$ chmod +x /etc/rc.d/rc.iptableco
```

Add a call in your /etc/rc.d/rc.local (Again, Slackware. Check your distro on how to start services on boot). Edit the file and add:

```
# Enabling rc.iptableco firewall script by drbeco version 20240404.005802
if [ -x /etc/rc.d/rc.iptableco ]; then
    echo "Enabling rc.iptableco firewall"
    /etc/rc.d/rc.iptableco start
fi
```

Create a folder for your rules at:

```
$ mkdir /etc/iptables
```


FIRST RUN
=========

1. Edit iptableco.sh to your liking
2. Run it to see the results

```
   $ ./iptableco.sh
```

3. If no errors and everything as you want, save the restore files with:

```
   $ ./iptableco.sh -s
```

This will save two files:
* $thedate-iptables-main-up.rules and
* $thedate-iptables-add-up.rules

4. Start the first file with:

```
  $ /etc/rc.d/rc.iptableco restore $thedate-iptables-main-up.rules
```

If needed, start any services that messes iptables up. Then you can add new rules with:

```
  $ /etc/rc.d/rc.iptableco add $thedate-iptables-add-up.rules # optional
```

5. Create your first backup with:

```
  $ /etc/rc.d/rc.iptableco backup
```

This will create a backup file located at /etc/iptables. If needed, use restore:

```
  $ /etc/rc.d/rc.iptableco restore $thedate-iptables-bkp-up.rules
```


How to use IPTABLECO to update rules
====================================

------------------------
0. backup old rules

```
root# /etc/rc.d/rc.iptableco backup
```

------------------------
1. generate new rules with your changes

```
root# cd ~/iptables/
root# vi ./iptableco.sh     ### add new rules
root# ./iptableclo.sh -s    ### save rules in a iptables compatible file
```

------------------------
2. apply the changes to IPV4 and IPV6

```
root# /etc/rc.d/rc.iptableco restore 20240325151640-iptables-main-up.rules
```

If needed, start any services that messes iptables up. Then you can add new rules with:

```
root# /etc/rc.d/rc.iptableco add 20240325151640-iptables-add-up.rules
```

------------------------
3. Check if all good. Order:

        - invalid rules
        - localhost     lo
        - ping          icmp
        - ssh           22
        - dns           53
        - https         443
        - http          80
        - ftp           21
        - ntp           123
        - smtp          25, 465, 587
        - gopher        70
        - rsync         873
        - dropbox       17500
        ---------------------
        - docker rules to append

------------------------

Copyright and Author
====================


* License: GNU/GPL v2.0
* rc.iptableco (C) 2016-present
* Author: Prof. Dr. Ruben Carlo Benante
* Contact email: rcb at beco.cc
* Cretion: 2016-05-26
* Last update: 2024-04-04

