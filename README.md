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
#####Chapter 4. Remote Access
######Installing OpenSSH
```
apt-get install ssh
apt-get install openssh-server //centos
```
######Using OpenVPN
```
apt-get install openvpn
openvpn --genkey --secret /etc/openvpn/static.key
vim /usr/share/doc/openvpn/examples/sample-config-files/client.conf
```
edit
```
remote wanaddress
proto udp
dev tun
secret /path/to/static.key
ifconfig 10.8.0.2 10.8.0.1
route 192.168.1.0 255.255.255.0
comp-lzo
verb 3
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
#####Chapter 6. Directory Services
######Configuring Samba as an Active Directory
```
apt-get install ntp samba smbclient
bash -c 'echo "manual" > /etc/init/nmbd.override'
bash –c 'echo "manual" > /etc/init/smbd.override'
```
then
```
rm /etc/samba/smb.conf
samba-tool domain provision --realm ad.example.org --domain example --use-rfc2307 --option="interfaces=lo eth1" --option="bind interfaces only=yes" --dns-backend BIND9_DLZ
```


#####Chapter 8. Setting up E-mail
######Configuring Postfix to send and receive e-mail
```
apt-get install postfix mailutils
vim /etc/postfix/main.cf
```
edit
```
mydomain = domain.com
mydestination = $mydomain $myhostname
mynetworks = 127.0.0.0/8
```
then
```
postfix reload
```

######






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
