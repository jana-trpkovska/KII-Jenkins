node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
        script {
            app = docker.build("jtrpkovska/kii-jenkins")
        }
    }
    stage('Push image') {
        when {
            branch 'dev'
        }
        steps {
            script {
                docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                    app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                    app.push("${env.BRANCH_NAME}-latest")
                    // signal the orchestrator that there is a new version
                }
            }
        }
    }
}
