pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t jsf-app .'
            }
        }
        
        stage('Deploy') {
            steps {
                bat 'docker-compose down || exit 0'
                bat 'docker-compose up -d'
            }
        }
    }
}
