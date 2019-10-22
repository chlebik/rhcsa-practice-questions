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
mkdir -p /var/log/journal
systemctl restart systemd-journald
```

and that's all. After reboot all logs will still be there.