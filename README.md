# Jenkins Pipeline for java base web application using Maven, SonarQube, Ansible, and (EKS) Kubernetes

The project involves for Java-based web application using Maven, SonarQube, Ansible, and EKS (Kubernetes).

![diagram](1.png)

**Version Control**: The code is stored in a version control system such as Git, hosted on GitHub. 

**Continuous Integration**: Jenkins is used as a CI server to build the application. whenever there 
is a new code, Jenkins automatically pulls the code from GitHub, builds it using Maven, and runs 
automated tests. If the tests fail, the build is marked as failed and then the team is notified.

**Containerization**: Docker is used to containerize the Java application. The Docker file is stored
in the Git repository along with the source code. The docker file specifies the environment and dependencies 
required to run the application.

**Container registry**: The Docker image is pushed to Docker Hub, a public or private Docker Registry. 
The Docker image can be versioned and tagged for easy identification.

**Continuous Deployment**: Webhooks are used to automate the deployment of the containerized application 
to Kubernetes. Whenever a new version of the application is pushed to  the Git repo, Webhook will automatically 
deploy it to the Kubernetes cluster.

Overall, this project demonstrates how to integrate various tools commonly used in software development to 
streamline the development process, improve code quality, and automate deployment

Configure all the below pre-requisites for the project.

1. Install Jenkins & Ansible & Maven

2. Install Sonarqube

3. Install Kubernetes Cluster

4. Git Account

5. Dockerhub Account

@@ Install Jenkins & Ansible & Maven @@

**************** JENKINS INSTALLATION *****************

Pre-Requisites

Jenkins -Ansible Server Details:

Operating System: Ubuntu

Hostname: jenkins-ansible

RAM: 2 GB

CPU: 1 Core

EC2 Instance: t2.small

![jenkins](2.png)

Update the repository of Ubuntu: 

```
sudo -i
sudo apt-get update
```

Change timezone:

```
date
timedatectl
sudo timedatectl set-timezone America/Chicago
timedatectl
date
```

Change hostname:

```
hostname
hostnamectl set-hostname jenkins-ansible
bash
hostname
```

Install Java

```
java -version
apt-get install openjdk-11-jdk
java -version
```

Install Jenkins:

```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins=2.361.3 -y
```

Service start, enable and check status:

```
systemctl start jenkins
systemctl enable jenkins
systemctl status jenkins
```

![jenkins](3.png)

Check 8080 port is used or not

```
netstat -plant | grep 8080
tcp6       0      0 :::8080                 :::*                    LISTEN      4891/java

jenkins - version
Running from: /usr/share/java/jenkins.war
webroot: $user.home/.jenkins
Exception in thread "main" java.lang.IllegalArgumentException: Multiple command line argument specified: version
	at winstone.cmdline.CmdLineParser.parse(CmdLineParser.java:67)
	at winstone.Launcher.getArgsFromCommandLine(Launcher.java:413)
	at winstone.Launcher.main(Launcher.java:383)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:566)
	at executable.Main._main(Main.java:334)
	at executable.Main.main(Main.java:116)
```

URL: http://<jenkins_server_ip>:8080

![unlock](4.png)

Get Jenkins Administrator password using this command:

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

![sudo](5.png)

![customize](6.png)

![started](7.png)

After completing the installation of the suggested plugin you need to set the First Admin User for Jenkins.

![admin](8.png)

![admin2](9.png)

Click Save and Continue:

![instance](10.png)

Start using Jenkins:

![start](11.png)


*************** ANSIBLE INSTALLATION *****************

Add Ansible repository:
```
sudo apt-add-repository ppa:ansible/ansible
```

Now fetch the latest update & install Ansible:

```
sudo apt update
sudo apt-get install ansible -y
```

```
ansible --version
ansible [core 2.14.6]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.10.6 (main, Mar 10 2023, 10:55:28) [GCC 11.3.0] (/usr/bin/python3)
  jinja version = 3.0.3
  libyaml = True
```

**************** MAVEN INSTALLATION *****************

Change dir to /opt and download maven:

$ wget https://mirrors.estointernet.in/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
$ tar -xvf apache-maven-3.6.3-bin.tar.gz

Add the following lines to the user profile file (.profile).

M2_HOME='/opt/apache-maven-3.6.3'
PATH="$M2_HOME/bin:$PATH"
export PATH

mvn -version
Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
Maven home: /opt/apache-maven-3.6.3
Java version: 11.0.19, vendor: Ubuntu, runtime: /usr/lib/jvm/java-11-openjdk-amd64
Default locale: en, platform encoding: UTF-8
OS name: "linux", version: "5.19.0-1025-aws", arch: "amd64", family: "unix"
```


