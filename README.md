router-config
=============

Secure router configuration for a dedicated Ubuntu 14.04 server running btrfs as its primary file system with a public facing NIC at eth0 and an internal facing NIC at eth1.

The purpose of this configuration is to provide a secure router that provides several advanced features such as
  1. Listening on any number of WAN addresses
  2. Providing tarpit protection to all incoming ports
  3. Allow outbound traffic for a host to appear to come from a specific WAN address
  4. Provide port forwarding
  5. Provide routing/NAT
  6. Provide DHCP/DNS services

The primary use case for this configuration is a collection of VMs which need to host publically facing services where there are fewer public IP addresses than VMs.

Another use case is having more public IP addresses than VMs and wanting to obscure where critical services are by making it discouraging for an attacker to enumerate your network.

In addition to configuring the server as specified by the configuration files in this directory, you will have to install a number of packages

```sh
# Install SSH server
apt-get install -f -y ssh
ssh-keygen -b 4096 -t rsa -f /etc/ssh/ssh_host_rsa_key
ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key
# Install NTP server
apt-get install -f -y ntp
# Install DNS server
apt-get install -f -y bind9 bind9utils 
rndc-confgen -a -b 512
# Install DHCP server
apt-get install -f -y isc-dhcp-server
# Install iptables management
apt-get install -f -y firehol
apt-get install -f -y xtables-addons-common xtables-addons-dkms
```
