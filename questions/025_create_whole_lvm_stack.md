# Create whole LVM stack

### Question:
Create a new physical volume with volume group in the name of **datacontainer**, the extent of VG should be **16MB**.
Also create new logical volume with name **datacopy** with the size of  **50 extents** and filesystem **vfat** mounted
under **/datasource**. 

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* Before any kind of operations on ***partitions*** it is good to know what we actually have in the system. The proper command to list all
devices we can use is in order **lsblk**. Also You have to be sure what kind of partitioning scheme was used (**MBR** mostly used on
older computers or **GPT** on computers that use **UEFI**). I advise reading this article to get knowledge hot to find out what
is going on in the system: https://www.binarytides.com/linux-command-check-disk-partitions/

* You can issue:

```
fdisk -l
# it is possible that You will have to install this tool
parted -l   
```

if the output for label/partition table contains **DOS** in any way then the partition table was configured using **MBR**. 
If there is anything else - **GPT**. **It is crucial to not mix them on one device (creating MBR partitions on GPT and vice versa)!**


* Creating new partition was described in **question 017**. Make sure that the type of partition is set to **Linux LVM** and that
You run **partprobe** after it (to let kernel reread new partition table). 


* When we got the partition the first step is to create **physical partition**: 

```
pvcreate /dev/PARTITION_IDENTIFIER
# check if it was created
pvdisplay
```

* Physical partition can be assigned to the **volume group**.

```
vgcreate -s 16M datacontainer /dev/PARTITION_IDENTIFIER
# check if it was created
vgdisplay
```

* Now it is time to create **logical volume** (notice **-l switch** that allows specifying extents number):

```
lvcreate -l 50 -n datacopy datacontainer
# check if it was created
lvdisplay
```

* Creating filesystem can be done with **mkfs** with **type** flag or with specialized tool like below:

```
mkfs.vfat /dev/datacontainer/datacopy
```

* Now we create mount point for it and we provide entry in **fstab** file to make it permanent:

```
mkdir /datasource
# get UUID for created logical volume
blkid
# edit /etc/fstab and append there below line
UUID=UUUID_IDENTIFIER_COPIED_FROM_BLKID  /datasource vfat  defaults   0 0    
```

* Save the file and check if everything works:

```
mount -a
```
