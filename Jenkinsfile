pipeline {
    agent any // Sử dụng bất kỳ agent nào có sẵn (có thể là Jenkins agent mặc định)

    stages {
        stage('Prepare Environment') {
            steps {
                // Cài đặt Docker CLI trong container Jenkins
                script {
                    docker.image('jenkins/jenkins:lts').inside('-u root') {
                        sh '''
                            apt-get update && \
                            apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common && \
                            curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
                            add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && \
                            apt-get update && \
                            apt-get install -y docker-ce docker-ce-cli containerd.io && \
                            usermod -aG docker jenkins && \
                            rm -rf /var/lib/apt/lists/*
                        '''
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Kiểm tra Docker CLI đã cài đặt thành công trong container Jenkins chưa
                    sh 'docker --version'
                    
                    // Thực thi các lệnh Docker bình thường trong pipeline
                    sh 'docker build -t myapp:latest .'  // Build Docker image
                }
            }
        }
    }
}
