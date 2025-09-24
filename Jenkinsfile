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
                    // Combine the -v and --user flags into a single args string
                    args '-v /var/lib/jenkins/workspace/learn-jenkins-app:/app --user 970:970'
                    reuseNode true
                }
            }
            steps {
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