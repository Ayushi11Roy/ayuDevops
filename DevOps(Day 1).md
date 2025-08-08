DevOps:

end-to-end product delivery.



4 environments:



1\. dev env

2\. test

3\. UAT

4\. prod



CI: Continuous Integration, on the integration side

CD: Continuous Deployment, on the deploying side



^^ done using Jenkins (open-source) -- there are many others, but yeahhh



-- It minimizes delivering time.



Linux: is a Kernel,  not an Operating system



Hypervisor

ISO

Centos Linux

partition: automatic and custom storage



Types of roots in Linux:



1\. Superuser

2\. Administrator

3\. Root home directory





Swap space, dirty page, Out of memory killer

Temp folder Linux -- world readable



VPC

SSH

RDP, rdp port no: 3389

ARN - amazon resource no



=====================



COMMANDS:



**cat /etc/os-release**

**hostnamectl set-hostname server.example.com**

**bash** (Sometimes the hostname will not reflect even after setting it. So, we can either exit or use the bash command)

**hostname**

**hostnamectl** (System info we can see)

**ip a s** (to check ip address)

**ll** --

**ls**

**cat /etc/passwd**

**nl /etc/passwd**

**less /etc/passwd** (We can find any specific keyword with the less command)

**mkdir data**

**pwd** (Present working directory)

**cd /**

**date**

**cal**

bin folder -- commands which anyone can execute

**cd etc/**  (Configuration file, only accessible through root)



imp: dev, etc, root



* only root can execute all the commands.
* By default, in cloud platform, root account is locked. To enable, we need to set a password. But then also, we can disable the password. (?)
* If filename starts with dot (.), then it's a hidden file.
* System user can exist but cannot see.
* System user id vary version to version.



l :- link

d :- ????



**touch filename.txt**

**cat > filename.txt**

**rm filename.txt**  (File will not be deleted??)

**whoami**

**rm -rf**

**tree**



Logging in from diff acc:- **su**

Example:



**su - root**



**exit**

**logout**

**alias** (if there's a lengthy command, we can create aliases. But alias will be removed once we exit the environment.

**sudo**

**sudo su** \[something something]

**cls**



==============================



User admin



Types of users in Linux:



Super user -> root

System user -> apache, samba, smbd, htpd ftp etc

Regular user or normal user -> general people like Ram, Shyam etc



---

How to create user (regular user):

---

**useradd Ram**

**passwd Ram**



-- but the machine will not recognize Ram. Because in Linux or maybe in other systems as well, some id is assigned and the machine recognizes by that id.

In Linux, a UID is assigned. Regular user UID starts from 1000. Root UID is 0.



**yum**

**yum install httpd -y**

**vim /etc/passwd**  -- world readable file.

**vim /etc/shadow**

**vim /etc/login.defs**

**chage --help**

**tail /etc/group**

**head /etc/group**





what is: **sbin/nologin**



**Demon process**





**cat /etc/shadow**



* /etc/shadow file can't be read by anyone other than the root. And it can access user info but not the password.
* When trying to switch from one account to another, always use a hyphen (-).

Eg: su - pooja  :- will go to the home dir. Without hyphen, will go to root.



* Field separator
* **$6$** -- sha512 algo for encryption



**usermod --help**

**usermod -s /sbin/nologin username**

 -- doesn't let user to login

To check if the access is actually removed, type **cat /etc/passwd** .

then try to login using **su - username**  . Login should not happen.

==================================================



Groups (Collection of users)

---



Primary group

Secondary group



* By default, every user is a part of primary group.
* One single user can be a part of multiple groups ETHICALLY. But, we need to use append, to add the user to both the groups.
* How to add one user to another group?



**groupadd**

**usermod -G mktg ironman**

**cat /etc/group | grep -i mktg**



**usermod -G sales jacksparrow**

**cat /etc/group | grep -i sales**



**usermod -G sales ironman**   (ironman will get out from mktg group)

BUT

**usermod -aG sales ironman** (ironman will remain part of both the groups) (a : append)

==================================


