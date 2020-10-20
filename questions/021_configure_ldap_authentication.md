# Configure LDAP authentication

### Question:
Bind with LDAP located on **ldap.server.com**
* LDAP dn is **dc=server,dc=com**
* certificate file is located on **http://ldap.server.com/pub/EXAMPLE-CA-CERT**
* **ldapuserX** should be able to log into your system, where **X** is server domain number but will have none home
directory (configured in different question)
* all **LDAP** users have password **password** 

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* At the very beginning make sure You have **auth** related tools installed on the system, followed by **sssd**:

```
yum install -y auth* sssd sssd-client
```

* Usually I provide solutions with command line however with setting up LDAP it is a long list of commands. Given that 
during **RHCSA** exam You will be given GUI to work with - the easiest way is just to use graphical tool designed for 
LDAP config:

```
authconfig-gtk
```

and You just fill in the blanks (remember that LDAP server address needs **ldap://** prefix instead of **http://**).

* After configuring LDAP to connect to we have to make sure that services that are responsible for handling the communication with 
LDAP server. So we should enable and start **SSSD**:

```
systemctl enable SSSD
systemctl start SSSD
```


* When You set up everything just issue:

```
getent passwd USERNAME
```
and in the output You should be given information about the user.
