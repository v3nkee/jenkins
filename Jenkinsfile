pipeline{
    agent any
    environment {
        IMAGE="jovenkat475159/app-flask"
        TAG="${BUILD_NUMBER}"

    }
    stages {
        stage('checkout'){
            steps {
                echo 'Checking out the repo'
                git branch: 'main', credentialsId: 'git-token', poll: false, url: 'https://github.com/v3nkee/jenkins.git'
            }
        }
        stage('build'){
            steps {
                echo 'building the ENV'
                sh 'docker build -t "$IMAGE:$TAG" -t "$IMAGE:latest" .'
            }
        }
        stage('push'){  
            steps {
                echo 'Pushing image'
                withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'DOCKERHUB_PWD', usernameVariable: 'DOCKERHUB_USER')]) {
                                    sh 'docker push "$IMAGE:$TAG"'
                                    sh 'docker push "$IMAGE:latest"'
                                }
                }
        }
        stage('deploy'){
            steps {
                echo 'Deploying image'
                sh 'docker pull "$IMAGE:$TAG"'
                sh 'docker rm -f app-flask || true'
                sh 'docker run -d --name app-flask -p 5000:5000 "$IMAGE:$TAG"'
            }
        }
        stage('test'){
            steps {
                echo 'hit http://localhost:5000 to see the app.'
            }
        }
    }
}
