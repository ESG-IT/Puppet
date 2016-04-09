# Puppet Setup
[Link to guide for Puppet 4.4](https://docs.puppet.com/puppet/4.4/reference/)
> This is to set up a machine on Red Hat Enterprise Linux 7.1

## Set the time to NTP
    sudo yum install -y ntp && grep ^server /etc/ntp.conf && sudo systemctl enable ntpd && sudo systemctl start ntpd && ntpq -p

## Change firewall to allow Puppet connections

- Remove the old firewall and set up IPTables

    sudo yum remove -y firewalld && sudo yum install -y iptables-services

- Open iptables configuration
    sudo nano /etc/sysconfig/iptables

- Allow puppet in IPTables, write at the bottom before COMMIT

    -A INPUT -p tcp -m state --state NEW -m tcp --dport 8140 --tcp-flags FIN,SYN,RST,ACK SYN -j ACCEPT

- Press CTRL + X and then Y to save

- Enable the settings

    sudo systemctl enable iptables && sudo systemctl start iptables && sudo iptables -L -n -v | grep 8140

## Install Puppet Server
- Enable the repo:

    sudo rpm -Uvh https://yum.puppetlabs.com/puppetlabs-release-pc1-el-7.noarch.rpm

- Install Puppetserver

    yum install -y puppetserver

- Start Puppetserver at boot

    sudo systemctl enable puppetserver

- Reboot machine

## Install PuppetDB

- In the terminal Type

    sudo yum install -y puppetdb puppetdb-termini










# Old

## Preparation for Install
[Link to guide](https://elatov.github.io/2014/08/setting-up-puppet-master-on-centos-7/)


### Run these commands from the Terminal

- Remove the old firewall and set up IPTables

    sudo yum remove firewalld && sudo yum install iptables-services


- Open iptables configuration
    sudo nano /etc/sysconfig/iptables

  - Allow puppet in IPTables, write at the bottom
    -A INPUT -p tcp -m state --state NEW -m tcp --dport 8140 --tcp-flags FIN,SYN,RST,ACK SYN -j ACCEPT




This allows Puppet Clients to Connect

    sudo systemctl enable iptables && sudo systemctl start iptables && sudo iptables -L -n -v | grep 8140

This enables the Puppet rules in the firewall.

    sudo nano /etc/hostname
Change the hostname to puppet if not already, CTRL + X saves

    sudo yum install -y ntp && grep ^server /etc/ntp.conf && sudo systemctl enable ntpd && sudo systemctl start ntpd && ntpq -p

This installs the time management and starts it.

### Main Puppet install

    sudo rpm -ivh sudo rpm -Uvh https://yum.puppetlabs.com/puppetlabs-release-pc1-el-7.noarch.rpm && sudo yum install -y puppet-server

Get the repository for Puppet and install

### Post-install Setup
[Link to guide](https://docs.puppet.com/puppet/3.8/reference/post_install.html#configure-a-puppet-master-server)

### Run these commands from the Terminal

Open the Puppet Configuration File

    sudo nano /etc/puppet/puppet.conf

In the [main] section, copy the follwing at the bottom

    dns_alt_names = puppet,puppet.esg.lan

    Type CTRL + X

These are the names that the puppet clients will look for with DNS.

Set up Certificates

    sudo puppet master --verbose --no-daemonize

Press CTRL + C when it shows:

    Notice: Starting Puppet master version 3.8.6



#### Main Puppet Configuration File
This is located at:
    /etc/puppet/puppet.conf
