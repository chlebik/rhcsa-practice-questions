#  Find files containing specific text within

### Question:
Find All Files in ***/etc*** (not subdirectories) that contain text "chrony" (ignore case).

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* For browsing file's contents the main command is **grep**. Below is the simple one-liner.

```
grep -lis chrony /etc/*
```


### Additional comment:

There is something known as **UUOC** which stands for **Unnecessary use of CAT**. It got its own history and is mentioned
separately <a href="https://en.wikipedia.org/wiki/Cat_(Unix)#Useless_use_of_cat">wiki</a>.