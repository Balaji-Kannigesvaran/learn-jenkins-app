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
                    # Clear npm cache
                    npm cache clean --force
                    
                    # Install a specific, stable version of npm to rule out version bugs
                    npm install -g npm@10.5.0
                    
                    node --version
                    npm --version
                    
                    rm -rf node_modules
                    
                    npm ci
                    
                    npm run build
                '''
            }
        }
    }
}