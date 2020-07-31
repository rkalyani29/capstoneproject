# CapstoneProject
Cloud DevOps Capstone Project

## Project Overview

> In this project, I applied my skills and knowledge which I learnt throughout the Cloud DevOps Nanodegree program.

## Project Tasks:

* Working in AWS
* Using Jenkins to implement Continuous Integration and Continuous Deployment
* Building pipelines
* Working with CloudFormation to deploy clusters
* Building Kubernetes clusters
* Building Docker containers in pipelines

## About Project: 

> I created a CI/CD pipeline for a basic website that deploys to a cluster in AWS EKS which is Blue/Green Deployment.

## Project Files

## infrastructure

This folder all the files related to infrastructure deployment.

-   `jenkins-server.yml`--> CloudFormation script for creating jenkins server.
-   `jenkins-server-parameters.json`: Parameters file for cloud formation stack.
-   `Jenkinsfile`: Jenkinsfile for creating EKS cluster and configuring kubectl.

## kubernetes-resources

This folder contains all template files for Kubernetes resources.

-   `blue-deployment.yml`, `green-deployment.yml`: A replication controller template which creates pods .
-   `green-service.yml`, `blue-service.yml` : blue and green Service templates .

#### screenshots

This folder contains all screenshots taken during creation of this project.


#### Dockerfile

This is Dockerfile of application.

#### index.html

This is main html file of application.

#### Jenkinsfile

This file contains the steps of CICD pipeline of application.

## STEPS

-   Create Jenkins server using cloud formation template.

```
$ sh scripts/createstack.sh jenkins infra/jenkins-server.yml infra/jenkins-server-parameters.json
```

-    after executing above command the resources VPC, Subnet, Route Table, Internet Gateway, Security Group, Launch Configuration will be created. And the tools Jenkins, Docker
-   AWS CLI, eksctl CLI, kubectl CLI and Tidy are automatically installed in the server using Launch Configuration.

-   Once the stack creation is complete, access the Jenkins UI using `http://<EC2_PUBLIC_IP>:8080`
-   Login using admin account and complete the initial setup of Jenkins.
-   Install the following plugins in Jenkins:
    -   CloudBees AWS Credentials
    -   Pipeline: AWS Steps
    -   Blue Ocean
-   Add AWS credentials in Jenkins.
-   Create `jenkins_pipeline`
-   Add the configuration for `jenkins_pipeline`, provide the GitHub repository as `https://github.com/rkalyani29/capstoneproject/` and script path as `infra/Jenkinsfile`
-   Click on `Build Now` to trigger the pipeline.
-   This pipeline 
    -   Creates a EKS cluster
    -   Configures kubectl which helps us to connect to EKS cluster
-   Add Docker Hub credentials in Jenkins so that we can push docker image to Docker Hub.
-   Create a new pipeline `capstone_pipeline`
-   Add the configuration for `capstone_pipeline`, provide the GitHub repository as `https://github.com/rkalyani29/capstoneproject/` and script path as `Jenkinsfile`
-   Apply and save the pipeline.
-   `Build Now` to trigger the pipeline
-   Once the pipeline is successful, go to Load Balancer page in AWS console and look for DNS name
-   Copy the DNS name `a25ba6e21d36311ea867406b0d65202e-797585048.us-west-2.elb.amazonaws.com`
-   In the browser, open a new tab and hit link as `http://<DNS_NAME>:8000/`. It will show the capstone project website as per the screenshot `My website`.


