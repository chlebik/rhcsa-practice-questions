# Create swap partition

### Question:
Create a logical volume of **200MB** called **lv_swap2** and add it permanently to the current swap space.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* Before any kind of operations on ***LVM*** it is good to know what we actually have in the system. The proper command to list all
devices we can use is in order **pvs**, **vgs** and **lvs**. It shows all physical storages and devices, volume groups and logical volumes.


* First we create a logical volume that is mentioned in the question and we create swap on it:

```
lvcreate –size 200M –name lv_swap2 /dev/vg
mkswap /dev/vg/lv_swap2
swapon /dev/vg/lv_swap2  
```

* To make swap changes permanent as usual ***/etc/fstab*** must be edited:

```
vi /etc/fstab
/dev/vg/lv_swap2 swap swap defaults 0 0
```

* It is good to check if everything works - the best way is to reboot the system (if possible) and after that issuing:


```
swapon -s
free -k
```

which will show swap/memory statistics.


### Additional comment:

Both commands **mkswap** and **swapon** have parameters like **-L** and **-U** so it is possible to give these commands not only the
path (to the file or partition) but label or UUID.