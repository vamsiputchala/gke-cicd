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

Cicd pipeline to deploy applications on Google Kubernetes Engine using cloud build and cloud deploy.

Mainly using 3 services in GCP:

-GOOGLE KUBERNETES ENGINE

-GOOGLE CLOUD BUILD

-GOOGLE CLOUD DEPLOY: Automates application deployment to a series of target environments like dev, stage, prod. We can setup sequence in delivery pipeline.

## Project Flow: 

1.When user push the code to git hub repo , the configured build trigger , triggers the cloud build.

2.Cloud build , builds the docker image with application code and push the image to Artifact registry and also triggers cloud deploy pipeline.

3.Cloud deploy pipeline deploys latest imagecontainer to dev Kubernetes cluster, if its fine then promotes to staging it is manual intervention, after that to 
  production with approval from staging.cloud deploy uses scaffold file for rendering deployment and verification.


## Steps:

1.Go to Kubernetes engine create 2 clusters

   cluster1- dev cluster
   
   cluster2- prod cluster   


2. We can create delivery pipe line by yaml file code.

3.create build trigger to trigger cloud build while push code to git hub.
  cloud build ---> triggers ---> create trigger
event ---> push to branch

source 1st gen 
repository add repo add GitHub account and authorize



configuration

cloud build configuration file

location repository
file location   cloudbuild.yaml

configure service account 

create

## cloudbuild.yaml file

step1 : build docker image from app folder with dockerfile in app1 folder

step2 : pushing docker image to artifact registery

step3: build docker image from app folder with dockerfile in app2 folder


step4: pushing docker image to artifact registery


step5 :/ executing gcloud deploy apply ---> in deploy folder pipeline.yaml file

         here we are deploying delivery pipeline from script instead of manual

           in dev.yaml creating a dev target pointed to cluster1
           
            prod.yaml creating a prod target pointed to cluster2 


step 6
this step create release 1st release for app1.yaml

app1.yaml--->deploying container image latest and expose as a service

app2.yaml--->deploying container image latest and expose as a service


As soon as push the change to git hub , cloud build pipeline start
 and create docker images with docker file in app1 & app2 and the images push to artifact registry then code deploy starts and deploys build container image and 
  1st deploys in dev after approve will deploy in prod



