pipeline {
    agent any
    environment {
        KUBECONFIG = '/var/lib/jenkins/.kube/config'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t cloudcart:latest .'
            }
        }
        stage('Verify Docker Image') {
            steps {
                sh 'docker images cloudcart'
            }
        }
        stage('Import Image into Kubernetes') {
            steps {
                sh '''
                    docker save cloudcart:latest -o /tmp/cloudcart.tar
                    sudo k3s ctr images import /tmp/cloudcart.tar
                '''
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    kubectl rollout restart deployment/cloudcart
                    kubectl rollout status deployment/cloudcart --timeout=120s
                    kubectl get pods,svc
                '''
            }
        }
    }
}
