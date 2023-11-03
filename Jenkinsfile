pipeline {
    agent any
    
    stages {
        // ...
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

