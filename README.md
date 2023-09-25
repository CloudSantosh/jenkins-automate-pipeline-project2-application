# Jenkins Pipeline for java base web application using Maven, SonarQube, Ansible and (EKS) Kubernetes

The project involves building and deploying a Java application using a CI/CD pipeline. Here are the steps involved:

**Version Control:** The code is stored in a version control system such as Git, and hosted on GitHub. The code is organized into branches such as the main or development branch.

**Continuous Integration:** Jenkins is used as the CI server to build the application. Whenever there is a new code commit, Jenkins automatically pulls the code from GitHub, builds it using Maven, and runs automated tests. If the tests fail, the build is marked as failed and the team is notified.

**Code Quality:** SonarQube is used to analyse the code and report on code quality issues such as bugs, vulnerabilities, and code smells. The SonarQube analysis is triggered as part of the Jenkins build pipeline.

**Containerization:** Docker is used to containerizing the Java application. The Docker file is stored in the Git repository along with the source code. The Docker file specifies the environment and dependencies required to run the application.

**Container Registry:** The Docker image is pushed to Docker Hub, a public or private Docker registry. The Docker image can be versioned and tagged for easy identification.

**Continuous Deployment:** Webhooks is used to automate the deployment of the containerized application to Kubernetes. Whenever a new version of the application image is pushed to the Git repository, Webhook will automatically deploy it to the Kubernetes cluster.

Overall, this project demonstrates how to integrate various tools commonly used in software development to streamline the development process, improve code quality, and automate deployment

Configure all below pre-requisites for project.

## Overview of project

<img src="https://github.com/CloudSantosh/jenkins-automate-pipeline-project2-application/tree/main/images/project.png" width="600" hight="100">

<br/>
<br/>

## +++++++++++++++++++++++++++ PART-2 ++++++++++++++++++++++++++++

### Configure all below pre-requisites for project.

<br/>

1. **[Install Jenkins & Ansible & Maven ](https://github.com/CloudSantosh/jenkins-automate-pipeline-project2-infra)**

2. **[Install Sonarqube](https://github.com/CloudSantosh/jenkins-automate-pipeline-project2-infra)**

3. **[Install Kubernetes Cluster](https://github.com/CloudSantosh/jenkins-automate-pipeline-project2-infra)**

4. **[Git Account](https://github.com/)**

5. **[Dockerhub Account](https://hub.docker.com/)**

<br/>
<br/>

## +++++++++++++++++++++++++++ PART-3 ++++++++++++++++++++++++++++

### Configure jenkins pipeline job.

```

Login Jenkins > New Item > project-1 > Pipeline > OK

    	               Pipeline:
    	                    Definition: Pipeline script from SCM

    	               SCM: Git

    	                 Repositories:
    	                      Repository URL: https://github.com/sunnydevops2022/devops_real_time_project_1.git

    	                 Script Path: Jenkinsfile

```

<br/>

### Jenkins integration with Sonarqube server.

<br/>

### Login Sonarqube server

```

Sonarqube > My Account > Security > Generate Tokens
Name : porject-1
Type : Global Analysis Token
Expires : 30 Days
Generate

After that copy token & save it.

```

### Go to Jenkins and create credential for Sonar token

```

Dashboard > Manage Jenkins > Credentials > System Global credentials (unrestricted) > Add credentials >
kind: Secret text
Scope: Global
Secret: **\*\***
ID: SONAR_TOKEN
Des: SONAR_TOKEN
Create

```

<br/>

### Configure inventry file & Password less authentication with Kubernetes server.

```

+++++++++++++++ KUBERNETES SERVER ++++++++++++++++++++++

passwd root
cp -r /etc/ssh/sshd_config /etc/ssh/sshd_config_orig
sed -i "s/#PermitRootLogin prohibit-password/PermitRootLogin yes/g" /etc/ssh/sshd_config
sed -i "s/PasswordAuthentication no/PasswordAuthentication yes/g" /etc/ssh/sshd_config
systemctl restart sshd.service

+++++++++++++++ ANSIBLE SERVER ++++++++++++++++++++++

cat /etc/ansible/hosts

> /etc/ansible/hosts
> cat /etc/ansible/hosts

vim /etc/ansible/hosts

[kubernetes]
<kubernetes_ip>

cat /etc/ansible/hosts
su - jenkins
ansible -m ping kubernetes -u root
ssh root@<kubernetes_ip>
ssh-keygen
ssh-copy-id root@<kubernetes_ip>
ssh root@<kubernetes_ip>

ansible -m ping kubernetes -u root

```

<br/>

### Create credential for Dockerhub server login.

```

Dashboard > Manage Jenkins > Credentials > System Global credentials (unrestricted) > Add credentials >
kind: Secret text
Scope: Global
Secret: **\*\***
ID: DOCKERHUB_USER
Des: DOCKERHUB_USER
Create

##################################

Dashboard > Manage Jenkins > Credentials > System Global credentials (unrestricted) > Add credentials >
kind: Secret text
Scope: Global
Secret: **\*\***
ID: DOCKERHUB_PASS
Des: DOCKERHUB_PASS
Create

```

<br/>

### Github integrate with Jenkins.

```

+++++++++++++++ GITHUB ACCOUNT ++++++++++++++++++++++
Github > Repository > Settings > Webhooks > Add Webhooks >
Payload UR : http://<jenkins_ip>:8080/github-webhook/
Content type : application/json

    					Just the push event.

+++++++++++++++ JENKINS SERVER ++++++++++++++++++++++

Jenkins > project-1 > Configure > Build Triggers >
GitHub hook trigger for GITScm polling

```

<br/>
<br/>
<br/>
<br/>

## `*************************   EOF   *************************`

```

```
