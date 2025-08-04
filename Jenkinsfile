pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-new-docker-app'
        DOCKER_HUB_USER = 'sanjub07'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/Sanjaykumar-2708/my-new-docker-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Login to Docker Hub and Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                    bat "docker tag %IMAGE_NAME% %DOCKER_HUB_USER%/%IMAGE_NAME%:latest"
                    bat "docker push %DOCKER_HUB_USER%/%IMAGE_NAME%:latest"
                }
            }
        }
    }
}
