pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'my-custom-image'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from your GitHub repository
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image from the Dockerfile in the 'website' directory
                    docker.image("docker:latest").inside {
                        def customImage = docker.build(env.DOCKER_IMAGE_NAME, "-f website/Dockerfile website")
                        customImage.inside {
                            // You can add additional build commands or environment setup here
                        }
                    }
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container with the built image on port 8081
                    docker.image(env.DOCKER_IMAGE_NAME).withRun('-p 8081:80 -d') {
                        echo "Docker container is running on port 8081"
                    }
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker containers after the job finishes
            script {
                sh "docker stop \$(docker ps -q --filter ancestor=${env.DOCKER_IMAGE_NAME})"
                sh "docker rm \$(docker ps -aq --filter ancestor=${env.DOCKER_IMAGE_NAME})"
            }
        }
    }
}

