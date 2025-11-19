pipeline {
    agent any
    environment {
        REGISTRY = "hub.docker.com"
        IMAGE_NAME = "mahity123/sample-repo/java-aap"
        IMAGE_TAG = "latest"
        DOCKERHUB_USERNAME = credentials('mahity123')
        DOCKERHUB_PASSWORD = credentials('Mahity@123')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
            }
        }

        stage('Login to Docker') {
            steps {
                sh 'echo "$DOCKERHUB_PASSWORD" | docker login -u "$DOCKERHUB_USERNAME" --password-stdin'
                sh 'docker push ${IMAGE_NAME}:${IMAGE_TAG}'
            }
        }
    }
}
