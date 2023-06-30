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
   	- ```curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64```
   	- ```chmod +x kops-linux-amd64```
   	- ```sudo mv kops-linux-amd64 /usr/local/bin/kops```
  
   - Create the Nodes using the following command
   	- ```kops create cluster --name=kubepro.novocarenb.ca --state=s3://kubernetes-kops47 --zones=eu-north-1a,eu-north-1b --node-count=2 --node-size=t3.micro --master-size=t3.micro --dns-zone=kubepro.novocarenb.ca \```
   	- ```kops update cluster --name kubepro.novocarenb.ca --state=s3://kubernetes-kops47 --yes --admin```
   	- Now wait for 20 minutes until your cluster is being created
   	- Once cluster created validate using following command
   	- ```kops validate cluster --name kubepro.novocarenb.ca --state=s3://kubernetes-kops47```
   - Installation of Helm
     	- ```cd /tmp/```
     	- ``` wget https://get.helm.sh/helm-v3.12.1-linux-amd64.tar.gz 	```
     	- ``` tar xzvf helm-v3.12.1-linux-amd64.tar.gz ````
     	- ```cd linux-amd64/```
     	- ```sudo mv helm /usr/local/bin/helm```
    Now your Helm has been installed
    - GitHub Repo
      	- Clone the Project repo
      	- ```git clone https://github.com/amitgitz/cicdkube-docker.git```
      	- Install the Java
      	 ```
               sudo add-apt-repository ppa:openjdk-r/ppa
      	      sudo apt update
      	      sudo apt install openjdk-11-jdk
        ```
   -  Create the Namespace
      ``` kubectl create namespace prod ```
      ``` kubectl get pods  --namespace prod ```

Now go to the Jenkins
- create a node with KOPS Private Key and Validate it
- New Item : Kube-Deploy
- Type : Pipeline
- SCM : Git
- GitHub Repo : https://github.com/amitgitz/cicdkube-docker.git
- Branch : */main
- Save the file
- Click on Build
- If you did your configuration right your pipeline would be successfully built and your app deployed on the Kubernetes Cluster.
  ![image](https://github.com/amitgitz/cicdkube-docker/assets/88843810/5a5cd5db-9bfe-42b0-9b7d-b081df005f37)
- You can check your app by going to AWS Load Balancer and copying the DNS Name and Pasting it in Browser
- Load Balancer Example : acc4522f717b440e6a158027f045451e-1353310725.eu-north-1.elb.amazonaws.com
- ![image](https://github.com/amitgitz/cicdkube-docker/assets/88843810/cdbdd8c9-30fb-49c2-8e13-6f410d00b30c)
- ![image](https://github.com/amitgitz/cicdkube-docker/assets/88843810/cf611d35-6f7d-4fd5-8143-d632fb684bc9)
- Now you can validate each of the Service of your app
- Once done with everything make sure to clean up all the resources


Connect me at https://www.linkedin.com/in/devopsamit/ if you have any queries or suggestions.

Thanks, Keep Learning the Cloud
  



   
	

	
      	  
     
       
 




    
