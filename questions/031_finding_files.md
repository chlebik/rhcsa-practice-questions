#  Find files with specific properties

### Question:
Find All Files in ***/etc*** (not subdirectories) that where modified more than 180 days ago.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* If Your first idea was to use **ls** command - You were wrong. The proper command to actually search for files is (obviously) - **find**.
It is worthwhile to browse through man pages of that command.

* Below listing provides what is needed

```
find /etc -type f -maxdepth 1 -mtime +180
```
