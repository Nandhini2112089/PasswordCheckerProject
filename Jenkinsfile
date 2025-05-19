pipeline {
    agent any

    environment {
        IMAGE_NAME = "password-checker"
    }

    stages {
        stage('Check Docker Access') {
            steps {
                sh 'docker --version'
                sh 'docker ps'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Login to Docker Hub') {
    steps {
        sh 'docker login -u sivanandhini23 -p Nandhini23'
    }
}


        stage('Push Docker Image') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }
    }
}
