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

                    def existingContainers = sh(script: "docker ps -a --format '{{.Names}}'", returnStdout: true).trim()

                    if (existingContainers.contains('backend')) {
                        sh "docker stop backend"
                        sh "docker rm backend"
                    }

                    sh "docker run -d -p 3000:3000 --name backend backend"
                }
            }
        }
    }
}