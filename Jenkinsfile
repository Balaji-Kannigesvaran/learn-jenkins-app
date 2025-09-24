pipeline {
    agent any

    options {
        skipDefaultCheckout true
    }

    stages {
        stage('Checkout') {
            steps {
                cleanWs() // 1. Use the built-in Jenkins cleanup step
                checkout scm
            }
        }
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    # 2. Run cache and node_modules cleanup
                    npm cache clean --force
                    rm -rf node_modules
                    
                    # 3. Install and build
                    npm ci
                    npm run build
                '''
            }
        }
    }
}