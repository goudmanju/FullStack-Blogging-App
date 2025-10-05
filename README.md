**Jenkins and EKS Deployment with Terraform and Docker Setup**

**Overview**
This documentation outlines the steps to set up Jenkins and EKS clusters for deploying applications, using Docker, Terraform, and Kubernetes tools. The setup consists of launching Jenkins servers, configuring Docker and SonarQube, and deploying applications on an EKS cluster.

****Step-by-Step Process**

**1. Jenkins Server Setup****
•	Initially, launch 2 Jenkins servers (medium instances) for service queues.
•	Additionally, launch one large Jenkins server instance.
•	Install Java 17 JDK on Jenkins servers.
•	Install Jenkins.
•	Install Docker inside Jenkins servers.

**2. Docker Socket Permissions**

**Set permissions for Docker socket using:**
chmod 666 /var/run/docker.sock
**Install SonarQube on both Jenkins servers.**

**Run SonarQube containers using Docker:**
docker run -d -p 9000:9000 sonarqube:lts-community
docker run -d -p 8081:8081 sonatype/nexus3

**To get the admin password for Nexus:**
docker exec -it <container_id> /bin/bash
cat /nexus/admin.password

**Jenkins Plugins Installation**
**•	Install Tivm (presumably a plugin) in Jenkins servers.**

**5. SonarQube Token Creation**
•	Create tokens for SonarQube and Nexus artifact repositories.
•	Configure Docker Hub credentials in Jenkins tools section and system configuration.

**6. Plugins and Configurations**
•	Update configuration files to allow plugin downloads and configurations.

**7. EKS Cluster Deployment**
•	Deploy applications using AWS EKS cluster.
•	Setup EKS with Terraform scripts.

**8. Secondary Server Setup**
Launch an additional server.
Install Terraform.
Launch EKS cluster.
Install kubectl.

**Update Kubernetes config with:**
aws eks --region us-east-1 update-kubeconfig --name <cluster_name>

**Note:(It is used for authentication purpose)**

**Verify nodes with:**
kubectl get nodes

**Create Kubernetes resources:**
•	Namespace
•	ServiceAccount
•	Role
•	RoleBinding
• ⁠Create tokens for these resources.
**Final steps**
**Get secrets for namespace webapps:**
**kubectl get secrets -n webapps**
**kubectl describe secret <secret_name> -n webapps**
**Use these secrets/tokens for authentication and deployment.**
u will get the token copy the token and paste in jenkins credentials
