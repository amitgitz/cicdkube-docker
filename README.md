![image](https://github.com/amitgitz/cicdkube-docker/assets/88843810/5cbc0683-8153-43c4-a8c7-99df66c4568e)
## Prerequisites
- AWS Account
- Kubernetes Nodes
- DockerHub Account
- Jenkins Server
- SonarQube Server
- Kops VM (EC2 Instance)

## Technologies 
- Spring MVC
- Spring Security
- Spring Data JPA
- Maven
- JSP
- MySQL
- AWS
- Docker
- Jenkins
- Kubernetes
- SonarQube
- Helm
## Flow of Execution
1. Continuous Integration Setup
   - Jenkins, SonarQube, and Nexus (Continuous Integration Project)
3. DockerHub Account (Containerization Project)
4. Store DockerHub Credentials in Jenkins
5. Setup Docker Engine in Jenkins
6. Install Plugins in Jenkins
	- a. Docker-pipeline
	- b. Docker
	- c. Pipeline utility
7. Create Kubernetes Cluster with Kops
8. Install Helm in Kops VM
9. Create Helm Charts
10. Test Charts in K8s Cluster in the test namespace.
11. Add Kops VM as Jenkins Salve
12. Create Pipeline code [Declarative]
13. Update Git Repository with
	- a. Helm Charts
	- b. Dockerfile
	- c. Jenkinsfile (pipeline code)
14. Create Jenkins Job for Pipeline
15. Run and Test the Job

 ## Jenkins Setup
 - Jenkins SG
 - It should allow traffic from SonarQube SG and the following rules
  ![image](https://github.com/amitgitz/cicdkube-docker/assets/88843810/f6b747f1-453e-4685-8b6e-da6f947c8908)

## SonarQube Setup
- SonarQube SG
- It should allow traffic from Jenkins SG and following rules
![image](https://github.com/amitgitz/cicdkube-docker/assets/88843810/b990f418-9d64-4a7a-8d2e-128b5a366448)

## Kubernetes (KOPS Setup )
 - create an EC2 instance with `ubuntu20lts` with `t3.micro`
 - SSH to EC2 Instance and give the following command
    - ```sudo apt update && sudo apt install awscli -y ```
    - configure the AWS with the access-key with Administrative access
 - Install Kubectl with the following Commands
     - ``` curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl ```
     - now give the execution command and move it to the bin directory
     - ``` chmod +x kubectl ```
     - ``` mv kubectl /usr/local/bin ```
  
   - Install Kops with the following Commands     
       
 




    
