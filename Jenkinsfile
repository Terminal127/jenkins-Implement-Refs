pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build and Deploy NGINX') {
            steps {
                script {
                    // Run NGINX container on port 8081
                    sh "docker run -d -p 8081:80 --name my-nginx nginx"
                }
            }
        }
    }
    
    post {
        always {
            script {
                // Remove the "Stop NGINX" stage if you want to stop it manually
            }
        }
    }
}

