pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "vanshika123/myapp"
        DOCKER_TAG   = "latest"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-creds') {
                        def image = docker.image("${DOCKER_IMAGE}:${DOCKER_TAG}")
                        image.push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo "✅ Docker image pushed successfully to Docker Hub"
        }
        failure {
            echo "❌ Docker build or push failed"
        }
    }
}
