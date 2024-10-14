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
            environment {
                // Override HOME to WORKSPACE value
                HOME = "${WORKSPACE}"
                // or override npm's cache directory (~/.npm)
                NPM_CONFIG_CACHE = "${WORKSPACE}/.npm"
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm install pnpm
                    node_modules/.pnpm i
                    node_modules/.pnpm run build
                    ls -la
                '''
            }
        }
    }
}
