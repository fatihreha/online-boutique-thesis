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

        stage('Build Docker images') {
            steps {
                powershell '''
                    echo "Building productcatalogservice..."
                    docker build -t productcatalogservice:latest ./src/productcatalogservice
                    echo "Building frontend..."
                    docker build -t frontend:latest ./src/frontend
                '''
            }
        }
        
        stage('Deploy to Minikube') {
            steps {
                powershell '''
                    echo "Deploying productcatalogservice..."
                    kubectl set image deployment/productcatalogservice server=productcatalogservice:latest
                    echo "Deploying frontend..."
                    kubectl set image deployment/frontend server=frontend:latest
                '''
            }
        }
    }
}