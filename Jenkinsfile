pipeline {
    agent any
    environment{
        docker_token=credentials('docker_token')
        docker_user=credentials('docker_user')
    }
    stages {
        stage('get code') {
            steps {
               git branch: 'main', credentialsId: 'vodeel', url: 'https://github.com/vodeel/webapp.git'
            }
        }
        
        stage('gernerate-buld') {
            steps {
               sh 'docker build -t vodeel14/web-httpd:${BUILD_NUMBER}  .'
            }
        }
        
        stage('push-buld') {
            steps {
                sh 'echo ${docker_token} | docker login -u ${docker_user}  --password-stdin'
               sh 'docker push  vodeel14/web-httpd:${BUILD_NUMBER}'
            }
        }
    }
    
    post{
        always{
            sh 'docker logout'
        }
    }
}
