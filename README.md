# CI/CD Pipeline for Deploying Applications on Google Kubernetes Engine (GKE).....


## Introduction

In the modern software development landscape, Continuous Integration/Continuous Deployment (CI/CD) pipelines play a pivotal role in automating the process of building, testing, and deploying applications. In this blog post, we’ll deep dive into the implementation of a robust CI/CD pipeline to deploy applications on Google Kubernetes Engine (GKE) using Google Cloud Build and Cloud Deploy services.


## Requirements

To achieve our goal, we have the following requirements:
- Deployment of two simple Flask applications (app1 & app2) on the GKE clusters.
- Automation of the entire deployment process, triggered by a developer’s code push.
- Dev-cluster deployment precedes production deployment, allowing for review before promoting to the prod-cluster.

## Architecture
![gke-arche](https://github.com/user-attachments/assets/d0d1e1a4-7d80-4687-b4cf-80e668fc701b)


## Technical Stack Summary

This CI/CD pipeline leverages several key components:
- Google Kubernetes Engine (GKE): Google’s managed Kubernetes service, providing a scalable and reliable platform for deploying containerized applications.
- Cloud Build: A fully managed continuous integration and continuous delivery platform that allows developers to build, test, and deploy applications on Google Cloud Platform.
- Cloud Deploy: A service for continuous delivery that automates the deployment of containerized applications to Google Kubernetes Engine and other platforms.
- GitHub: A popular version control platform where developers collaborate, manage, and version control their codebase.

## Solution

We are going to implement the solution using the following steps to implement the CI/CD pipeline for deploying applications on GKE:

1. Create two simple Flask applications (app1 & app2).
2. Set up a GitHub repository and push the application code.
3. Create two GKE clusters: dev-cluster and prod-cluster, using Google Kubernetes Engine.
4. Create Kubernetes manifest files in the Kubernetes folder to deploy the application and expose it as a service.
5. Create skaffold.yaml file now.
6. Now Create cloudbuild.yaml file to build and push docker images to Artifact registry for both application and Configure a Cloud Build trigger to initiate the pipeline upon code push events in the GitHub repository.
7. Implement the necessary code to define the Cloud Deploy pipeline and targets for both dev-cluster and prod-cluster.
8. Push the updated code to the GitHub repository, triggering the Cloud Build and Cloud Deploy processes.

   
## Steps to Execute

cicd pipeline to deploy applications on gke using cloud build and cloud deploy

flow: user push the code to git hub repo , once push with configured build trigger , triggers the cloud build 
cloud build , builds the docker image with application code and push the image to artifact registry and also triggers cloud deploy pipeline

cloud deploy pipeline deploys latest imagecontainer to dev Kubernetes cluster, if its fine then promotes to staging it is manual intervention, after that to production with approval from staging.

Mainly using 3 services in gcp
GOOGLE KUBERNETES ENGINE
GOOGLE CLOUD BUILD
GOOGLE CLOUD DEPLOY: Automates application deployment to a series of target environments like dev, stage, prod
we can setup sequence in delivery pipeline

cloud deploy uses scaffold file for rendering deployment and verification


