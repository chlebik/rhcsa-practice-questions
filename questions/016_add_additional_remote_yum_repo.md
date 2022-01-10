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

* Suppose the contents of the repo file is too hard to remember, you can alternatively use `yum-config-manager` to add a new repo and rename it later.

```
yum-config-manager --add-repo="http://local.repo/rhel7"

```
* This will create a new repo file in `/etc/yum.repos.d/local.repo_rhel7.repo` with the following contents.

```
[local.repo_rhel7]
name= created by dnf config-manager from http://local.repo/rhel7
baseurl=http://local.repo/rhel7
enabled=1
```
* You can then edit the file contents and rename the file as per you need. In our content, it would be:
```
[my_custom_repo] # renamed
name= my_custom_repo # renamed
baseurl=http://local.repo/rhel7
enabled=1
```

* Make sure that repository is seen by YUM:

```
yum repolist | grep my_custom_repo
* or other (which is more readable)
yum-config-manager my_custom_repo 
```
**Note:** You might encounter gpg check failures when you add a new repo, so skip gpg checks in that case append to the new repo file the following.
```
gpgcheck=0
```
