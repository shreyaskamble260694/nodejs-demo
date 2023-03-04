pipeline {
    agent {label "deployment"} 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-valaxy')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/ravdy/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t shyam .'
            }
        }
        
         stage('Build conatiner container') {
            steps {  
                sh 'docker run -it --name shreyas125 shyam /bin/bash'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push valaxy/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

