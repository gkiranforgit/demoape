pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'myacr123.azurecr.io/simple-webapp:latest'
        AZURE_CREDENTIALS = credentials('azure-credentials-id')
    }
    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/your_username/simple-webapp.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
        stage('Push to ACR') {
            steps {
                script {
                    sh 'docker login $DOCKER_IMAGE -u $AZURE_CREDENTIALS_USR -p $AZURE_CREDENTIALS_PSW'
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
        stage('Deploy to AKS') {
            steps {
                script {
                    sh 'kubectl apply -f deployment.yaml'
                    sh 'kubectl apply -f service.yaml'
                }
            }
        }
    }
}
