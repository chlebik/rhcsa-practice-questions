# User creation with specific properties

### Question:
Create two users: ***john*** with uid/gid equal to 2000, password 12345678 and ***davis*** with uid/gid equal to 3000, password 87654321. 
Make ***davis'*** password validity stopping in one month.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* The best command for user creation and editing are these starting with ***user*** - so ***useradd*** and ***usermod***. 

```
useradd -u 2000 john
passwd john
# here provide password for john

useradd -u 3000 davis
passwd davis
# here provide password for davis
```

* Right now is the time to change validity of ***davis*** account.  On my system (CentOS) I've run:

```
[root@centos1 ~]# chage -l davis
Last password change                                    : Sep 14, 2019
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 0
Maximum number of days between password change          : 99999
Number of days of warning before password expires       : 7
```

* Given that we know the current date we can set expiry date manually by copying the following from the chage man pages:

```
man chage
chage -E $(date -d +30days +%Y-%m-%d)
```

### Additional comment:
Using "man chage" and scrolling down a bit you can copy and paste the command above without memorizing it and just simply paste the number of days you want to add until the account expires.
Remember there is a difference between **password expiration** and **account validation**. It is usually better to expire password and 
make user not being able to log into the system or disable the user, rather than deleting it.

**usermod** command is also used for adding/removing users to the group (**groupmod** command does not do that)

Trying to create user with already taken UID will result in an error.
 
During user's creation with **useradd** command the structure of home direcotry is taken from ***/etc/skel*** folder. 
