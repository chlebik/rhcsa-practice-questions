# Add new remote repository for YUM

### Question:
Add additional repository for YUM with name **my_custom_repo** which can be found via URL **http://local.repo/rhel7**

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* **YUM** repositories are configured mostly in the file **/etc/yum.conf**. We can see the total contents of this file with
added formatting using command (if it is not installed You can find it in the **yum-utils** package):

```
yum-config-manager
```

* Among the properties listed in this file is **reposdir** which specifies (by default) paths to folders which are being scanned for
 files containing information about repositories. In my case the existing folder is **/etc/yum.repos.d**. 

* We create a config file in this folder - by convention the suffix of these files is **.repo**. 

```
vi /etc/yum.repos.d/my_custom_repo.repo
# and we enter in editor below content
[my_custom_repo]
name=my_custom_repo
baseurl=http://local.repo/rhel7
enabled=1
```

* Make sure that repository is seen by YUM:

```
yum repolist | grep my_custom_repo
* or other (which is more readable)
yum-config-manager my_custom_repo 
```
