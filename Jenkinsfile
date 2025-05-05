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

            post {
                always {
                    // For example: archive test results
                    junit 'test-results/junit.xml'
                    echo 'Post actions completed.'
                }
            }
        }

         /*stage('Test2') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.52.0-noble'
                    reuseNode true
                }
            }
            steps {
                sh '''
                npm install serve
                node_modules/.bin/serve -s build &
                npx playwright test
                '''
            }
        }*/

        stage('Deploy') {
            agent {
        docker {
            image 'node:18-alpine'
            reuseNode true
        }
    }
            steps {
                sh '''
                npm install netlify-cli
                node_modules/.bin/netlify --version
                
                '''
            }
        }
    }
}
