pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = "dickyfli/my-app:latest"
    }

    triggers {
        GenericTrigger(
            genericVariables: [
                [key: 'pushed_image', value: '$.push_data.tag']
            ],
            causeString: 'Triggered by Docker Hub Webhook',
            token: 'dockerhub-trigger',
            printContributedVariables: true,
            printPostContent: true
        )
    }

    stages {
        stage('Pull Latest Image') {
            steps {
                sh "docker pull ${DOCKER_HUB_REPO}"
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                sh """
                    docker compose down || true
                    docker compose up -d
                """
            }
        }
    }
}
