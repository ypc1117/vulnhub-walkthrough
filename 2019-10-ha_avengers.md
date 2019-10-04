

### **Netdiscover**

![netdiscover](images/avengers/netdiscover.png)

We use the tools called netdiscover scan hosts, we found the 192.168.0.110 is our target virtualbox host ip. 

------

### **Namp**

![nmap0](images/avengers/nmap0.png)

![nmap1](images/avengers/nmap1.png)

We found some services <u>HTTP, SSH</u>

------

### Solution

![80](images/avengers/80.png)

![8080](images/avengers/8080.png)

We looked the https certificate, find the stone.

![mindstones](images/avengers/mindstones.png)

At first, We use dirb to brute the website directory.

![dirb](images/avengers/dirb.png)

We found http://192.168.0.100/wifi and http://192.168.0.100/wfi and http://192.168.0.100/img

![space](images/avengers/space.png)

![spacestone](images/avengers/spacestone.png)

We linked to the /img, we found the space.jpg , we got the stone by **strings space.jpg**

![wifi](images/avengers/wifi.png)

![pwd](images/avengers/pwd.png)

So we use python to generate wordlist dictionary auto.

![wordlist](images/avengers/wordlist.png)

We now have passowrd dictoary. but we have no user. So we tried to use the dictionary to brute force the wifi cap.

![aircrack](images/avengers/aircrack.png)

Now we have wifi password. But we have nothing else. May we should try to use the **gamA00fe2012** as web directory.

![gamA00fe2012](images/avengers/gamA00fe2012.png)

![realitystone](images/avengers/realitystone.png)

Got the stone.

![aether](images/avengers/aether.png)

Why the author give us a suvery to do.  as we see , i thought there was a strings by 01, but it was only 8 bit,

So there may dirctory. 

direcory is http://192.168.0.100/01101001/

![braincode](images/avengers/braincode.png)



![brain_decode](images/avengers/brain_decode.png)

We Got the **admin:avengers**, their may jenkins user and password.

![jenkins](images/avengers/jenkins.png)

We are login in jenkins server successfully!!!

![exploit](images/avengers/exploit.png)

We have jenkins user and password, After a litter tries, so we use a authorized exploit.

![shell](images/avengers/shell.png)

Now we got the user jenkins.

![find](images/avengers/find.png)

Let's find wether anything owns suid permission.

![timestone](images/avengers/timestone.png)

We Got a another stone.

![users](images/avengers/users.png)

Let's to see how many users in home. we found the user morag.

![morag.kdbx](images/avengers/morag.kdbx.png)

And we find the /opt exists morag.kdbx. this is a key hint. we should get the user morag, then escalate privilege to root. Let's begin.

![keepassjohn](images/avengers/keepassjohn.png)

Because we have not kdbx database login password, So we use keepass2john by kail to generate hash.

![john](images/avengers/john.png)

Then we got the login password. the password is **princesa**.

![powerstone](images/avengers/powerstone.png)

![cred](images/avengers/cred.png)

We use keepass2(linux) to do it, we open the kdbx with password. We found the FLAG and  Creds.

![decode](images/avengers/decode.png)

The cred strings is base64 encoded,  we decoded it. we found the password keypair==> **morag:yondu**

![ssh](images/avengers/ssh.png)

Yeah, login was okay.

![sudo](images/avengers/sudo.png)

Let's we find wether exists any command to escalate our privilege.

![root](images/avengers/root.png)

we use /bin/sh to spawn shell env and we got root privilege.

![final](images/avengers/final.png)

Finally, we cd /root and get the flag.

Successfully!!!

------

**That' all , Thanks for your watching**