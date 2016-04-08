# ToDo List for Puppet

- ~~DNS on DC01 Forward and reverse DNS to find puppet @ 10.17 price check req from cgit~~
- ~~ip to to 10.17~~
- ~~let joakim know about the server~~
- ~~Open port 8140, between 10 , 30 and 40 nets  adjusted to reflect ip update~~
- ~~# IP is now 10.18  pointer also to be moved.~~
- -
Port	Use
~~8140~~
~~The Puppet master uses this port to accept inbound traffic/requests from Puppet agents.~~
~~The PE console sends request to the Puppet master on this port.~~
~~Certificate requests are passed over this port unless ca_port is set differently.~~
~~Classifier group: “PE Master”~~
~~443~~
~~This port provides host access to the PE console.~~
~~The PE Console accepts HTTPS traffic from end-users on this port.~~
~~Classifier group: “PE Console”~~
~~61613~~
~~MCollective uses this port to accept inbound traffic/requests from Puppet agents.~~
~~Any host used to invoke commands must be able to reach MCollective on this port.~~
~~Classifier group: “PE ActiveMQ Broker”~~
~~8142~~
~~Orchestration services and the Run Puppet button use this port to accept inbound~~ ~~traffic/responses from Puppet agents.~~
~~Classifier group: “PE Orchestrator”~~
