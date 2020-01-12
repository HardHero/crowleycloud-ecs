pipeline {
    agent any
    parameters{
        string(name:'IMAGE_NAME', defaultValue: '', description: 'ECR Registry')
    }
    stages {
        stage('Build Docker'){
            steps{
                script{
                    image = docker.build("${IMAGE_NAME}")
                }
            }
        }
        stage('Push Docker'){
            steps{
                script{
                    sh "eval `aws ecr get-login --no-include-email`"
                    image.push('latest')
                }
            }
        }
        stage('Update ECS Cloudformation Stack'){
            steps{
                withAWS(region:'us-east-1', profile:'default') {
                    cfnUpdate(
                        stack:"crowley-cloud-ecs", 
                        file:'ecs.yml', 
                    )
                }
            }
        }
        stage('Update ECS cluster with new image'){
            steps{
                sh 'ecs deploy CrowleyCloudECSCluster crowley-cloud-service'
            }
        }
    }
}