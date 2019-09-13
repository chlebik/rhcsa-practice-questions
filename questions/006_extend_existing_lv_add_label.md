# Extend existing logical volume by 200MB and add label to it 

### Question:
Extend the existing ***xfs*** file system to a total size of ***200MB*** and add a label called ***myFS***.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* Before any kind of operations on ***LVM*** it is good to know what we actually have in the system. The proper command to list all
devices we can use is in order **pvs**, **vgs** and **lvs**. It shows all physical storages and devices, volume groups and logical volumes.

* Exam objectives require extending of logical partitions. The tricky part here is to remember that **XFS** filesystem (which is the default setting for RHEL)
does not allow downsizing of **XFS** partition (the only possibility is to grow that volume). So please be careful when reading LVM related questions
during the exam.
  
* When question is presented in a form we have in this task we can assume that the logical volume is less than given **200MB** we have to set. Then we can use: 

```
# notice -r flag which indicates not only to resize logical volume but also filesystem on it
lvextend –size 200M -r /dev/VOLUME_GROUP/LOGICAL_VOLUME
```

* In order to give a logical volume a label we have to unmount it first, set a label and then mount it again:
 
```
# umount /LINK/TO/FILESYSTEM/MOUNT/POINT
# xfs_admin -L "myFS" /dev/VOLUME_GROUP/LOGICAL_VOLUME
# mount /LINK/TO/FILESYSTEM/MOUNT/POINT
```