pipeline {
    agent any

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
    }
}
