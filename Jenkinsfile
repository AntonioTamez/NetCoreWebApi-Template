pipeline {
    agent any
    environment {
        DOTNET_VERSION = '8.0'
        IMAGE_NAME = 'netcore-api'
        CONTAINER_NAME = 'netcore-api-container'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/AntonioTamez/NetCoreWebApi-Template.git'
            }
        }
        stage('Build') {
            steps {
                sh 'dotnet build --configuration Release'
            }
        }
        stage('Test') {
            steps {
                sh 'dotnet test --logger trx'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Docker Run') {
            steps {
                sh 'docker stop $CONTAINER_NAME || true'
                sh 'docker rm $CONTAINER_NAME || true'
                sh 'docker run -d --name $CONTAINER_NAME -p 5000:5000 $IMAGE_NAME'
            }
        }
    }
}
