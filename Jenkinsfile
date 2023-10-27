pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Check out your GitHub repository
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Build the Docker image using the Dockerfile in the 'website' directory
                script {
                    def dockerImage = docker.build('website:latest', "-f website/Dockerfile .")
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                // Run the Docker container, mapping port 8081 to 80
                script {
                    dockerImage.run('-p 8081:80 -d')
                }
            }
        }
    }
    
    post {
        always {
            // Clean up - stop and remove the container
            script {
                dockerImage.stop()
                dockerImage.remove()
            }
        }
    }
}
