# Set new default system level

### Question:
Set the default target to boot into **X Window level** (previously level 5).

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* It is simple task configuring **systemd** properly:

```
systemctl set-default graphical.target
```

* We can also check if it succeeded with:

```
systemctl get-default
```

### Additional comment:

Here is the list of all targets in **systemd**:
  * 0	poweroff.target
  * 1	rescue.target
  * 2	multi-user.target
  * 3	multi-user.target
  * 4	multi-user.target
  * 5	graphical.target
  * 6	reboot.target


Some time ago a file **/etc/inittab** was used to specify default system level however now it is deprecated and does not work. 
