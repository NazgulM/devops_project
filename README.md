# Jenkins Pipeline for java base web application using Maven, SonarQube, Ansible, and (EKS) Kubernetes

The project involves for Java-based web application using Maven, SonarQube, Ansible, and EKS (Kubernetes).

![diagram](1.png)

**Version Control**: The code is stored in a version control system such as Git, hosted on GitHub. 

**Continuous Integration**: Jenkins is used as a CI server to build the application. whenever there 
is a new code, Jenkins automatically pulls the code from GitHub, builds it using Maven, and runs 
automated tests. If the tests fail, the build is marked as failed and then the team is notified.
