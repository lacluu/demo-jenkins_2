pipeline {
    agent {
        docker {
            image 'docker:24.0.2-dind'
            args '--privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Verify Branch') {
            steps {
                echo '$GIT_BRANCH'
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'docker --version'  // Verify Docker is available
                    sh 'docker build -t myapp:latest .'  // Build Docker image
                }
            }
        }
    }
}
