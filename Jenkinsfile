pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = 'my-custom-image'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image from the Dockerfile
                    docker.build(env.DOCKER_IMAGE_NAME, './website')
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container from the built image
                    docker.image(env.DOCKER_IMAGE_NAME).withRun('-p 8081:80 -d') {
                        echo "Docker container is running on port 8081"
                    }
                }
            }
        }
    }
    post {
        always {
            // Stop and remove the Docker container
            script {
                try {
                    sh "docker stop ${env.DOCKER_IMAGE_NAME}"
                    sh "docker rm ${env.DOCKER_IMAGE_NAME}"
                } catch (Exception e) {
                    echo "Error stopping or removing the container: ${e.message}"
                }
            }
        }
    }
}

