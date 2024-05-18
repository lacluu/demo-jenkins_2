FROM jenkins/jenkins:lts

# Install Docker CLI
USER root
RUN apt-get update && \
    apt-get install -y apt-transport-https \
                       ca-certificates \
                       curl \
                       gnupg-agent \
                       software-properties-common && \
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && \
    apt-get update && \
    apt-get install -y docker-ce docker-ce-cli containerd.io && \
    usermod -aG docker jenkins && \
    rm -rf /var/lib/apt/lists/*

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
