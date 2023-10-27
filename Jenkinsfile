def dockerImage // Define the dockerImage variable at the top level

pipeline {
    agent any
    
    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    dockerImage = docker.image('the127terminal/new:latest')
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    dockerImage.run("-p 8081:80 -d")
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

