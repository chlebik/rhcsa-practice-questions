# Configure autofs

Question is related to question **21**.

### Question:
Configure **autofs** to automount the home directories of LDAP users.
* classroom.example.com (172.25.254.254) NFS-exports **/home/guests** to your system, whereX is Your server number
* LDAP userX home directory is **classroom.example.com:/home/guests/ldapuserX**
* **ldapuserX** home directory should be automounted locally beneath **/home** as **/home/guests/ldapuserX**
* home directories must be writable by their users
* while You are able to login as any of the users **ldapuser1-20** the only home directory You are able to access is **ldapuserX**
 

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* First we have to install **autofs** for usage:

```
yum install -y autofs
```

* Then we have to create config file for **autofs** that holds configuration. 

```
vi /etc/auto.master.d/home.autofs
# and put below content (start point for indirect mounts  -  conf file for this specific mount)
/home/guests /etc/auto.home
```

* As we mention config file in the previous step we have to create it:

```
vi /etc/auto.home
# put below contents there
* -rw,sync classroom.example.com:/home/guests/&
```

using wildcard * sign as a first parameter and & as the same in path on remote server will make sure that any user that is logged 
using LDAP will have its name used as parameter for mounting.

* Make sure that the service **autofs** is enabled and started:

```
systemctl enable autofs.service
systemctl start autofs.service
```

* Just SSH locally with user that is supposed to exist on LDAP server and check the home directory:

```
ssh ldapuser5@localhost
cd
pwd  # it should be /home/guests/ldapuser5
```


### Additional comment:

**autofs** is working in user space - and mounting network shares via **/etc/fstab** is using root context

Name of the config file in **/etc/auto.master.d** is not important - the only important thing is that is must have **.autofs** suffix
