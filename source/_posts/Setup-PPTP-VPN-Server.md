title: Setup PPTP VPN Server on Ubuntu
date: 2014-12-09 17:26:36
categories: Programming
tags:
---
Successfully setup a PPTP VPN Server on Ubuntu, following the instructions [here](http://jesin.tk/setup-pptp-vpn-server-debian-ubuntu/).
<!--more-->
All went smoothly. Just one thing to be noticed that don't install OpenVPN and PPTP VPN on the same host. I did that and neither of them work. Guess there might be some kind of confliction.

And for my first impression, PPTP VPN appears easier to use than OpenVPN. Although OpenVPN provides a web page to setup the configuration in graphical UI, but that's probably becuase there's too much configurations to set. And PPTP just needs several lines of command to setup everything.

The general process as below.
## Installation ##
``` sh
apt-get install pptpd -y
update-rc.d pptpd defaults
```
##Configuration##
``` sh
vim /etc/pptpd.conf
localip 172.20.1.1
remoteip 172.20.1.2-254

vim /etc/ppp/pptpd-options
ms-dns 8.8.8.8
ms-dns 8.8.4.4

vim /etc/ppp/chap-secrets
username * password *
```
##Start Service##
``` sh
service pptpd restart
```
##Forwording##
``` sh
vim /etc/sysctl.conf
net.ipv4.ip_forward=1

sysctl -p

iptables -I INPUT -p tcp --dport 1723 -m state --state NEW -j ACCEPT
iptables -I INPUT -p gre -j ACCEPT
iptables -t nat -I POSTROUTING -o eth0 -j MASQUERADE
iptables -I FORWARD -p tcp --tcp-flags SYN,RST SYN -s 172.20.1.0/24 -j TCPMSS  --clamp-mss-to-pmtu

iptables -L
iptables-save > /etc/iptables.rules
```

