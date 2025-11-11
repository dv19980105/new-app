pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-demo"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Deploy to k3d') {
            steps {
                sh "k3d image import ${IMAGE_NAME}:latest"
                sh "kubectl apply -f k8s/deployment.yaml"
                sh "kubectl apply -f k8s/service.yaml"
                sh "kubectl get pods"
            }
        }
    }
}
