pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/DickyfliPerdanaPutra/jenkins-docker-lab.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                when {
                    changeset "**", exclude: ["README.MD", "docs/**"]
                }
                script {
                    docker.build("jenkins-docker-lab:latest")
                }
            }
        }
        stage('Run Container') {
            when {
                    changeset "**", exclude: ["README.MD", "docs/**"]
            }
            steps {
                script {
                    sh 'docker stop flask-app'
                    sh 'docker rm flask-app'
                    sh 'docker run -d -p 5000:5000 --name flask-app jenkins-docker-lab:latest'
                }
            }
        }
    }
}
