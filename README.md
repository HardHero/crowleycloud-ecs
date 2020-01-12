# Crowley.Cloud with AWS ECS

This repo uses AWS Cloudformation to deploy a website in ECS. It is based on the directions written here:

https://milapneupane.com.np/2019/07/28/how-to-deploy-a-docker-container-with-aws-ecs-using-cloudformation/

## Pre-reqs

Install ecs-deploy

        pip install ecs-deploy

To run any of the `Jenkinsfile*` you need a jenkins instance with the appropriate jenkins pipeline jobs.
        
## How to set the stacks up

1. To Start:
        
        aws cloudformation create-stack --stack-name crowley-cloud-ecr --template-body file://ecr.yml

        aws cloudformation create-stack --stack-name crowley-cloud-loadbalancer --template-body file://loadbalancer.yml

        aws cloudformation create-stack --stack-name crowley-cloud-ecs --capabilities CAPABILITY_IAM --template-body file://ecs.yml

2. To Update:
        
        aws cloudformation update-stack --stack-name crowley-cloud-ecr --template-body file://ecr.yml

        aws cloudformation update-stack --stack-name crowley-cloud-loadbalancer --template-body file://loadbalancer.yml

        aws cloudformation update-stack --stack-name crowley-cloud-ecs --template-body file://ecs.yml

## Using it in Jenkins

There are Jenkinsfile for ECR/ELB and the ECS stacks respectively.