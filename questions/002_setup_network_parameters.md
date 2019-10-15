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

* Issue following command (as one liner) to set connection data (we assume type is ethernet connection as used interface is called ***eth0***):
 
```
nmcli conn add conn-name MY_CONNECTION ifname eth0 type ethernet
ip4 SOME.IP.TO.BE.USED/mask
gw4 SOME.GATEWAY.TO.BE.USED
```
 
* that command adds connection for specific interface - however we still need to add DNS resolving. Notice [+] in the command - if
used with + sign provided DNS will be added to the list of DNS being used. If we omit + sign the whole list will be replaced by 
provided value:

```
nmcli conn modify MY_CONNECTION [+]ipv4.dns SOME.DNS.TO.BE.USED  
nmcli conn mod MY_CONNECTION ipv4.ignore-auto-dns yes       # to disable DHCP DNS
```

* at the final stage it is wise to start this connection:

```
nmcli conn show --active      # to check if the connection is not up 
nmcli conn up MY_CONNECTION
nmcli conn show --active      # to check if the connection is up
```



### Additional comment:

It is possible to edit existing connection using **nmtui** tool which can be easier. 
Also when using GUI there is also graphical interface for it.
