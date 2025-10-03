pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "webapp:latest"
        CONTAINER_NAME = "webapp-container"
        TOMCAT_PORT = "8080"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Charan290403/ci_cd_pipeline.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('Stop Existing Container') {
            steps {
                sh "docker stop ${CONTAINER_NAME} || true"
                sh "docker rm ${CONTAINER_NAME} || true"
            }
        }

        stage('Run Docker Container') {
            steps {
                sh "docker run -d -p ${TOMCAT_PORT}:8080 --name ${CONTAINER_NAME} ${DOCKER_IMAGE}"
            }
        }
    }
}
