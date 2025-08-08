### **DevOps Day 2**



**\[killercoda]**



Permissions



* UGO Permission : U -> user ; G -> Group; O -> Other





\# hostnamectl set-hostname server.example.com

\# bash

\# mkdir /data

\# cat > devops.txt

Hello everyone

\# ll -d devops.txt

-rw-r--r--. 1 root root 15 Aug 5 04:15 devops.txt

**drwxr-xr-x**  -- ?????

**drwxrwxr--** --?????



---



**chown permission <resource name>**

**chgrp permission <resource name>**



---



* Owner can read, execute, write
* Grp can read and execute but not write
* Other category have users don't belong from ownership or group membership. They have read and execute permission by default.
* Permissions can be assigned in multiple way. On is alphabetically, like r for read, w for write and x for execute.
* Value of **r is 4**, value of **w is 2** and value of **x is 1**. **Total = 7**
* So, **chmod 777 /data** :- 1st 7 is full permission for owner, 2nd 7 is full permission for group and 3rd 7 is full permission for others.
* **chmod u+rwx g+rwx o-rwx /data**
* ^^ u is user, g is group and o is others. (+) gives permissions while minus (-) revokes permission. So, we revoke all permission from others.
* **chmod 770 /salesdata/**

---



* **777 max permission on folder**
* **666 max permission on file.** (There is no execute permission on file)



---



* Sticky Bit (always on folder)
* ^^can read but can't delete.
* Some **o+t** or something command.  (resources availabl but we can't delete)
* **g+s**
* sgidbit -- on group level

---



\# ll -d /salesdata/

drwxrwx---



---



**whreis useradd**

**vim /etc/sudoers**

to login a user:



**su - username**

**sudo su -**



To logout:



**logout**

**:se nu**

**:wq!**

**:q**

**vim /etc/sudoers**

**whereis useradd**





**sudo** before commands like adding a new user etc.

Do not add any user to %wheel

Add user to root ALL=(ALL)





---



from the user account, do **whereis useradd**. Then, copy the user location, something like userbin something. Then logout, then from root, do vim /etc/sudoers. Then, password can be added on the all thing, but not on the wheel thing. But since the sudoers file is very sensitive, and vim doesn't show if we made any error, the **visudo** command is better.

---



SETUP:



open terminal

copy paste the key

then,

sudo su -

passwd

\[set and confirm password]

hostnamectl set-hostname server.example.com

bash

cat /etc/os-release



Then, we can useradd etc.



---



How to manage the daemons - disk and executing management program



**rpmquery httpd**

(Apache)^^

**vim /etc/httpd**

**vim /etc/httpd/conf/httpd.conf**

**systemctl status httpd    (To quit the status view mode, press 'q')**

**systemctl start httpd**

**systemctl restart httpd**

**cd /var/www/html/**

**curl http://localhost**

**curl http://localhost:80**

^^By default, apache runs on port 80.



--how to add this port on aws?





---



**systemctl reload**

**systemctl reload-or-restart httpd.service**



---



MASKING

unmasking



---



CONFIGURE AND SECURE SSH

