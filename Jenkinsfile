node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    // Only build and push if on the 'dev' branch
    if (env.BRANCH_NAME == 'dev') {
        stage('Build image') {
            app = docker.build("matej2345/devops-lab4")
        }

        stage('Push image') {
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
                // signal the orchestrator that there is a new version
            }
        }
    } else {
        echo "Skipping Docker build and push since this is not the 'dev' branch."
    }
}

