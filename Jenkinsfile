def dockerImage // Define the dockerImage variable at the top level

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
                script {
                    dockerImage = docker.build('website:latest', "-f website/Dockerfile .")
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    dockerImage.run('-p 8081:80 -d')
                }
            }
        }
    }
    
    post {
        always {
            script {
                // Access the global dockerImage variable for cleanup
                dockerImage.stop()
                dockerImage.remove()
            }
        }
    }
}

