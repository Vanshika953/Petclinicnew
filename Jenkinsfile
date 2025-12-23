pipeline {
    agent any

    tools {
        jdk 'JAVA'
        maven 'MAVEN'
    }

    environment {
        IMAGE_NAME = "vanshika693/petclinic"
    }

    stages {
        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

stage('Build & Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-creds') {
                        def app = docker.build("vanshika123/myapp:latest")
                        app.push()
                    }
                }
            }    }
}
