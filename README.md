##############################################################################
manual way:
##############################################################################
0. backup               $ cp iptables-2018-hydra-gera-rules.sh iptables-2020-hydra-gera-rules.sh
1. new rules            $ ./iptables-2020-hydra-gera-rules.sh > /etc/iptables.active-2020-09-20-up.rules
2. Copiar para /etc     $ mv /etc/iptables.up.rules /etc/iptables5.rules # numero crescente
                        $ cp /etc/iptables.active-2020-09-20-up.rules /etc/iptables.up.rules
3. reiniciar firewall   $/etc/init.d/iptables.sh restart

##############################################################################
automatic way
##############################################################################
------------------------
0. backup old rules

root# /etc/rc.d/rc.iptableco save
------------------------
1. gerar

root# cd ~/iptables/
root# vi ./iptableco.sh     ### ajustar regras
root# ./iptableclo.sh -s    ### save rules in a iptables compatible file
------------------------
2. aplicar, restaurar IPV4 e IPV6

root# /etc/rc.d/rc.iptableco restore 20210717235731-iptables.up.rules
------------------------
3. testar
        - invalid
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


