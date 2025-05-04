pipeline {
    

    stages {
        stage('Build') {
            agent {
        docker {
            image 'node:18-alpine'
            reuseNode true
        }
    }
            steps {
                sh 'npm run build'
            }
        }

        stage('Test') {
            agent {
        docker {
            image 'node:18-alpine'
            reuseNode true
        }
    }
            steps {
                sh 'npm test'
            }
        }

         stage('Test') {
            agent{
                docker{
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    resuseNode true
                }
            }
            steps {
                sh '''
                npm install -g serve
                serve -s build
                npx playwright test
                '''
            }
        }
    }

   /* post {
        always {
            // For example: archive test results
            junit 'test-examples/results.xml'
            echo 'Post actions codsmpleted.'
        }
    }*/
}
