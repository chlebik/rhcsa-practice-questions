# Configure virtual console

The description of this question on cert-depot is not clear. However it is worth knowing the tool used to configure kernel boot options. 

### Question:
Configure a virtual console.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* Setting virtual console is a part of configuring kernel parameters. Therefore a command **grubby** can be used:

```
grubby –update-kernel=ALL –args="console=ttyS0"
```

* With above parameters we update all kernels that are installed on the system with argument setting default console.

### Additional comment:

Kernels are not updated but installed as new ones. By default **4** previous kernels are kept on the system.