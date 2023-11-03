def dockerImage

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
                    dockerImage = docker.build('the127terminal/new:latest', "-f website/Dockerfile website")
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
                // Check if dockerImage is not null before stopping and removing it
                if (dockerImage != null) {
                    dockerImage.stop()
                    dockerImage.remove()
                }
            }
        }
    }
}

