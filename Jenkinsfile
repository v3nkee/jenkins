pipeline {
    agent any

    stages {
        stage('Buuild') {
            agent {
                docker {
                    image 'node:18-alpine'
                
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
        stage('test'){
            steps{
            sh'''
            echo "test stage ..."
            ls
            cd build
            test index.html
            npm test
            
            '''
            }
        }
    }
}
// test changes