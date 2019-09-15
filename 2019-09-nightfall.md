

### **Netdiscover**



<img src="images/Screen Shot 2019-09-15 at 9.53.11 AM.png" alt="Screen Shot 2019-09-15 at 9.53.11 AM" style="zoom:50%;" />

We use the tools called netdiscover scan hosts, we found the 192.168.0.106 is our target virtualbox host ip.

------

### **Namp**



<img src="images/Screen Shot 2019-09-15 at 10.09.45 AM.png" alt="Screen Shot 2019-09-15 at 10.09.45 AM" style="zoom:50%;" />

We found some services <u>FTP</u>, <u>SSH</u>, <u>HTTP</u>, <u>SMB</u>, <u>MYSQL</u> 

------

### Enum4linux



<img src="images/Screen Shot 2019-09-15 at 7.43.24 PM.png" alt="Screen Shot 2019-09-15 at 7.43.24 PM" style="zoom:50%;" />



<img src="images/Screen Shot 2019-09-15 at 8.31.39 PM.png" alt="Screen Shot 2019-09-15 at 8.31.39 PM"  />



When we see smbd service , we use enum4linux scan smbd service config and basic infomation, we not found user but we find a smb share filefolder: <u>*IPC$*</u> and user: <u>*nightfall, matt*</u>

------

### Searchsploit

<img src="images/Screen Shot 2019-09-15 at 8.18.19 PM.png" alt="Screen Shot 2019-09-15 at 8.18.19 PM" style="zoom:50%;" />

By searchsploit mysql version, we can find two exploit ways existed.we save this two exploit scripts, may we use later.

------

### Gobuster



Try to use Gobuster to brute force the HTTP Server directory. regretfully, Nothing Found.

------

### Hydra


<img src="images/Screen Shot 2019-09-15 at 8.56.28 PM.png" alt="Screen Shot 2019-09-15 at 8.56.28 PM" style="zoom:50%;" />


Now, We have a samba share directory, we guest that the author may use ftp and samba.We try to use hydra to  brute force ftp password with user <u>*nightfall, matt*</u>. Try to brute force the user nightfall , then failed, Luckly, we found the ftp password of user matt , the password is <u>***cheese***</u>



### Solution


<img src="images/Screen Shot 2019-09-15 at 9.07.55 PM.png" alt="Screen Shot 2019-09-15 at 9.07.55 PM" style="zoom:50%;" />


We login in this user matt successfully, We found this "/" current directory. So we can use *<u>**.ssh authorized_keys</u>*** file to bypass the ssh login password. we create folder .ssh and upload authorized_keys to the .ssh filefolder. then we try to login by ssh with user matt, yeah, we login successfully .

<img src="images/Screen Shot 2019-09-15 at 9.22.15 PM.png" alt="Screen Shot 2019-09-15 at 9.22.15 PM" style="zoom:50%;" />

Now, We find wether if anything can make a **Privilege Escalation**

<img src="images/Screen Shot 2019-09-15 at 9.24.05 PM.png" alt="Screen Shot 2019-09-15 at 9.24.05 PM" style="zoom:50%;" />

we use linux find command, otherwise, we may use the linuxenum.sh.we found /scripts/find owned the suid permission, so we should use the ***/scripts/find*** to escalate privilege.

`/scripts/find . -exec /bin/sh -p \; -quit`

<img src="images/Screen Shot 2019-09-15 at 9.35.30 PM.png" alt="Screen Shot 2019-09-15 at 9.35.30 PM" style="zoom:50%;" />


Now, We are user nightfall,  we use /home/matt/.ssh/authorizeds_keys instead of /home/nightfall/.ssh/authorized_keys, then we login successfully...

<img src="images/Screen Shot 2019-09-15 at 9.47.04 PM.png" alt="Screen Shot 2019-09-15 at 9.47.04 PM" style="zoom:50%;" />

We find whether the user nightfall has sudo privilege.

<img src="images/Screen Shot 2019-09-15 at 10.01.01 PM.png" alt="Screen Shot 2019-09-15 at 10.01.01 PM" style="zoom:50%;" />

user nightfall only has root privilege on **<u>/usr/bin/cat</u>**. so we decide to see what the **<u>/etc/shadow</u>** folder is.

<img src="images/Screen Shot 2019-09-15 at 10.02.18 PM.png" alt="Screen Shot 2019-09-15 at 10.02.18 PM" style="zoom:50%;" />

We found the root password hash is 

`root:$6$JNHsN5GY.jc9CiTg$MjYL9NyNc4GcYS2zNO6PzQNHY2BE/YODBUuqsrpIlpS9LK3xQ6coZs6lonzURBJUDjCRegMHSF5JwCMG1az8k.:18134:0:99999:7:::`

Now we use john( brute force password tools ) by Kali Linux.

<img src="images/Screen Shot 2019-09-15 at 10.09.59 PM.png" alt="Screen Shot 2019-09-15 at 10.09.59 PM" style="zoom:50%;" />

The password of root is <u>***miguel2***</u>, so we use su root with root password.Successfully, we found the flag.txt.
<img src="images/Screen Shot 2019-09-15 at 10.13.45 PM.png" alt="Screen Shot 2019-09-15 at 10.13.45 PM"  />

<img src="images/Screen Shot 2019-09-15 at 10.13.26 PM.png" alt="Screen Shot 2019-09-15 at 10.13.26 PM" style="zoom:50%;" />

------

OS: Util now , We don't use mysql and samba server. →_→

------

**That' all , Thanks for your watching**
