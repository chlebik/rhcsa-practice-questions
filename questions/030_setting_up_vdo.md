# Configure block device to use VDO

PURE RHCSA 8 QUESTION!

### Question:
Apply **VDO** (Virtual Data Optimizer) to the block device.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* **VDO** is a way to provide deduplication and compression of data on the disc. Worth read material can be found
<a href="https://hobo.house/2018/09/13/using-vdo-on-centos-rhel7-for-storage-efficiency/">here</a>.

* Configuring system to use it is starting with installation of proper kernel modules and drivers and then running
installed service:

```
yum -y install vdo kmod-kvdo 
systemctl enable vdo.service
systemctl start vdo.service
```

* Creating VDO is easy:

```
vdo create --name=SOME_NAME --device=/dev/BLOCK_DEVICE --vdoLogicalSize=SIZE
```

* size should be different depending on the type of objects stored. For containers the multiplier of size can be up to
**10 times** than size of block device. For object storage it can be up to **3 times**. So eg. for **20GB** device we want to 
use for object storage we can set the size of VDO to **60GB**. 

* when creating VDO we do not want to discard blocks when making the filesystem. So use proper switch (see man pages) for specific 
type of filesystem being created.

```
mkfs.xfs -K /dev/LINK
# or
mkfs.ext4 -E nodiscard /dev/LINK
```

after this make sure to refresh registers:

```
udevadm settle
```

* mounting of VDO is simple but requires adding additional properties to ***/etc/fstab*** file when doing it:

```
UUID=smething  /mount_point   FS_TYPE  _netdev,x-systemd.device-timeout=0,x-systemd.requires=vdo.service 0 0 
```

### Additional comment:

We require over **500MB** of RAM for every TB of storage to apply VDO.

The commands to check status and size of VDOs are:  **vdo** and **vdostats**
