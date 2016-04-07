# Puppet Setup

> This is to set up a machine on Red Hat Enterprise Linux 7.1

## Preparation for Install

### Run these commands from the Terminal
``` sudo yum remove firewalld && sudo yum install iptables-services
  > This removes the default firewall

``` -A INPUT -p tcp -m state --state NEW -m tcp --dport 8140 --tcp-flags FIN,SYN,RST,ACK SYN -j ACCEPT

  > This allows Puppet Clients to Connect

``` sudo systemctl enable iptables && sudo systemctl start iptables && sudo iptables -L -n -v | grep 8140

 > This enables the Puppet rules in the firewall.

#### Main Puppet Configuration File
This is located at
  > /etc/puppet/puppet.conf
