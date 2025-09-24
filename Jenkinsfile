pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    # Force removal of the node_modules directory to prevent 'ENOTEMPTY' errors
                    rm -rf node_modules
                    npm cache clean --force
                    npm ci
                    ls -la
                    npm run build
                    ls -la
                '''
            }
        }
    }
}