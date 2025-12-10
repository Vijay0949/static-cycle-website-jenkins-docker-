pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pull code from GitHub
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                // Ignore error if container doesn't exist
                sh 'docker stop myapp || true'
                sh 'docker rm myapp || true'
            }
        }

        stage('Run New Container') {
            steps {
                // Map EC2 port 1111 -> container port 80
                sh 'docker run -d --name myapp -p 1111:80 myapp:latest'
            }
        }
    }
}
