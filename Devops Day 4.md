**Devops Day 4**





-------

cloudstakh -- linkedin

-------





BRM Process

ci/cd - Jenkins (Open-source) - create pipelines

Pipelines: Declarative approach

UI Based pipeline



GitHub actions can also be used, but there are some differences. Like, Jenkins is open-source and GitHub actions is closed-source, under MS. Security differences as well.



Jenkins alternatives:



Spacelift

GitHub Actions

GitLab CI

CircleCI

Travis CI

CodeShip

AWS CodePipeline

Azure DevOps

Bitbucket Pipelines

TeamCity



Diff b/w continuous deployment and continuous delivery: Continuous delivery is manual approach while continuous deployment is automatic approach.



Continuous Delivery means the software is always ready to be released, with the final decision to deploy being a manual step.

Handles automatic release to the repo.



Continuous Deployment means the software is automatically released to production once it passes the automated tests, eliminating the manual approval step. Handles automatic deployment to the productions.



---------------------------------



First host Jenkins

then on GitHub do something.............



-----------------------



We can install plugins on Jenkins and customize it according to our requirements.



---------------------------------



yum install Jenkins

--Jenkins isn't available on yum. 



**Jenkins is developed under java.**



yum repolist all



--------



We need to install a java library called java corretto

Then, we can install Jenkins.



-- we can find Jenkins installation process on Jenkins documentation.



------------



Then, we'll enable Jenkins and start it.



sudo systemctl enable Jenkins

sudo systemctl start Jenkins

systemctl status Jenkins



-------------------------



By default, Jenkins uses port:8080.

we need to allow port 8080 on security group, otherwise the below link will not run. (ie, :8080 part)

<ip address>:8080  -- to open jenkins from web. The ip address is the public ip address of the instance.



Jenkins default password is always stored inside : On Linux, you'll usually find it at **/var/jenkins\_home/secrets/initialAdminPassword** or **/var/lib/jenkins/secrets/initialAdminPassword**



After the status Jenkins command, find the password. Then, webhook (I think)

------------------------



webhook



go to GitHub webhook.



------------



Generate token on Jenkins

Create new api token



--------------



Why use multiple resources: single point of failure





-------------------



git branch -M main

git remote add origin <ssh url from github>

git remote -v

\[If we add hhtp url while adding the remote branch, then there will be error in authentication further down the line, because GitHub will not allow https authentication, only ssh. So, if we do that by mistake, or in general, if we want to remove the remote branch, command:]

git remote remove origin



Now authenticate git using ssh to establish connection. We do it by generating the key. We generate the key in the root folder, not in the directory.



Genrate key using ssh-keygen

then see the key using, cat ~/.ssh/id\_rsa.pub





----------------------------------





Jenkins job create:



new item > item name give whatever > job style : frestyle > okay

source control > git > repo url (http)

Branches to build > /main

Apply > save (Triggers for now, manually)





---------------



Jenkins slave machine Jenkins -- when to build, why to build



---------------------------



WHAT IF WHEN JENKINS BECOME SLOW: (After restarting vm -- why?)



1. cd /var/lib/Jenkins/
2. Here, there is a file called Jenkins model.
3. In EC2, on shutting down instance, public ip addresses changes but on restarting/rebooting, the public address doesn't change.
4. But the Jenkins address is the prev one only, in my case: 
5. So, we need to change the new public ip address with the Jenkins one, on the Jenkins model file.
6. How to:



* cd /var/lib/Jenkins
* vim jenkins.model.JenkinsLocationConfiguration.xml
* The file that will open will contain the previous ip address. Copy-paste the new public ip address there. And save and exit.
* systemctl start Jenkins
* systemctl status jenkins
* systemctl restart jenkins
----------------------------



NODE DOWN JENKINS (When space is less)





1. df -h   (we press this command to se the files
2. cd /tmp/    (temporary processes)
3. tmpfs /tmp tmpfs defaults,noatime,mode=1777,size=2G 0 0
4. To permanently allocate the space, we do:
5. vim /etc/fstab
6. Then on ##for temp, we add:
7. tmpfs /tmp tmpfs defaults,noatime,mode=1777,size=2G 0 0
8. Save the file
9. sudo mount -a
10. if mount doesn't happen, remount, using command:
11. sudo mount -o remount,size=2G /tmp
12. Then, to check if the space was allocated 
13. systemctl daemon-reload
14. You can also do,
15. sudo systemctl daemon-reexec
16. sudo systemctl restart tmp.mount
17. Now we restart (reboot) the instance and see if the space has been increased.





----------------------------

CLEAN WRITE-UP. WHAT TO DO:-

============================



1. Make instance on aws
2. Connect, copy the key and paste it on the terminal like usual.
3. sudo su -
4. bash
5. yum install git -y
6. Create a directory, mkdir devops
7. cd devops
8. initialize git: git init
9. create a file and write something: cat > test.txt 
10. see what's written: cat test.txt
11. git status
12. git add .
13. git commit -m "Created a file."
14. Now, authenticate.
15. To authenticate, 1st generate a ssh key.
16. ssh-keygen
17. Now, this will come:  Enter file in which to save the key (/root/.ssh/id\_rsa):  \[press enter]
18. Keep pressing enter in all the consecutive prompts like: 

&nbsp;	Enter passphrase (empty for no passphrase):

&nbsp;	Enter same passphrase again:

19\. Now, this will come:



&nbsp;	Your identification has been saved in /root/.ssh/id\_rsa

&nbsp;	Your public key has been saved in /root/.ssh/id\_rsa.pub

&nbsp;	The key fingerprint is:

&nbsp;	SHA256:i+FnjVL9Qwzo23gNo+wA/OBUmHjm09Bkv13qjC4kBxA root@ayu-server.example

&nbsp;	The key's randomart image is:

&nbsp;	+---\[RSA 3072]----+

&nbsp;	|  E.  o          |

&nbsp;	|  .. \* . .       |

&nbsp;	|  ..\* o o . .    |

&nbsp;	|   =.+ . + =     |

&nbsp;	|    B.o S \* o    |

&nbsp;	|   o.\*o= % \*     |

&nbsp;	|    .+\* @ \* +    |

&nbsp;	|      .B .   .   |

&nbsp;	|       .o        |

&nbsp;	+----\[SHA256]-----+



20\. cd ~   (we are going to the root directory)

21\. ls -a  (listing the files)

&nbsp;	.   .bash\_logout   .bashrc  .ssh     devops

&nbsp;	..  .bash\_profile  .cshrc   .tcshrc

22\. in the .ssh directory, the key is saved.

23\. So, we do: cd .ssh

24\. Then, we do 'ls' to see the files in the .ssh directory.

25\. There is a file called "id\_rsa.pub". In that file, the key is saved.

26\. cat is\_rsa.pub

&nbsp;	\[the key is shown]

* Then, we go to github > profile > settings > ssh and gpg > add new ssh > paste the ssh key, and save.
* This was the authentication.

27\. cd ~

28\. cd devops

29\. git branch (to see which branch we are in)

30\. git push origin master

31\. Then, there are commands which we are getting from jenkins documentation called "jenkins on aws" (commands for installing and then downloading jenkins).

32\. Then, if space issue is shown, do the node thing written above.

33\. To connect github with jenkins now, we need to set the webhook.

34\. Github > Repo settings > webhooks > add webhook > payload url : http://<link of jenkins>/github-webhook/



* On secret tab, we need to add an api key.
* To generate the key:
* &nbsp;	go to jenkins settings > security > (scroll down) access key > create/generate > copy key > go to github and paste it on secrets > save 



35\. Build jenkins (select github option on trigger)

36\. make changes on github file

37\. see if the change appears on jenkins as well. To see, go to workspace, select the file, and see if the changes appear.

Jenkins on aws commands:

Downloading and installing Jenkins


1.	Completing the previous steps enables you to download and install Jenkins on AWS. To download and install Jenkins:

2.	The following steps are written for Amazon Linux 2. If you’re using Amazon Linux 2023, it’s recommended to use dnf instead of yum. While the yum command is still available for compatibility in this context, it is actually a symbolic link to dnf and may not support all of its features. For more details, please refer to the official AWS documentation.
3.	Ensure that your software packages are up to date on your instance by using the following command to perform a quick software update:

4.	[ec2-user ~]$ sudo yum update –y

1.	Add the Jenkins repo using the following command:
2.	
3.	[ec2-user ~]$ sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo


1.	Import a key file from Jenkins-CI to enable installation from the package:

2.	[ec2-user ~]$ sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

3.	[ec2-user ~]$ sudo yum upgrade

4.	Install Java:

5.	[ec2-user ~]$ sudo yum install java-17-amazon-corretto -y

6.	Install Jenkins:

7.	[ec2-user ~]$ sudo yum install jenkins -y

8.	Enable the Jenkins service to start at boot:

9.	[ec2-user ~]$ sudo systemctl enable jenkins

10.	Start Jenkins as a service:

11.	[ec2-user ~]$ sudo systemctl start jenkins

12.	You can check the status of the Jenkins service using the command:

13.	[ec2-user ~]$ sudo systemctl status jenkins

Jenkins is now installed and running on your EC2 instance. To configure Jenkins:

Connect to 

http://<your_server_public_DNS>:8080

from your browser. You will be able to access Jenkins through its management interface

To generate the password:

[ec2-user ~]$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword



