

### **Netdiscover**



<img src="images/Screen Shot 2019-09-16 at 9.57.43 PM.png" alt="Screen Shot 2019-09-16 at 9.57.43 PM" style="zoom:100%;" />

We use the tools called netdiscover scan hosts, we found the 192.168.0.106 is our target virtualbox host ip.

------

### **Namp**

<img src="images/Screen Shot 2019-09-16 at 9.59.36 PM.png" alt="Screen Shot 2019-09-16 at 9.59.36 PM" style="zoom:100%;" />


We found some services <u>SSH</u>, <u>HTTP</u>, <u>SMB</u>

------

### Enum4linux


<img src="images/Screen Shot 2019-09-16 at 10.16.43 PM.png" alt="Screen Shot 2019-09-16 at 10.16.43 PM" style="zoom:100%;" />


<img src="images/Screen Shot 2019-09-16 at 10.22.33 PM.png" alt="Screen Shot 2019-09-16 at 10.22.33 PM" style="zoom:100%;" />



When we see smbd service , we use enum4linux scan smbd service config and basic infomation, we not found user but we find a smb share filefolder: <u>*wave, IPC$*</u> and user: <u>*aveng,root, wavex*</u>

------

### Solution

<img src="images/Screen Shot 2019-09-16 at 11.04.23 PM.png" alt="Screen Shot 2019-09-16 at 11.04.23 PM" style="zoom:100%;" />


connected samba server, two files found. we upload these files to our localhost.

<img src="images/Screen Shot 2019-09-16 at 11.06.09 PM.png" alt="Screen Shot 2019-09-16 at 11.06.09 PM" style="zoom:100%;" />


so i guess, we login in user wavex ==> find aveng user ==> root

now let's login in user wavex

<img src="images/Screen Shot 2019-09-16 at 11.07.51 PM.png" alt="Screen Shot 2019-09-16 at 11.07.51 PM" style="zoom:100%;" />


We download enumlinux.sh from github. run this scripts
<img src="images/Screen Shot 2019-09-16 at 11.11.51 PM.png" alt="Screen Shot 2019-09-16 at 11.11.51 PM" style="zoom:100%;" />


may aveng password in it

<img src="images/Screen Shot 2019-09-16 at 11.12.20 PM.png" alt="Screen Shot 2019-09-16 at 11.12.20 PM" style="zoom:100%;" />

So we ssh or su - aveng login successfully. found aveng is owned sudo privilege.

<img src="images/Screen Shot 2019-09-16 at 11.14.23 PM.png" alt="Screen Shot 2019-09-16 at 11.14.23 PM" style="zoom:100%;" />

now we su - , that's can we find flag.txt and whoami is root, congratulations

<img src="images/Screen Shot 2019-09-16 at 11.16.00 PM.png" alt="Screen Shot 2019-09-16 at 11.16.00 PM" style="zoom:100%;" />

------

**That' all , Thanks for your watching**
