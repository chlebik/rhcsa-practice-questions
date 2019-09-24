# Create compressed archive

### Question:
Create the archive file **/root/local.tgz** for **/usr/local** compressed by **gzip**.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* The command is simple and straightforward (just remember that **-f** flag must be the last one as the file name follows it):

```
tar -cvzf /root/local.tgz /usr/local
```