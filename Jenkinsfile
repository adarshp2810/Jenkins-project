pipeline {
    agent any

    environment {
        DOCKER_IMAGE_USER = '<your-dockerhub-username>'
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull the latest code from GitHub
                git 'https://github.com/your-repo/microservices.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build Docker images for both services
                    sh 'docker build -t ${DOCKER_IMAGE_USER}/user-service ./user-service'
                    sh 'docker build -t ${DOCKER_IMAGE_USER}/order-service ./order-service'
                }
            }
        }

        stage('Push Docker Images') {
            steps {
                script {
                    // Push Docker images to Docker Hub
                    sh 'docker push ${DOCKER_IMAGE_USER}/user-service'
                    sh 'docker push ${DOCKER_IMAGE_USER}/order-service'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Pull and deploy Docker images on your server or cloud environment
                    // You can use Docker commands to deploy the services or Kubernetes if you have it set up
                    sh 'docker run -d -p 3000:3000 ${DOCKER_IMAGE_USER}/user-service'
                    sh 'docker run -d -p 3001:3001 ${DOCKER_IMAGE_USER}/order-service'
                }
            }
        }
    }
}
