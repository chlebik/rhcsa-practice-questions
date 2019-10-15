# Create folder with group access rights

### Question:
Create a collaborative directory **/redhat/sysgrp** with following properties:
* group ownership of the folder is for group **sysgrp**
* members of **sysgrp** should have full access to this folder but no other user
* files created in this folder have by default group access to **sysgrp** 

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* Creation of **sysgrp** may be or may be not necessary. Simply **grep /etc/groups** to see if the group is already in the system.
If not: 

```
groupadd sysgrp
```

* Create folder we are talking about and assign it group ownership:

```
mkdir -p /redhat/sysgrp
chgrp sysgrp /redhat/sysgrp/
```

* Assign access rights to the folder. Remember that **2** mentioned below is called **SGID** - which means that when user 
does something on folder/file with **GUID** set will be assigned the access rights of the group.
Assigning **7** to owner and group owner makes sure that the contents of directory is not only readable and writable but also can 
be listed (which **7** for folders mean).

```
chmod 2770 /redhat/sysgrp
ls -ltr /redhat/  # to check the permissions
```

* Create a file in the folder and see the permissions given:

```
touch /redhat/sysgrp/test.log
ls -ltr /redhat/sysgrp
```

### Additional comment:

Even if the user creating file in the directory is **root** it will still have group owner of **sysgrp**.
