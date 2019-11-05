

### **Netdiscover**

![netdiscover](images/bossplayerctf/netdiscover.png)

We use the tools called netdiscover scan hosts, we found the 192.168.111.231 is our target virtualbox host ip.

------

### **Namp**

![nmap](images/bossplayerctf/nmap.png)

We found some services <u>SSH</u>, <u>HTTP</u>

------

### Solution

![index](images/bossplayerctf/index.png)

![dirb](images/bossplayerctf/dirb.png)

We found http://192.168.111.231/robots.txt

![robots](images/bossplayerctf/robots.png)

![d_robots](images/bossplayerctf/d_robots.png)

The strings maybe a password.  

![index_resource0](images/bossplayerctf/index_resource0.png)

![index_resource1](images/bossplayerctf/index_resource1.png)

![workinginprocess](images/bossplayerctf/workinginprocess.png)

We found a hidden php page. http://192.168.111.231/workinginprogress.

![workpage](images/bossplayerctf/workpage.png)

After i tried params: file, command,cmd, found the param is cmd

![id](images/bossplayerctf/id.png)

![nc](images/bossplayerctf/nc.png)

So we use cmd to reverse the shell.

![shell](images/bossplayerctf/shell.png)

Let's look around the home directory.

![ls](images/bossplayerctf/ls.png)

Let's find wether somethings owns suid permission.

![find](images/bossplayerctf/find.png)

Yeah, we could use find to escalate our privilege.

`find . -exec '/bin/sh' -p \;`

![root](images/bossplayerctf/root.png)

We Got the root user. So let's go to the /root directory to get the flag.

![flag](images/bossplayerctf/flag.png)

Successfully!!!

------

**That' all , Thanks for your watching**