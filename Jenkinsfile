pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    def customImage = docker.build("my-custom-image").withDockerHost('tcp://127.0.0.1:2375')
                    customImage.push()
                }
            }
        }
    }
}

