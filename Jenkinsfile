pipeline {
    agent {
        label 'windows'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        
        stage('Set up Minikube Docker environment') {
            steps {
                powershell 'minikube -p minikube docker-env --shell powershell | Invoke-Expression'
            }
        }

        stage('Build Docker image for shippingservice') {
            steps {
                powershell 'docker build -t shippingservice:latest ./src/shippingservice'
            }
        }
        
        stage('Deploy to Minikube') {
            steps {
                powershell 'kubectl set image deployment/shippingservice server=shippingservice:latest'
            }
        }
    }
}