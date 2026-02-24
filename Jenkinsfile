pipeline {
    agent any

    environment {
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nesths-image"
        EMAIL = "ritikrawat2002@gmail.com"
        PORT = "3000"
    }

    stages {
        stage('Clone Repo') {
            steps{
                git branch: 'main',
                url: 'https://github.com/hri1/CICD-jenkins-aws-email.git'
            }
        }

        stage('Build Docker Image'){
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop & Remove Previous Container') {
            steps {
                sh '''
                   docker stop $CONTAINER_NAME || true
                   docker rm $CONTAINER_NAME || true
                  ''' 
            }
        }

        stage('Docker Container Run'){
            steps {
                sh '''
                  docker run -d -p ${PORT}:${PORT} $CONTAINER_NAME $IMAGE_NAME
                  '''
            }
        }
        stage('Send Email Notification'){
            steps {
                emailext(
                    subject: "Nestjs App Deployed Successfully on EC2!",
                    body: "Your Nest JS app is Deployed1 http://13.53.174.188:${PORT}/",
                    to: "${EMAIL}"
                )
            }
        }
    }
}