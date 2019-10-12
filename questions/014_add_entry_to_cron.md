# Add entry to cron

### Question:
Create a cron job running as ***root***, starting at ***11PM every day*** and writing a report on daily system resource consumption in the **/var/log/consumption.log** file.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* Command use to gather system statistics is called **sar** and may not be installed on the system. So first what we have to do is install it and then enable the service:

```
yum install sysstat
systemctl enable sysstat
systemctl start sysstat
```


* As usual it is wise to check what we have already in the system. To see **crontab** we just issue:

```
crontab -l
```

if there are no jobs scheduled then we get information about it.


* edit crontab:

```
crontab -e
# and then editing the file by adding
0 23 * * * /usr/bin/sar -A > /var/log/consumption.log
```

### Additional comment:

The log file does not need to exist - it will be created automatically.
Of course **root** user can edit crontab of every user with flag **-u** specifying user name.
It is worth remembering that there are **/etc/cron.allow** and **/etc/cron.deny**. 
