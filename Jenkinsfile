pipeline {
    agent any

    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    // contoh: app Anda ada di Docker Hub dengan tag latest
                    sh "docker pull dickyfli/my-app:latest"
                }
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                script {
                    // masuk ke folder docker-compose.yml Anda
                    sh """
                        cd /opt/myapp-deploy
                        docker compose down
                        docker compose up -d
                    """
                }
            }
        }
    }
}
