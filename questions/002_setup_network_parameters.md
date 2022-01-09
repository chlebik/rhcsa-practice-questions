# Setup network parameters
### Question:
Please create new network connection using provided values:
IP:           some.ip.to.be.used/mask
Gateway:      some.gateway.to.be.used
DNS server:   some.dns.to.be.used
Interface:    eth0
***
(scroll down for an answer)
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* We use the network manager CLI (nmcli) to perform this action.
* Issue following command (as one liner) to set the new connection data (we assume type is ethernet connection as used interface is called ***eth0***):

```
nmcli conn add con-name MY_CONNECTION ifname eth0 type ethernet
ip4.addresses SOME.IP.TO.BE.USED/mask
ipv4.gateway SOME.GATEWAY.TO.BE.USED
ipv4.dns SOME.DNS.TO.BE.USED  
```

* That command creates a new connection for a specific interface - However, if we want to modify an exisiting connection issue the following command.

*Note: Notice [+] in the command - if used with + sign provided DNS will be added to the list of DNS being used. If we omit + sign the whole list will be replaced by 
provided value.*

```
nmcli con modify MY_CONNECTION [+]ipv4.dns SOME.DNS.TO.BE.USED  
nmcli con mod MY_CONNECTION ipv4.ignore-auto-dns yes       # to disable DHCP DNS
```

* At the final stage it is wise to start this connection:

```
nmcli con show --active      # to check if the connection is not up 
nmcli con up MY_CONNECTION
nmcli con show --active      # to check if the connection is up
```

* If asked to automatically start the new connection on system reboot:

```
nmcli con mod OLD_ACTIVE_CONNECTION connection.autoconnect no     # disable the old connection from starting on reboot 
nmcli con up MY_CONNECTION connection.autoconnect yes # automatically switch to new connection on reboot 
```
  
### Additional comment:
It is possible to edit existing connection using **nmtui** tool which can be easier. 
Also when using GUI there is also graphical interface for it.
