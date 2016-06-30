#### pklinuxnetcok
#####Chapter 1. Configuring a Router
######Setting up the physical network
```
ip link set dev eth0 up
ip link show eth0
```
######Congigure ipv4
```
ip addr add dev eth0 10.0.0.1/24
ip addr list eth0
```
######configure ipv4 permanently
in centos, from original
```
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
TYPE=Ethernet
USERCTL=yes
PEERDNS=yes
IPV6INIT=no
PERSISTENT_DHCLIENT=yes
RES_OPTIONS="timeout:2 attempts:5"
DHCP_ARP_CHECK=no
```
to
```
DEVICE=eth0
BOOTPROTO=none
ONBOOT=yes
NETWORK=10.0.0.0
NETMASK=255.255.255.0
IPADDR=10.0.0.1
USERCTL=no
```
then
```
ifup eth0
```
######Connecting two networks
```
```


#####Chapter 5. Web Servers
######Configuring Apache with TLS
ubuntu
```
sudo a2enmod ssl
sudo a2ensite default-ssl
```
file: (private key and public)
```
/etc/ssl/private
/etc/ssl/certs
```
edit relevant file
```
/etc/apache2/sites-enabled/default-ssl.conf
```
centos
```
yum install httpd mod_ssl
```
file: (private key and public)
```
/etc/pki/tls/private
/etc/pki/tls/certs
```
edit relevant file
```
/etc/httpd/conf.d/ssl.conf
```

#####Chapter 10. Monitoring Your Network
######Installing Nagios
```
apt-get update && apt-get install nagios3
```
Adding Nagios users
```
htpasswd /etc/nagios3/htpasswd.users user
```
then
```
vim /etc/nagios3/conf.d/contacts_nagios2.cfg
```
(failed to add users)
######Adding Nagios hosts
```
vim /etc/nagios3/conf.d/host.cfg
```
