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
                    // Define the dockerImage variable here
                    def dockerImage = docker.build('website:latest', "-f website/Dockerfile .")
                }
                // This stage will end, but the dockerImage variable is still accessible
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    // Access the dockerImage variable defined in the previous stage
                    dockerImage.run('-p 8081:80 -d')
                }
            }
        }
    }
    
    post {
        always {
            script {
                // Access the dockerImage variable for cleanup
                dockerImage.stop()
                dockerImage.remove()
            }
        }
    }
}

