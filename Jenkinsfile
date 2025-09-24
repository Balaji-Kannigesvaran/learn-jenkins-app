pipeline {
    agent any
    options {
        skipDefaultCheckout true
    }
    stages {
        stage('Checkout') {
            steps {
                cleanWs()
                checkout scm
            }
        }
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-v /var/lib/jenkins/workspace/learn-jenkins-app:/app'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    # Change to the mounted volume's path
                    cd /app

                    # Run the build commands
                    rm -rf node_modules
                    npm ci
                    npm run build
                '''
            }
        }
    }
}