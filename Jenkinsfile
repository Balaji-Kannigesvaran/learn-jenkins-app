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
                    # Clean the local node_modules directory to avoid permission issues
                    rm -rf node_modules

                    # Clear the npm cache forcefully to fix any corruption
                    npm cache clean --force
                    
                    # Install dependencies from package-lock.json
                    npm ci

                    # Build the application
                    npm run build
                '''
            }
        }
    }
}