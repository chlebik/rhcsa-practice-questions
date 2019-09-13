# Assign SELinux context

### Question:
Assign the same **SELinux** contexts used by the home directories to the **/xfs** directory permanently.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* For interacting with **context** in **SELinux** we need a command that is not available by default on RHEL. Therefore we have to install it. First we find out
what is the package name we need:

```
yum whatprovides */semanage
```

* On my system (CentOS) it was **policycoreutils-python** with additional architecture/version suffix. This is what must be installed using **YUM**.

* There is a command called **chcon** - however its usage is not advised (besides restoring root password)!

* Finding proper **context** to be applied is usually the most tricky part. However it is good to remember that almost every Linux command that is used to list files/folders/processes/etc
has ***-Z*** flag, which will show the **SELinux** context of specified item. So we can use:
 
```
ls -Z /home
```

which on my computer produces the output below:

```
drwx------. chlebik chlebik unconfined_u:object_r:user_home_dir_t:s0 chlebik
```

* **Context** is the one with ***_t*** suffix. The way to assign it to mentioned ***/xfs*** target folder is this:

```
semanage fcontext -a -t user_home_dir_t "/xfs(/.*)?"
```

* However above command only assigns this **context** to the **policy**. In order to write it to the filesystem we need to invoke:

```
restorecon -R /xfs
```