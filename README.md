# Puppet Setup

> This is to set up a machine on Red Hat Enterprise Linux 7.1

## Preparation for Install
[Link to guide](https://elatov.github.io/2014/08/setting-up-puppet-master-on-centos-7/)


### Run these commands from the Terminal
    sudo yum remove firewalld && sudo yum install iptables-services
This removes the default firewall

    -A INPUT -p tcp -m state --state NEW -m tcp --dport 8140 --tcp-flags FIN,SYN,RST,ACK SYN -j ACCEPT

This allows Puppet Clients to Connect

    sudo systemctl enable iptables && sudo systemctl start iptables && sudo iptables -L -n -v | grep 8140

This enables the Puppet rules in the firewall.

    sudo nano /etc/hostname
Change the hostname to puppet if not already, CTRL + X saves

    sudo yum install -y ntp && grep ^server /etc/ntp.conf && sudo systemctl enable ntpd && sudo systemctl start ntpd && ntpq -p

This installs the time management and starts it.

### Main Puppet install

    sudo rpm -ivh http://yum.puppetlabs.com/puppetlabs-release-el-7.noarch.rpm && sudo yum install -y puppet-server

Get the repository for Puppet and install

### Post-install Setup
[Link to guide](https://docs.puppet.com/puppet/3.8/reference/post_install.html#configure-a-puppet-master-server)

### Run these commands from the Terminal

    sudo nano /etc/puppet/puppet.conf

Open the Puppet Configuration File

In the [main] section, copy the follwing at the bottom

    dns_alt_names = puppet,puppet.esg.lan

These are the names that the puppet clients will look for with DNS. 


#### Main Puppet Configuration File
This is located at:
    /etc/puppet/puppet.conf
