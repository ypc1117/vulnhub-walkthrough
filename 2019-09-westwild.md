

### **Netdiscover**

![discover](images/westwild/discover.png)

We use the tools called netdiscover scan hosts, we found the 192.168.0.106 is our target virtualbox host ip.

------

### **Namp**

![nmap](images/westwild/nmap.png)


We found some services <u>SSH</u>, <u>HTTP</u>, <u>SMB</u>

------

### Enum4linux


![enuml4inux](images/westwild/enuml4inux.png)

![user](images/westwild/user.png)

When we see smbd service , we use enum4linux scan smbd service config and basic infomation, we not found user but we find a smb share filefolder: <u>*wave, IPC$*</u> and user: <u>*aveng,root, wavex*</u>

------

### Solution

![samba](images/westwild/samba.png)


connected samba server, two files found. we upload these files to our localhost.

![flag1](images/westwild/flag1.png)


so i guess, we login in user wavex ==> find aveng user ==> root

now let's login in user wavex

![ssh](images/westwild/ssh.png)

We download enumlinux.sh from github. run this scripts
![ififoregt](images/westwild/ififoregt.png)


may aveng password in it

![cat_ififoregt](images/westwild/cat_ififoregt.png)

So we ssh or su - aveng login successfully. found aveng is owned sudo privilege.

![sudo](images/westwild/sudo.png)

now we su - , that's can we find flag.txt and whoami is root, congratulations

![flag2](images/westwild/flag2.png)

------

**That' all , Thanks for your watching**
