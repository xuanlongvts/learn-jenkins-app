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
                    npm --version
                    npm install -g pnpm
                    pnpm i
                    pnpm run build
                    ls -la
                '''
            }
        }
    }
}
