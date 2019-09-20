# Configure new NTP server

### Question:
Configure Your system that it is **NTP** client of **classroom.example.com** 

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* **NTP** is a service that is using **chrony** deamon. It should be already installed in the system but it does not cost You
to issue:

```
yum install -y chrony
systemctl enable chronyd.service
systemctl start chronyd.service
```

to make sure it is installed, up and running. Also we have to enable it:

```
timedatectl set-ntp 1
```

* Config file for this service is **/etc/chrony.conf**: 

```
vi /etc/chrony.conf
```

* There is a list of servers being used to get time from. The lines start with **server**. In order to use only one of the 
servers (the one that is provided in question) You should comment all others and just put new line there: 

```
server classroom.example.com iburst
```

* User command to interfere with **chronyd** is **chronyc**. To list the **NTP** sources being used we issue:

```
chronyc sources -v
```


### Additional comment:

Second parameter in the **chrony.conf** file (***iburst***) is the interval between requests. More in man pages.
