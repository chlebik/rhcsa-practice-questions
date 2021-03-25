# Change hostname

### Question:
Change hostname of the system

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* Actually there are numerous ways to achieve that.
* The simplest one is just to use ***nmtui*** and choose proper item in the menu
* You can manually edit **/etc/hostname** (not recommended)
* It is possible to use specific command - **hostnamectl**:
 
```
hostnamectl set-hostname SOME_NAME
```

* It is possible to use **nmcli** for this with command:
 
```
nmcli general hostname SOME_NAME
```
 


### Additional comment:

Of course hostname is being shown near prompt sign in the console, however there is also a couple of ways of obtaining it
is using ***hostnamectl*** which besides info about hostname gives a lot of other useful information
