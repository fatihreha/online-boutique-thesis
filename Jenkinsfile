pipeline {
    // Bu pipeline'ın nerede çalışacağını belirtir. 
    // 'any', herhangi bir uygun Jenkins agent'ında çalışabilir demektir.
    agent any

    // Otomasyonun adımlarını (aşamalarını) tanımlar.
    stages {
        stage('Checkout Code') {
            steps {
                // 1. Adım: GitHub deponuzdaki kodu indirir.
                checkout scm
            }
        }
        
        stage('Set up Minikube Docker environment') {
            steps {
                // 2. Adım: Docker komutlarının Minikube'un içindeki Docker'a gönderilmesini sağlar.
                // PowerShell komutu olduğu için 'powershell' adımı içinde çalıştırıyoruz.
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
                // 4. Adım: Minikube'daki mevcut deployment'ı yeni oluşturduğumuz imajla günceller.
                powershell 'kubectl set image deployment/productcatalogservice server=productcatalogservice:latest'
            }
        }
    }
}
