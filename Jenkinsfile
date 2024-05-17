pipeline {
    agent {
        docker {
            image 'docker:25.0.4-dind'
            args '--privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Verify Branch') {
            steps {
                echo '$GIT_BRANCH'
            }
        }
        stage('Docker build') {
            steps {
                sh(script: 'docker-compose build')
            }
        }
    }
}
