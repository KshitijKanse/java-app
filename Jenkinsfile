pipeline {
    agent any
    environment {
        IMAGE_NAME = "mahity123/sample-repo/java-aap"
        IMAGE_TAG  = "latest"
        DOCKERHUB_USERNAME = credentials('mahity123')
        DOCKERHUB_PASSWORD = credentials('Mahity@123')
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                    credentialsId: 'github-token', 
                    url: 'https://github.com/KshitijKanse/java-app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh """
                    docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
                """
            }
        }
        stage('Login to Docker Hub') {
            steps {
                sh """
                    echo "${DOCKERHUB_PASSWORD}" | docker login -u "${DOCKERHUB_USERNAME}" --password-stdin
                """
            }
        }
        stage('Push Image') {
            steps {
                sh """
                    docker push ${IMAGE_NAME}:${IMAGE_TAG}
                """
            }
        }
    }
}
