pipeline {
    agent any

    stages {
        stage('Verify Branch') {
            steps {
                echo '$GIT_BRANCH'
            }
        }
        stage('Docker build') {
            steps {
                sh(script: 'docker compose build')
            }
        }
    }
}
