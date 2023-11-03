pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Clone the Jenkinsfile from the repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/Terminal127/jenkins-project']]])
                }
            }
        }

        stage('Build and Deploy NGINX') {
            steps {
                script {
                    // Build and run the NGINX container
                    sh 'docker run -d -p 8081:80 --name my-nginx nginx'
                }
            }
        }
    }

    post {
        always {
            script {
                // Stop and remove the NGINX container
                sh 'docker stop my-nginx'
                sh 'docker rm my-nginx'
            }
        }
    }
}

