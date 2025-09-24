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
                    args '-v /var/lib/jenkins/workspace/learn-jenkins-app:/app' // 1. Map the Jenkins workspace to /app
                    reuseNode true
                }
            }
            steps {
                // 2. Change the working directory and run a clean install
                dir('/app') {
                    sh '''
                        rm -rf node_modules
                        npm ci
                        npm run build
                    '''
                }
            }
        }
    }
}