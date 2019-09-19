# Install new kernel and make it default

### Question:
Install the kernel from the source http://some.link/to/kernel. The following criteria must be met:
* installed kernel will be the default one when system boots
* previous kernel is still available

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* In order to get new kernel from specified link You should add this link as a repository that can be seen by **YUM**.
The procedure for adding a repository was described in question **016** so I won't be repeating myself here.

* After the repo is added, enabled and visible by **YUM** the command is: 

```
yum install kernel  
```

* Mentioned criteria are actually not a problem as this is the default behaviour - the kernel is not itself updated but
new version is installed. By default system saves previous **4** versions of kernel on the disc.

* To make sure what is the default kernel being loaded by boot-loader we use a command **grubby**:

```
grubby --info=ALL
```

that will list all installed kernels (the one with index **0** will be loaded by default). If it is not the kernel You just
installed You can change it by issuing:

```
grubby --set-default-index INDEX_OF_NEW_KERNEL
```

and reboot the system to see if the changes apply







