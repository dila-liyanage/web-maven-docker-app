pipeline {
    agent any

    tools {
        maven 'MAVEN3'
    }

    environment {
        DOCKER_USERNAME = 'dilshanliyanage1000'
        DOCKER_IMAGE = 'dilshanliyanage1000/web-maven-docker-app'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Maven Project') {
            steps {
                bat 'mvn clean install'
            }
        }
        stage('Docker Login') {
            steps {
                withCredentials([string(credentialsId: 'DockerHub_Pwd', variable: 'DOCKER_PASSWORD')]) {
                    bat """
                    echo \$DOCKER_PASSWORD | docker login -u \$DOCKER_USERNAME --password-stdin
                    """
                }
            }
        }

        stage('Docker Build') {
            steps {
                bat "docker build -t ${DOCKER_IMAGE}:latest ."
            }
        }

        stage('Docker Push') {
            steps {
                bat "docker push ${DOCKER_IMAGE}:latest"
            }
        }
    }
}
