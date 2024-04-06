INSTALL
=======

Download the script (or clone to `/etc/iptableco`)
(from now on, this is the working directory implied when a directory is not explicitely cited)

If you download to a different folder `$DIFOLDER`, run:

```
$DIFOLDER/rc.iptableco install
```

to create `/etc/iptableco` and a minimum `/etc/iptableco/iptables-main-up.rules`

-------------------------

Change directory to `cd /etc/iptableco` (from now on, consider this the working directory for the commands bellow), and
copy the template to create rules for your server "myserver" with:

```
$ cp iptableco-template.sh iptableco-myserver.sh
```

To facilitate, we will create an optional link:

```
$ ln -s /etc/iptableco/iptableco-myserver.sh /etc/iptableco/iptableco.sh
```

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
# Enabling rc.iptableco firewall script by drbeco version 20240406.094428
if [ -x /etc/rc.d/rc.iptableco ]; then
    echo "Enabling rc.iptableco firewall"
    /etc/rc.d/rc.iptableco start
fi
```


FIRST RUN
=========

0. `$ cd /etc/iptableco`
1. Edit `iptableco.sh` to your liking
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

This will create a backup file located at /etc/iptableco. If needed, use restore:

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
root# cd /etc/iptableco/
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

