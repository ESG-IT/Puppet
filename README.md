# Puppet Setup on OS X
Download Latest Puppet from [here](https://downloads.puppetlabs.com/mac/)

Download Latest Factor from [here](https://downloads.puppetlabs.com/mac/)

# Puppet Setup on Server
[Link to guide for The Foreman](http://theforeman.org/manuals/1.11/quickstart_guide.html)
> This is to set up a machine on CentOS 7, Foreman sets up Puppet.

## Set the time to NTP
    sudo yum install -y ntp && grep ^server /etc/ntp.conf && sudo systemctl enable ntpd && sudo systemctl start ntpd && ntpq -p

## Change firewall to allow Puppet connections

- Remove the old firewall and set up IPTables

    sudo yum remove -y firewalld && sudo yum install -y iptables-services

- Open iptables configuration
    sudo nano /etc/sysconfig/iptables

- Allow puppet in IPTables, write under the second entry

    -A INPUT -p tcp -m state --state NEW -m tcp --dport 8140 --tcp-flags FIN,SYN,RST,ACK SYN -j ACCEPT

- Press CTRL + X and then Y to save

- Enable the settings

    sudo systemctl enable iptables && sudo systemctl start iptables && sudo iptables -L -n -v | grep 8140

## Install The Foreman
- Enable the repo:

    rpm -ivh http://yum.puppetlabs.com/puppetlabs-release-el-7.noarch.rpm


- Install extra repo

    sudo yum -y install epel-release http://yum.theforeman.org/releases/1.11/el7/x86_64/foreman-release.rpm


- Install the Foreman

    sudo yum -y install foreman-installer


- Run The Foreman installer

    sudo foreman-installer -i


- Reboot machine
