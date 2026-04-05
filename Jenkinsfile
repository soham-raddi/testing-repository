pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "sohamraddi/python-app"
    }

    stages {

        stage('Build Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE%:latest .'
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run --rm %DOCKER_IMAGE%:latest'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    bat 'echo %PASS% | docker login -u %USER% --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                bat 'docker push %DOCKER_IMAGE%:latest'
            }
        }
    }
}
