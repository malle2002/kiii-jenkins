node {
    def app
    
    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        if (env.BRANCH_NAME == 'dev') {
            app = docker.build("malle2002/kiii-jenkins")
        } else {
            echo "Skipping build stage as the branch is not 'dev'"
        }
    }

    stage('Push image') {
        if (env.BRANCH_NAME == 'dev') {
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
            }
        } else {
            echo "Skipping push stage as the branch is not 'dev'"
        }
    }
}
