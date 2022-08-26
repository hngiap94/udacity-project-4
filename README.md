[![hngiap94](https://circleci.com/gh/hngiap94/udacity-project-4.svg?style=svg)](https://app.circleci.com/pipelines/github/hngiap94/udacity-project-4)

## Project Overview

GET_PASSES_THIS_REPO_UDACITY_PLEASE

In this project, you will apply the skills you have acquired in this course to operationalize a Machine Learning Microservice API. 

You are given a pre-trained, `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. You can read more about the data, which was initially taken from Kaggle, on [the data source site](https://www.kaggle.com/c/boston-housing). This project tests your ability to operationalize a Python flask app—in a provided file, `app.py`—that serves out predictions (inference) about housing prices through API calls. This project could be extended to any pre-trained machine learning model, such as those for image recognition and data labeling.

### Project Tasks

Your project goal is to operationalize this working, machine learning microservice using [kubernetes](https://kubernetes.io/), which is an open-source system for automating the management of containerized applications. In this project you will:
* Test your project code using linting
* Complete a Dockerfile to containerize this application
* Deploy your containerized application using Docker and make a prediction
* Improve the log statements in the source code for this application
* Configure Kubernetes and create a Kubernetes cluster
* Deploy a container using Kubernetes and make a prediction
* Upload a complete Github repo with CircleCI to indicate that your code has been tested

You can find a detailed [project rubric, here](https://review.udacity.com/#!/rubrics/2576/view).

**The final implementation of the project will showcase your abilities to operationalize production microservices.**

---

## Setup the Environment
* Create an ec2 instance with t3.small ami and 30GB storage
* ssh into ec2 instance
* Create a virtualenv with Python 3.7 and activate it. 
```bash
# Use a command similar to this one:
python3 -m venv ~/.devops
source ~/.devops/bin/activate
```
* install git with following commands:
```bash
#Perform a quick update on your instance:
sudo yum update -y
 
#Install git in your EC2 instance
sudo yum install git -y
 
#Check git version
git version
```
* Clone source code repository into ec2 instance

* Run `make install` to install the necessary dependencies

* Install docker on ec2 instance
```bash
#Perform a quick update on your instance:
sudo yum update -y
 
#Install docker in your EC2 instance
sudo yum install docker
 
#Change permission to ec2-user in order to use docker command without sudo
sudo usermod -a -G docker ec2-user
id ec2-user
#Reload a Linux user's group assignments to docker w/o logout
newgrp docker

#Enable docker service at AMI boot time
sudo systemctl enable docker.service
#Start the Docker service
sudo systemctl start docker.service
```

* Install Kubectl on ec2 instance
```bash
#Download the latest release with the command
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
#Make the kubectl binary executable
chmod +x ./kubectl
#Move the binary in to your PATH
sudo mv ./kubectl /usr/local/bin/kubectl
#Test to ensure the version you installed is up-to-date
kubectl version --client
```

* Install Minikube on ec2 instance
```bash
#Install minikube
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
&& chmod +x minikube \
&& sudo mv minikube /usr/local/bin/
#Check minikube version
minikube version
```

* Install Hadolint on ec2 instance
```bash
sudo wget -O ./hadolint https://github.com/hadolint/hadolint/releases/download/v2.10.0/hadolint-Linux-x86_64
sudo chmod +x ./hadolint
sudo mv ./hadolint /usr/local/bin/hadolint
```

### Docker Steps

* Complete Dockerfile
* Complete run_docker.sh
* Build docker and make a prediction
```bash
#Build and run docker
./run_docker.sh
#Make a prediction
./make_prediction.sh
```
* Complete upload_docker.sh and upload docker image to dockerhub
```bash
#Upload docker image to docker hub
./upload_docker.sh
```

### Kubernetes Steps

* Complete run_kubernetes.sh
* Deploy application on kubernetes and make a prediction
```bash
#Deploy application on kubernetes
./run_kubernetes.sh
#Make a prediction
./make_prediction.sh
```
## Directory Structure
* `.circleci/config.yml`: Config file for CircleCI pipeline
* `model_data`: training model data
* `output_txt_files`: log output of docker and kubernetes steps
* `app.py`: main application file
* `Dockerfile`: file to build docker image
* `make_prediction.sh`: bash script to call application's api to make a prediction
* `Makefile`: defines set of task to be executed
* `requirements.txt`: dependencies require to run python application
* `run_docker.sh`: build and run docker image
* `run_kubernetes.sh`: deploy application using kubernetes
* `upload_docker.sh`: upload docker image to dockerhub