# Make journald persistent between reboots

PURE RHCSA8 QUESTION!

### Question:
Configure **journald** to persist between reboots

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* Usually **journald** does not preserve logs between reboots which can sometime makes troubleshooting pretty hard. 
 Enabling it to be persistent is pretty straightforward:

```
#edit the file /etc/systemd/journald.conf and change "#Storage=auto" to "Storage=persistent"
systemctl restart systemd-journald.service
```

and that's all. After reboot all logs will still be there.
### From `man journald.conf`:
> (...)  
> Storage= 
>> Controls where to store journal data. ... If "persistent", data will be stored preferably on disk, i.e. below the /var/log/journal hierarchy (which is created if needed), with a fallback to /run/log/journal (which is created if needed), during early boot and if the disk is not writable. "auto" behaves like "persistent" if the /var/log/journal directory exists, and "volatile" otherwise (the existence of the directory controls the storage mode)."
