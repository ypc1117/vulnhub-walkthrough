

### **Netdiscover**



![netdiscover](images/nightfall/netdiscover.png)

We use the tools called netdiscover scan hosts, we found the 192.168.0.106 is our target virtualbox host ip.

------

### **Namp**

![nmap](images/nightfall/nmap.png)

We found some services <u>FTP</u>, <u>SSH</u>, <u>HTTP</u>, <u>SMB</u>, <u>MYSQL</u> 

------

### Enum4linux

![samba](images/nightfall/samba.png)

![user](images/nightfall/user.png)

When we see smbd service , we use enum4linux scan smbd service config and basic infomation, we not found user but we find a smb share filefolder: <u>*IPC$*</u> and user: <u>*nightfall, matt*</u>

------

### Searchsploit

![search_mysql_exploit](images/nightfall/search_mysql_exploit.png)

By searchsploit mysql version, we can find two exploit ways existed.we save this two exploit scripts, may we use later.

------

### Gobuster



Try to use Gobuster to brute force the HTTP Server directory. regretfully, Nothing Found.

------

### Hydra


![hydra](images/nightfall/hydra.png)


Now, We have a samba share directory, we guest that the author may use ftp and samba.We try to use hydra to  brute force ftp password with user <u>*nightfall, matt*</u>. Try to brute force the user nightfall , then failed, Luckly, we found the ftp password of user matt , the password is <u>***cheese***</u>



### Solution


![ssh1](images/nightfall/ssh1.png)


We login in this user matt successfully, We found this "/" current directory. So we can use *<u>**.ssh authorized_keys</u>*** file to bypass the ssh login password. we create folder .ssh and upload authorized_keys to the .ssh filefolder. then we try to login by ssh with user matt, yeah, we login successfully .

![ssh2](images/nightfall/ssh2.png)

Now, We find wether if anything can make a **Privilege Escalation**

![find](images/nightfall/find.png)

we use linux find command, otherwise, we may use the linuxenum.sh.we found /scripts/find owned the suid permission, so we should use the ***/scripts/find*** to escalate privilege.

`/scripts/find . -exec /bin/sh -p \; -quit`


Now, We are user nightfall,  we use /home/matt/.ssh/authorizeds_keys instead of /home/nightfall/.ssh/authorized_keys, then we login successfully...

![ssh2](images/nightfall/ssh2.png)

We find whether the user nightfall has sudo privilege.

![sudo](images/nightfall/sudo.png)

user nightfall only has root privilege on **<u>/usr/bin/cat</u>**. so we decide to see what the **<u>/etc/passwd</u>** folder is.

![passwd](images/nightfall/passwd.png)

We found the root password hash is 

`root:$6$JNHsN5GY.jc9CiTg$MjYL9NyNc4GcYS2zNO6PzQNHY2BE/YODBUuqsrpIlpS9LK3xQ6coZs6lonzURBJUDjCRegMHSF5JwCMG1az8k.:18134:0:99999:7:::`

Now we use john( brute force password tools ) by Kali Linux.

![john](images/nightfall/john.png)

The password of root is <u>***miguel2***</u>, so we use su root with root password.Successfully, we found the flag.txt.

![ls2](images/nightfall/ls2.png)

![flag](images/nightfall/flag.png)

------

OS: Util now , We don't use mysql and samba server. →_→

------

**That' all , Thanks for your watching**
