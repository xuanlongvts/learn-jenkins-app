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
                    npm i
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:22-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }
        stage('Deploy') {
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
                    npm install -g netlify-cli --unsafe-perm=true
                '''
            }
        }
    }
    
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
