# Kubernetes Cluster Deployment using Ansible Script

This project is designed to deploy a multi-node Kubernetes cluster using Ansible scripts. The cluster consists of one master node and one worker node, with a valid container runtime and pod networking tool installed.

## Prerequisites
* Ansible (v2.9.6 or later)
* Two virtual machines with valid configurations and security settings
* Installation
* Clone this repository to your local machine.

## Create the playbooks and Run them

*	Create a new User Account for use with Kubernetes on each node
*	Install Kubernetes and containerd on each node
*	Configure the Master node
*	Get the join code from the master node
*	Join the Worker nodes to the new cluster

## Version issue (CRI v1 is not implemented)

if you face this kind of issue you can menually upgrade  containerd version with below steps

* In the Docker repos, there are packages for containerd 1.6 and above. So you can also add the Docker repos, and install containerd.io from there:

```sudo mkdir -p /etc/apt/keyrings
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install containerd.io 
```
* upgrading containerd to 1.6 or above, by downloading and replacing the binaries

```wget https://github.com/containerd/containerd/releases/download/v1.6.12/containerd-1.6.12-linux-amd64.tar.gz
tar xvf containerd-1.6.12-linux-amd64.tar.gz
systemctl stop containerd
cd bin
cp * /usr/bin/
systemctl start containerd
```


## Configuration Namespace
To create a namespace called "devops-test", run the following command:

```
kubectl create namespace devops-test

```
## CI/CD Pipeline
To establish a connection between a Jenkins CI/CD server and the Kubernetes cluster, you need to specify the Kubernetes configuration file in the Jenkins server.

## Application Deployment
To deploy an application to the cluster using the CI/CD pipeline script, follow these steps:

## Modify the Jenkinsfile to include your application deployment steps.
Push the modified Jenkinsfile to your Git repository.
Configure the Jenkins job to build the pipeline from the Jenkinsfile in the Git repository.
Run the Jenkins job to deploy the application to the devops-test namespace.
## Auto Deployment
Auto deployment can be implemented by configuring a continuous deployment pipeline in Jenkins, which automatically deploys changes to the devops-test namespace whenever a new version of the application is pushed to the Git repository.

## Transport Layer Security
Transport Layer Security can be implemented by enabling HTTPS communication between the Kubernetes API server and the worker nodes.

## Service Mesh using Istio
Service mesh can be implemented using Istio to improve the observability, security, and reliability of the application by managing the communication between microservices in the Kubernetes cluster.

## Conclusion
This project provides a simple and efficient way to deploy a multi-node Kubernetes cluster using Ansible scripts, and integrate it with a CI/CD pipeline for continuous deployment of applications. With additional configurations for security, service mesh, and transport layer security, the cluster can be further enhanced to meet the needs of any application deployment.