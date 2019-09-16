# Create new filesystem on logical volume

### Question:
Create a ***xfs*** file system on a new logical volume of ***100MB*** called ***lv_xfs***. Mount it permanently with uuid under **/xfs**.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* Before any kind of operations on ***LVM*** it is good to know what we actually have in the system. The proper command to list all
devices we can use is in order **pvs**, **vgs** and **lvs**. It shows all physical storages and devices, volume groups and logical volumes.


* First we create a logical volume that is mentioned in the question and we create files system on it:

```
lvcreate –size 100M –name lv_xfs /dev/vg
# we can also use mkfs -type xfs /dev/vg/lv_xfs 
mkfs.xfs /dev/vg/lv_xfs
```

* After that we have to perform all the steps for permanent mounting, starting with creation of mount point:

```
mkdir /xfs
```


* Then we edit **fstab** file in order to make mounting permanent:   

```
blkid | grep lv_xfs >> /etc/fstab

OR 

vi /etc/fstab
UUID=... /xfs xfs defaults 1 2
```

* Finally we remount the discs by reloading **fstab** configuration using:
  
```
mount -a
```


### Additional comment:

Make sure that You know the difference between **partition label** and **file system name** - https://superuser.com/questions/1099232/what-is-the-difference-between-a-partition-name-and-a-partition-label/1099292
and You do not confuse them.

When editing **fstab** file by hand we got much more control over mount options. Also pay attention to the fact that with provided solution we use '1 2' values for 
checking mount point integrity - the first one indicates how often the partition will be backed by **dump** program, the second one points to the level of integrity check when
mounting (0 means no check, 1 is applied only to the root partition).