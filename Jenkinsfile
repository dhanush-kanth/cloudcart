pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/dhanush-kanth/cloudcart.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'sudo docker build -t cloudcart:latest .'
            }
        }

        stage('Verify Docker Image') {
            steps {
                sh 'sudo docker images cloudcart'
            }
        }
    }
}
