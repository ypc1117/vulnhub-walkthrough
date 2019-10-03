

### **Netdiscover**

![netdiscover](images/hardy/netdiscover.png)

We use the tools called netdiscover scan hosts, we found the 192.168.0.107 is our target virtualbox host ip.

------

### **Namp**

![nmap](images/hardy/nmap.png)

We found some services  <u>HTTP</u>

------

### **Wpscan**

![index](images/hardy/index.png)

We found nothing in this page.So we brute force his web directory.

![gobuster](images/hardy/gobuster.png)

We found http://192.168.0.107/notes.txt and http://192.168.0.107/wordpress

![notes](images/hardy/notes.png)



![wordpress](images/hardy/wordpress.png)

About hint 1, we didn't know for the time beginning.

So we look about the hint 2. We scan the wordpress website.

![user](images/hardy/user.png)

We found wordpress users: **amin, aarti**, but sadly, i couldn't brute force their password.

![p0](images/hardy/p.png)

So we needed to scan wordpress plugin exploit and We found some interesting file. 

Here are 5-ways to got  root  privilege of the machine.

------

### Solution 1

![p0](images/hardy/p0.png)

**We found the reflex-gallery plugin has the Arbitrary File Upload.**

![exploit0](images/hardy/exploit0.png)

We use metasploit `exploit/unix/webapp/wp_reflexgallery_file_upload ` to get shell.

![shell0](images/hardy/shell0.png)

We could get the www-data user, so we should escalate our privilege to root.

![find](images/hardy/find.png)

Let's find thers which owns suid permissions file. So we find ***cp*** and ***wget*** has suid permission.

![passwd0](images/hardy/passwd0.png)

![passwd1](images/hardy/passwd1.png)

Because the machine  didn't open the ssh server , So we couldn't cp authorized_keys, But we could cp passwd to his /etc/passwd. So i copied this /etc/passwd to passwd in my local machine.

 So i  user perl  to generate his password hash.

![hacker](images/hardy/hacker.png)

`echo 'hacker:Go9OwoSklHOLU:0:0:root:/root:/bin/bash' >> passwd`

Then we  wget this passwd, and use cp to /etc/passwd.So we owns a root user called hacker

![root0](images/hardy/root0.png)

Yeah, We were root, then cd /root and Got the flag.

![flag](images/hardy/flag.png)

Successfully!!!

------

### Solution 2

![p0](images/hardy/p1.png)

We came back the mail-masta part, found a LFI exploit. So we linked the url

 https://www.exploit-db.com/exploits/40290/

![exploit1](images/hardy/exploit1.png)

![poc1](images/hardy/poc1.png)

We found the LFI has a effect.

So we look this /etc/apache2/.htpasswd

![aarti](images/hardy/aarti.png)

![aarti_passwd](images/hardy/aarti_passwd.png)

We found a Base64 encoded strings, and decode ==> found **aarti: aarti@gmail.com**

**![aarti_login](images/hardy/aarti_login.png)**

After tried login in http://192.168.0.107/wp-admin/ failed, I was sure that the  aarti@gmail.com is the detail of  the user aarti.



Successfully!!!

------

**That' all , Thanks for your watching**