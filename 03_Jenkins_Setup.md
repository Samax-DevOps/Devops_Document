# Jenkins Server Setup in Linux VM #

## Step - 1 : Create Linux VM ##

1) Create Ubuntu VM using AWS EC2 (t2.medium) <br/>
2) Enable 8080 Port Number in Security Group Inbound Rules
3) Connect to VM using MobaXterm

## Step-2 : Instal Java ##

```
sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version
```

## Step-3 : Install Jenkins ##
```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins
```

## Step-4 : Start Jenkins ## 

```
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

## Step-5 : Verify Jenkins ##

```
sudo systemctl status jenkins
```
	
## Step-6 : Open jenkins server in browser using VM public ip ##

```
http://public-ip:8080/
```

## Step-7 : Copy jenkins admin pwd ##
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

## Step-8 : Change Jenkins Port ##  
```
sudo nano /etc/sysconfig/jenkins
```
 > look for port 8080 and change to 8081
 
>cat /etc/sysconfig/jenkins |grep JENKINS_PO
```
systemctl restart jenkins
systemctl start jenkins
systemctl status jenkins
```
	   
## Step-9 : Create Admin Account & Install Required Plugins in Jenkins ##
