pipeline {
    agent any

    tools {
        maven 'MAVEN3'
    }

    environment {
        DOCKER_PASSWORD = credentials('DockerHubPassword')
        DOCKER_IMAGE = 'dilshanliyanage1000/web-maven-docker-app'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/dila-liyanage/web-maven-docker-app.git'
            }
        }
        stage('Build Maven Project') {
            steps {
                bat "mvn clean install"
            }
        }
        stage('Unit Test') {
            steps {
                bat "mvn test"
            }
        }
        stage('Docker Login') {
            steps {
                bat "docker login -u dilshanliyanage1000 -p ${DOCKER_PASSWORD}"
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
