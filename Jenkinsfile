pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "malle2002/kiii-jenkins"
        REGISTRY = "https://registry.hub.docker.com"
        CREDENTIALS_ID = "dockerhub"
    }

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build image') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    app = docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Push image') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    docker.withRegistry("${REGISTRY}", "${CREDENTIALS_ID}") {
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        app.push("${env.BRANCH_NAME}-latest")
                    }
                }
            }
        }
    }
}
