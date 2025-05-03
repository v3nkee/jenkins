pipeline {
    agent any

    stages {
        stage('Buuild') {
            agent {
                docker {
                    image 'node:18-alpine'
                    args '--network my_custom_network'
                    reuseNode true
                }
            }
            steps {
                sh '''
                ls -la
                node --version
                npm --version
                npm ci
                npm run build
                ls -la 
                '''
            }
        }
    }
}
// test changes