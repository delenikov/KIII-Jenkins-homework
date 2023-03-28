node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build and push image') {
        if (env.BRANCH_NAME == 'dev') {
            app = docker.build("delenikov/kiii-jenkins")
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
            }
        } else {
            echo "[Changes not on 'dev' branch] Skipping Docker image build and push"
        }
    }
}