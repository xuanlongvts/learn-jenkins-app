pipeline {
    agent any

    stages {        
        stage('Build') {
            agent {
                docker {
                    image 'node:22-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --verison
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
    }
}
