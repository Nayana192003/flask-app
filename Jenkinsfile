pipeline {
    agent any

    environment {
        IMAGE_NAME = 'flask-app'
        CONTAINER_NAME = 'flask-container'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Nayana192003/flask-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat 'docker build -t flask-app .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    bat 'docker run -d -p 5000:5000 --name flask-container flask-app'
                }
            }
        }
    }

    post {
        failure {
            script {
                bat 'docker stop flask-container || echo "Container not running"'
                bat 'docker rm flask-container || echo "Container not found"'
                bat 'docker rmi flask-app || echo "Image not found"'
            }
        }
    }
}
