pipeline {
    agent any

    environment {
        registry = '939083599624.dkr.ecr.us-east-1.amazonaws.com/node-frontend'
        registryCredential = 'challenge'
        dockerImage = ''
    }
    stages {
        stage ('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/Freensh/Node-challenge-frontend.git'
            }
        }

        stage ('Install dependencies'){
            steps {
                sh 'npm install'
            }
        }
        stage ('Build docker container') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Push Image to ECR') {
            steps {
                script {
                    docker.withRegistry("https://"+registry, "ecr:us-east-1:"+registryCredential){
                        dockerImage.push()
                    }
                }
            }
        }
    }
}