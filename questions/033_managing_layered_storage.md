#  Manage layered storage

PURE RHCSA 8 QUESTION!

### Question:
Create pool and filesystem for thin provisioning and snapshots.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* Actually, the question stated above is not in fact a question. The problem with **layered storage** in **RHEL 8** is that 
there is still not that much information about it available online.

* **Stratis** is a tool (written in Rust language) that is supposed to be used in **RHEL 8** for managing layered storage.
How to fully create **pool** from block devices and then **filesystems** is very well explained in <a href="https://stratis-storage.github.io/howto/">Stratis How-to</a> - so I won't 
be rewriting this. 

* In my opinion, this objective was introduced to actually raise awareness of this tool. And for the time being, I do not expect heavy-metal-questions
 about it.
