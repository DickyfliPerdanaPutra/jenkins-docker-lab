pipeline {
    agent any

    stages {
        stage('Check Changes') {
            steps {
                script {
                    // optional, cek perubahan di repo kalau Jenkins juga clone source
                    def changes = sh(
                        script: "git diff --name-only HEAD~1 HEAD || true",
                        returnStdout: true
                    ).trim()

                    if (changes && !(changes.contains("app/") || changes.contains("Dockerfile"))) {
                        echo "Tidak ada perubahan relevan, skip deploy"
                        currentBuild.result = 'SUCCESS'
                        error("Skip pipeline")
                    }
                }
            }
        }

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
