pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', 
                          branches: [[name: '*/main']],
                          userRemoteConfigs: [[url: 'https://github.com/luchobennu/test.git']]])
            }
        }
        
        stage('Build and Deploy') {
            steps {
                script {
                    sh "docker build . -t backend"
                    sh "docker-compose down"
                    sh "docker-compose up -d"
                }
            }
        }
    }
}