pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Set up Minikube Docker environment') {
            steps {
                // DEĞİŞİKLİK: 'powershell' yerine 'sh' kullanıyoruz ve komut Linux için uyarlandı.
                sh 'eval $(minikube -p minikube docker-env)'
            }
        }

        stage('Build Docker image for productcatalogservice') {
            steps {
                // DEĞİŞİKLİK: 'powershell' yerine 'sh' kullanıyoruz.
                sh 'docker build -t productcatalogservice:latest ./src/productcatalogservice'
            }
        }

        stage('Deploy to Minikube') {
            steps {
                // DEĞİŞİKLİK: 'powershell' yerine 'sh' kullanıyoruz.
                sh 'kubectl set image deployment/productcatalogservice server=productcatalogservice:latest'
            }
        }
    }
}