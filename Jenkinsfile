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
                    # This command is now executed by the container's user,
                    # ensuring it has the necessary permissions.
                    rm -rf node_modules

                    # Clearing the npm cache forcefully inside the container.
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