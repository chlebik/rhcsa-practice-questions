# Configure access rights to the file

### Question:
Copy the file **/etc/fstab** to **/var/tmp**. The file copied should be owned by **root**, the group also should be set to **root**
and should not be executable by anyone.
The user **andrew** should have read&write access to this file.
User **susan** should not have any rights to this file.
All other users (current or future) should have the ability to read this file.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* We start with copying the file with permissions it already have

```
cp /etc/fstab /var/tmp
ls -al /var/tmp
```

* We have to create users mentioned in question (if we do not have them already): 

```
useradd andrew
useradd susan
```

* Setting special access rights to files/directories is achieved via **FACL**. The commands are:

```
setfacl -m u:andrew:rw- /var/tmp/fstab
setfacl -m u:susan:--- /var/tmp/fstab
# in order to check if everything is ok
getfacl /var/tmp/fstab
```

* By default all other users can read this file so this requirement is already met.
