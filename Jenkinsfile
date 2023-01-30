pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('nafey1-dockerhub')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                sh 'docker build -t nafey1/flaskapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('verify image') {
            steps{
                sh 'docker inspect image nafey1/flaskapp:$BUILD_NUMBER'
            }
        }                
        stage('push image') {
            steps{
                sh 'docker push nafey1/flaskapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
