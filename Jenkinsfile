pipeline {
    agent any

    environment {
        IMAGE_NAME = "password-checker"
    }

    stages {
       
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerbubpwd')]) {
                    sh 'docker login -u sivanandhini23 -p $(dockerbubpwd)'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }
    }
}
