# Allow user access to home directory of another user

User's creation was covered by question 008 

### Question:
Allow ***davis*** (and only ***davis***) to get full access to ***john's*** home directory.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* Usually the system operates only on file/folder user owner and group owner. The default settings for users is that the files and
folders created by that user are given ownership (user and group) of the creating user. 

* This question is somehow problematic to me. From the way it is constructed it seems that simple:

```
chown -R davis:davis /home/john
chmod -R 700 /home/john 
```

should suffice. 

* In order to extend the possibility to add additional users to be able to operate on folders and files there is a concept of
**ACL**. They are set using the command **setfacl**.

* In the given case we can use below command to achieve what we want (however this **adds** the ownership not **replaces** it)   

```
setfacl -R -m u:davis:rwx /home/john
```

* To check what is the status of **ACLs** on the file/home we use ***getfacl /home/john***.

* Above commands are changing existing files and folders (with ***-R*** making it recursive). However if we want to make it applicable to the 
  new files and folders there must be ***d:*** (default) prefix used. So the final command should look like:
  
 ```
 setfacl -R -m d:u:davis:rwx /home/john
 ```


### Additional comment:

**ACLs** are indicated by the **'+'** (plus) sign at the end of the owning folder (this is the listing from ***/home*** folder):
```
drwxrwx---+  7 davis   davis    176 Jun 27 16:23 john
```

For the partition to be able to use **ACLs** it must be mounted with ***acl mount*** property

Removal of **ACLs** is achieved also via ***setfacl*** command but with proper flag (see man pages for examples)
