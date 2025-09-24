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
                    npm config set cache /var/lib/jenkins/.npm --global
                    npm ci
                    ls -la
                    npm run build
                    ls -la
                '''
            }
        }
    }
}