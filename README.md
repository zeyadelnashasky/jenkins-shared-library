# CI/CD Pipeline with Jenkins Shared Library
-------------------------------------------

This project implements a CI/CD pipeline using Jenkins, organized through a shared library approach. The key components are:
A central Shared Library Repo that contains the pipeline logic, built-in stages, and common steps.
Three individual Service Repos: Each of these repositories connects to the shared library to reuse pipeline logic, while having custom environment variables to define their unique behaviors.


# Structure
---------

1- Shared Library Repo:

This repo holds all the pipeline code and reusable functions.
It is imported by each of the other service repos through their Jenkinsfile.


2- Service Repos:

These are three separate repositories: petclinic-service-1, petclinic-service-2, petclinic-service-3.
In each of these repos, I added a Dockerfile to build the application.
Each repo has its own Jenkinsfile that references the shared library.
Within each Jenkinsfile, environment variables are used to customize the behavior for each service.


# Jenkins Setup
--------------

1- I created three separate Jenkins jobs on the Jenkins server—one for each service.

2- Each job is configured with the GitHub repository link of its respective service (e.g., petclinic-service-1, petclinic-service-2, petclinic-service-3).

3- From these jobs, I triggered the pipeline runs to validate the process.

4- After the pipeline succeeded, the Dockerfile in each repo built an image.

5- I pushed the image to my Docker Hub using credentials stored in Jenkins.

6- After the image was uploaded, it was pulled (via polling) on the target Jenkins server.

7- The service container ran with the application on the following ports: petclinic-service-1 on port 9090, petclinic-service-2 on port 9091, and petclinic-service-3 on port 9092.

8- All services were tested and confirmed to be running successfully on their respective ports, accessible via the IP address of my Jenkins server.


# GitHub Repositories
---------------------

Shared Library Repo: https://github.com/zeyadelnashasky/jenkins-shared-library

petclinic-service-1: https://github.com/zeyadelnashasky/spring-petclinic-service-1

petclinic-service-2: https://github.com/zeyadelnashasky/spring-petclinic-service-2

petclinic-service-3: https://github.com/zeyadelnashasky/spring-petclinic-service-3


# 🐳 Docker Images
-------------------

zeyadelnashashky/service-1 --> docker pull zeyadelnashashky/service-1:latest 

zeyadelnashashky/service-2 --> docker pull zeyadelnashashky/service-2:latest 

zeyadelnashashky/service-3 --> docker pull zeyadelnashashky/service-3:latest 


# Tech Stack
----------
1- Jenkins (CI/CD)

2- Docker

3- Maven

4- Spring Boot

5- JDK-17


- Quick Note: you can work with these images on your kubernetes cluster to maintain the deployment and orchestration, 
also you could observe the cluster (cpu, ram, storage, pods, nodes, etc) by using lens software, which you can connect your cluster to it to visualize your kubernetes cluster by inserting your kubeconfig file in it to connect your cluster effectively. 

# Getting Started
----------------

1- Clone each of the service repos.

2- Ensure that Jenkins server is configured with your Docker Hub credentials.

3- Customize environment variables in each service Jenkinsfile as needed in each repo.

4- Create three Jenkins jobs on jenkins server, each pointing to its respective repo link.

5- Run the pipeline from Jenkins to observe the automated build, test, and deployment.

6- After a successful build, the Docker image is pushed to Docker Hub.

7- The image is then pulled and run as a container on the target Jenkins server, with services running on ports 9090, 9091, and 9092 respectively.

8- To run your application, open your browser on jenkins server and write this url: [http://YOUR_JENKINS_IP_SERVER:PORT_NUMBER] to visualize your application.
