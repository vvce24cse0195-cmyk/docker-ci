pipeline {
    agent any

    environment {
        REGISTRY = "localhost:5000"
        IMAGE_NAME = "anil-demo-app"
    }

    stages {

        stage('1. Application Build & Test') {
            steps {
                bat 'python --version'
                bat 'python -m py_compile app.py'
            }
        }

        stage('2. Build & Tag Docker Image') {
            steps {
                bat "docker build -t ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER} -t ${REGISTRY}/${IMAGE_NAME}:latest ."
            }
        }

        stage('3. Push Image to Registry') {
            steps {
                bat "docker push ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER}"
                bat "docker push ${REGISTRY}/${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        success {
            echo "Pipeline succeeded! Docker image pushed successfully."
        }
    }
}
