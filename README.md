## Automated Container Deployment with GitHub Actions CI/CD to AWS ECS Fargate 

![image_alt]()

## Background
As part of my cloud and DevOps engineering journey, I wanted to build a real-world CI/CD pipeline that showcases my ability to:
1.Provision infrastructure as code using **Terraform**

2.Set up a secure, scalable container deployment using **AWS ECS Fargate**

3.Automate testing and deployment using **GitHub Actions**

This project demonstrates a production-ready deployment pipeline for a Java application using modern DevOps practices and tools.

## Project Overview
This project contains a complete CI/CD pipeline for a containerized Java application. It includes:
1.Infrastructure provisioning with Terraform

2.Java app packaged with Docker

3.CI/CD using GitHub Actions

4.Deployment to AWS ECS Fargate

5.Logging with Amazon CloudWatch

6.Load balancing with ALB

7.Private/public subnet isolation

8.Store docker images with ECR

## Project Objectives
1.Automate infrastructure provisioning using Terraform

2.Deploy Java app container to AWS ECS Fargate

3.Ensure zero-downtime deployments with ECS service updates

4.Implement CI/CD with GitHub Actions

5.Apply secure secret management using GitHub Secrets

6.Store logs in Amazon CloudWatch for observability

##  Features
1.Fully automated CI/CD pipeline with GitHub Actions

2.Build and test Java application on every commit

3.Push Docker images to Amazon ECR

4.Deploy to ECS Fargate with zero manual steps

5.Logs accessible in CloudWatch

6.Highly available architecture with ALB & VPC isolation


## Technologies Used
1.AWS ECS Fargate- Serverless container hosting  

2.Amazon ECR- Docker image registry   

3.GitHub Actions- CI/CD automation  

4.Terraform- Infrastructure as Code 

5.CloudWatch Logs- Logging and observability 

6.Docker- Containerization  

7.ALB, VPC, Subnets- Networking and Load Balancing   

8.Java (Spring Boot)- Backend Application                  


##  Use Case
You work as Devops Engineer at Up the Chels Corp and run a cloud-based Java microservice that needs automatic deployment to a scalable, fault-tolerant infrastructure. Perfect for **startups**, **enterprise microservices**, or **DevOps learning labs**.

## Prerequisites
1.AWS Account with admin permissions

2.[AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) configured (`aws configure`)

3.Terraform installed

4.Docker installed

5.GitHub repository with secrets:
  - `AWS_ACCESS_KEY_ID`
  - `AWS_SECRET_ACCESS_KEY`
  - `ECR_URI`
  - `TASK_FAMILY`
  - `ECS_CLUSTER_NAME`
  - `ECS_SERVICE_NAME`

## Step 0: Clone the Repository
Clone this repository to your local machine.
```language
git clone https://github.com/Tatenda-Prince/Automated-Container-Deployment-with-GitHub-Actions-CI-CD-to-AWS-ECS-Fargate.git
```

## Step 1: Create a ECR Repository 
1.1.Before Terraform provisons AWS resources we need to push your application Docker image to ECR, so we need to build and push docker images to Amazon ECR:
```language
aws ecr create-repository --repository-name your-repository-name

aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <YOUR ACCOUNT ID>.dkr.ecr.us-east-1.amazonaws.com

docker build -t my-java-app .

docker tag my-node-app:latest <ECR_URI>:latest

docker push <ECR_URI>:latest
```
![image_alt]()

## Step 2 : Run Terraform workflow to initialize, validate, plan then apply
2.1.Terraform will provision:

1.ECS Cluster, Task Definition, and Service

2.Load Balancer & Target Group

3.ECR Repository for container storage

4.IAM roles for security

5.VPC, Subnets, NAT GW, IGW

2.2.In your local terraform visual code environment terminal, to initialize the necessary providers, execute the following command in your environment terminal
```language
terraform init
```
Upon completion of the initialization process, a successful prompt will be displayed, as shown

![image_alt]()

2.3.Next, let’s ensure that our code does not contain any syntax errors by running the following command
```language
terraform validate
```
The command should generate a success message, confirming that it is valid, as demonstrated below.

![image_alt]()

2.4.Let’s now execute the following command to generate a list of all the modifications that Terraform will apply.
```language
terraform plan
```

![image_alt]()

The list of changes that Terraform is anticipated to apply to the infrastructure resources should be displayed. The “+” sign indicates what will be added, while the “-” sign indicates what will be removed.

2.5.Now, let’s deploy this infrastructure! Execute the following command to apply the changes and deploy the resources. Note — Make sure to type “yes” to agree to the changes after running this command.
```language
terraform apply
```



