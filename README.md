How to use IPTABLECO
====================

------------------------
0. backup old rules

root# /etc/rc.d/rc.iptableco save

------------------------
1. generate new rules with your changes

root# cd ~/iptables/
root# vi ./iptableco.sh     ### adjust new rules
root# ./iptableclo.sh -s    ### save rules in a iptables compatible file

------------------------
2. apply the adjustment to IPV4 and IPV6

root# /etc/rc.d/rc.iptableco adjust 20240325151640-iptables-main-up.rules 20240325151640-iptables-aux-up.rules

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
* Last update: 2024-03-25

