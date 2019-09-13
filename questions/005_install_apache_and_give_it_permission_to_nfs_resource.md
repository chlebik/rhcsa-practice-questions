# Install Apache and allow it to get documents from NFS mounted folder 

### Question:
Install Apache and allow it to get documents from NFS mounted folder (**SELinux** part)

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* First step is to install **Apache** using **YUM**. It does not require special treatment - just type the command ***yum install -y httpd***
* Always when installing service/software which interacts with network **it is crucial** to keep in mind configuring firewall to enable incoming
connections for this service. Therefore the commands used:

```
# notice the '-permament' option (in order to save rule to survive during reboots)
firewall-cmd –permanent –add-service=http
firewall-cmd –reload
```

* Besides firewall configuration for network-interacting services for all services being installed in the system remember to enable it (to autostart after reboot)
and also starting it up right after the installation (services usually does not autostart as a part of installation process):

```
systemctl enable httpd
systemctl start httpd
```

* **SELinux** at the end of the exam should be enabled and set to **enforcing** mode. Therefore always pay attention to this aspect of system
configuration. The usual problem for using **SELinux** is to find out what **rule** should be used. In order to simplify that a concept of
**boolean settings** is a part of **SELinux**. Below commands are listing all of them, grepping in search for ***nfs*** (that we are interested in), then
grepping again only for ***httpd*** service. At the end we just enable proper boolean setting (notice ***-P*** flag to make it persistent).
 

```
getsebool -a | grep nfs | grep httpd
setsebool -P httpd_use_nfs on
```


### Additional comment:

**Apache** knowledge is not in the requirements for the exam. However it is very popular server and also serves additional purposes here - 
it gives an opportunity to use **yum**, configure **firewall** with **systemd service** and finally configure **SELinux**.
<br />
