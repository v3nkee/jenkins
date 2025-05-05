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
                sh 'npm run build'
              }
        }

        stage('Test') {
           
            steps {
                sh 'npm test'
            }

             post {
        always {
            // For example: archive test results
            junit 'jest-results/junit.xml'
            echo 'Post actions codsmpleted.'
        }
        }

         stage('Test2') {
            agent{
                docker{
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    resuseNode true
                } 
            }
            steps {
                sh '''
                npm install -g serve
                node_modules/.bin/serve -s build &
                sleep 10
                npx playwright test
                '''
            }
        }
         stage('Deploy') {
            
            steps {
                sh '''
                npm install netlify-cli -g
                netlify --verion
                '''
            }
        }
     }

   
    
    }
}