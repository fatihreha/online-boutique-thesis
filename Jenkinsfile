pipeline {
    // İşi, 'windows' etiketli agent'ımızda çalıştır diyoruz.
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
                // DEĞİŞİKLİK: Windows'ta çalıştığımız için tekrar 'powershell' kullanıyoruz.
                powershell 'minikube -p minikube docker-env --shell powershell | Invoke-Expression'
            }
        }

        stage('Build Docker image for productcatalogservice') {
            steps {
                // DEĞİŞİKLİK: 'powershell' kullanıyoruz.
                powershell 'docker build -t productcatalogservice:latest ./src/productcatalogservice'
            }
        }

        stage('Deploy to Minikube') {
            steps {
                // DEĞİŞİKLİK: 'powershell' kullanıyoruz.
                powershell 'kubectl set image deployment/productcatalogservice server=productcatalogservice:latest'
            }
        }
    }
}