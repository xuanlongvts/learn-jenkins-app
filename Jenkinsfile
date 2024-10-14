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
                    sudo npm cache clean -force
                    sudo npm i
                    sudo npm run build
                    ls -la
                '''
            }
        }
    }
}
