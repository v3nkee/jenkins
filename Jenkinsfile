pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            reuseNode true
        }
    }

    stages {
        stage('Build') {
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

        stage('Test') {
            steps {
                sh '''
                echo "test stage ..."
                ls
                cd build
                test index.html
                npm test
                '''
            }
        }

        post {
     always {
        junit 'test-examples/results.xml'
            }
              }
    }
}
