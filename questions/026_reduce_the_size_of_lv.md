# Reduce the size of existing logical volume

### Question:
Reduce the size of existing **logical volume** by **400MB**.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* First we list existing logical volumes:

```
lvdisplay   
```

* We should get the **/dev...*** link to our logical volume. That is step one. In order to shrink the existing size of
logical volume it requires unmounting it to perform this operation:

```
umount /MOUNT_POINT
```

* It came the time to resize our logical volume:

```
lvreduce -L -400M /dev/LINK_TO_LVM
```

* Now we just remount the volume again and check if everything as it should be:

```
mount -a
lvdisplay
```
