pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build and Push Docker Image') {
            steps {
                sh 'docker build -t gcr.io/reflected-coder-397313/hello-gke:$BUILD_NUMBER .'
                sh 'gcloud auth configure-docker'
                sh 'docker push gcr.io/reflected-coder-397313/hello-gke:$BUILD_NUMBER'
            }
        }
        stage('Deploy to GKE') {
            steps {
                sh 'kubectl apply -f path/to/kubernetes/deployment.yaml'
                sh 'kubectl apply -f path/to/kubernetes/service.yaml'
            }
        }
    }
}
