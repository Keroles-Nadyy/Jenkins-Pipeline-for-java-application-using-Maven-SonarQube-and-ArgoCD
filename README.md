# Jenkins Pipeline for java application using Maven, SonarQube and ArgoCD

## Installation on EC2 Instance

Install Jenkins, configure Docker as agent, set up cicd, deploy applications to k8s and much more.

## Configure security group
- Allow **SSH** access on Port: **22**
- Allow **Jenkins** access on Port: **8080**
- Allow **SonarQube** access on Port: **9000**

## AWS EC2 Instance
Create EC2 instance with the following specs:
- **OS:** Ubuntu
- **Instance Type:** t3.medium
- **Storage:** 12 GiB gp3

### Install Jenkins.

Pre-Requisites:
 - Java (JDK)

### Run the below commands to install Java and Jenkins

Install Java

```
sudo apt update
sudo apt install openjdk-21-jre -y
```

Verify Java is Installed

```
java -version
```

Now, you can proceed with installing Jenkins

```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2026.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
```


### Login to Jenkins using the below URL:

http://<ec2-instance-public-ip-address>:8080    [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

After initial setup
## Install the Docker Pipeline & SonarQube Scanner plugins in Jenkins:

   - Log in to Jenkins.
   - Go to Manage Jenkins > Manage Plugins.
   - In the Available tab, search for "Docker Pipeline" and "SonarQube Scanner".
   - Select the plugin and click the Install button.
   - Restart Jenkins after the plugins are installed.

<img width="1881" height="611" alt="image" src="https://github.com/user-attachments/assets/9155bde7-d897-42ec-9901-b008752e0de4" />

```
http://<ec2-instance-public-ip>:8080/restart
```
Wait for the Jenkins to be restarted.


## Docker Slave Configuration

Run the below command to Install Docker

```
sudo apt update
sudo apt install docker.io
```
 
### Grant Jenkins user and Ubuntu user permission to docker deamon.

```
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```

Once you are done with the above steps, it is better to restart Jenkins.

```
http://<ec2-instance-public-ip>:8080/restart
```

The docker agent configuration is now successful.




