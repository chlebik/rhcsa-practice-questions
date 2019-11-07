# Directory ownership by a group

User's creation was covered by question 008 

### Question:
Create a directory named ***/common***. Allow **john** and **davis** to share documents in the ***/common*** directory using a group called **team**.
Both of them can read, write and remove documents from the other in this directory but any user not member of the group can’t.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* As mentioned above - creation of user is covered in question ***008***. Also it is always worth mentioning that in the questions related to
creating something it is better to actually create everything before we delve deeper into configuration (folders/files/users/groups/partitions)

* First we create a directory which is pretty straightforward (however creating user-related folders in root hierarchy is not a good idea)

```
mkdir /common
```

* Then we create mentioned group and assign it as an owner of already created folder:

```
groupadd team
chgrp team /common
```


* Here is the most tricky part. To achieve our goal we will be using **SGID**, which is a concept that users operating on the files are
given the same permissions like to group owner of the folder/file. We've already set group owner for the folder so now we assign permissions to it.   

```
chmod 2770 /common
```

Notice the ***2*** prefix in the access rights. This sets up **SGID**. That means that any user from the group that owns the file/folder will be given
group permissions when operating on it. It simplifies administration as You do not have to give users access via **ACLs** to the folder, rather than
just assign them to the group and that's it.

* Finally we need to remember to actually add our users to the mentioned group **team**.
  
```
usermod -aG team john
usermod -aG team davis
```


### Additional comment:

It is possible to change user's primary group for the current session using **newgrp** command.

