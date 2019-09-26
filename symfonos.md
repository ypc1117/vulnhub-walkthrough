

### **Netdiscover**

![netdiscover](images/symfonos/netdiscover.png)

We use the tools called netdiscover scan hosts, we found the 192.168.111.140 is our target virtualbox host ip.

------

### **Namp**

![nmap](images/symfonos/nmap.png)

We found some services <u>ssh</u>, <u>smtp, http, smb</u>

------

### Solution

![index](images/symfonos/index.png)



![enumlinux](images/symfonos/enumlinux.png)

We Found a anonymous directory, by connecting from smbclient.

![smb](images/symfonos/smb.png)

![attention](images/symfonos/attention.png)

We uploads attention.txt and found some possible passwords.

![hailos](images/symfonos/hailos.png)

So we login in **helios** with password **qwerty**.![smb2](images/symfonos/smb2.png)

Found /h3l105 directory, so we add /etc/hosts with [symfonos.local](http://symfonos.local/)

![hello](images/symfonos/hello.png)

We found a wordpress website, So we use wpscan to do it.

![user](images/symfonos/user.png)

admin found

![wpscan1](images/symfonos/wpscan1.png)

![wpscan2](images/symfonos/wpscan2.png)

LFI found. We use Unauthenticated LFI

```HTML
wp-content/plugins/mail-masta/inc/campaign/count_of_send.php?pl=/etc/passwd
```

Successfully!!

![LFI](images/symfonos/LFI.png)

We known that exists a mail server, so we cat this user mail.

![mail](images/symfonos/mail.png)

So We use php log poision attack.

![mail_poision](images/symfonos/mail_poision.png)

![poc0](images/symfonos/poc0.png)

We can execute ls -al command, so we nc to reverse shell.

![poc](images/symfonos/poc.png)

![shell](images/symfonos/shell.png)

Now we are reverse shell successfully!!, let's find those which owns suid permission file.

![find](images/symfonos/find.png)

We found **/opt/statuscheck**, check his type , return.![resp](images/symfonos/resp.png)

This is http header, we guess may something important in executeable file.

![type](images/symfonos/type.png)

![rev](images/symfonos/rev.png)

So we execute

`echo '/bin/sh' > curl`

`chmod 777 curl`

`mkdir /tmp`

`mv curl  /tmp`

`export PATH=/tmp:$PATH`

`/opt/statuscheck`

![root](images/symfonos/root.png)

now we'are root., So let's get the flag.

![flag](images/symfonos/flag.png)

Successfully!!!

------

**That' all , Thanks for your watching**