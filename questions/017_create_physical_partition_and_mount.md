# Create new physical partition and create filesystem on it

### Question:
Create new physical partition with 100MB size and mount it under **/meet**

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
If there is anything else - **GPT**. **It is crucial to not mix them on one device(creating MBR partitions on GPT and vice versa)!**

* Of course to create a partition You have to use free disc space on physical device. When You figure out what kind of partitioning
 You want to use for that the process is fairly simple and similar to both **GPT/MBR**.
Just identify device on which You want to create a partition on and use:

```
# for MBR-like
fdisk /dev/something
# for GPT-like  
parted /dev/something
```

* If You decided to use MBR-like partition You can create **primary** or **extended** partition on the device. However there are only
**4 primary partitions** that can be created on a device. In order to use more first You have to create **extended** partition type and then
using it as a target create new **logical** partition on it (up to the total number of **15**).

* Editor will be opened where You choose **n** to create new partition, we prompt the start of block size, then to easy things
just provide **+100MB** value (instead of using blocks) and then remember to write the changes to the partition table by pressing
**w**. Then quit.

* We should let know the kernel that partition table was changed (compare **fdisk -l /link/to/disc** with **cat /proc/partitions**).
If there is a difference between them then:

```
partprobe /dev/something
```

* So far we've created a partition but there is no filesystem on it. When creating filesystem You have to know what type of filesystem
You would like to use. By default in **RHEL** system  **XFS** is used, but the most popular substitute is **EXT4**. Whatever type
You choose creating filesystem can be done like this:

```
mkfs -t PROVIDED_FILESYSTEM_TYPE /dev/link/to/new/partition
```

* We are almost there. Right now we need to create mount folder for the partition and permanently mount it. First we have to
find out the **UUID** of newly created partition. Using direct links to the partition or names is not recommended as they can be a 
subject to change. **UUID** are unique and permanent:

```
blkid

# find out the UUID of partition You just created

mkdir /meet
vi /etc/fstab

# append below definition to the file
UUID=UUID_YOU_GOT_FROM_BLKID    /meet   PROVIDED_FILESYSTEM_TYPE     defaults 0 0
```

* save the file and rerun mounting process by issuing:

```
mount -a
```

if everything is ok You should not be given any kind of error message.

### Additional comment:

There are shortcut commands for creating filesystems, eg. **mkfs.ext4**

