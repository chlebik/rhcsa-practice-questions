# Search for string using grep and redirect the output

### Question:
Search the string **sarah** in the **/etc/passwd** file and save the output in **/root/lines**

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* The command is simple and straightforward (just remember that **>** overrides the file contents and **>>** appends):

```
grep sarah /etc/passwd >> /root/lines
cat /root/lines
```