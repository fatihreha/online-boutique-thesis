pipeline {
    // İşi, 'windows' etiketli agent'ımızda çalıştır diyoruz.
    agent {
        label 'windows'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // 1. Adım: GitHub deponuzdaki kodu indirir.
                checkout scm
            }
        }

        stage('Set up Minikube Docker environment') {
            steps {
                // 2. Adım: Windows'ta çalıştığımız için 'powershell' kullanıyoruz.
                powershell 'minikube -p minikube docker-env --shell powershell | Invoke-Expression'
            }
        }

        stage('Build Docker image for productcatalogservice') {
            steps {
                // 3. Adım: productcatalogservice için Docker imajını oluşturur.
                powershell 'docker build -t productcatalogservice:latest ./src/productcatalogservice'
            }
        }

        stage('Deploy to Minikube') {
            steps {
                // 4. Adım: Minikube'daki mevcut deployment'ı yeni imajla günceller.
                powershell 'kubectl set image deployment/productcatalogservice server=productcatalogservice:latest'
            }
        }
    }
}