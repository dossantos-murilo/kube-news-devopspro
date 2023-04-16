pipeline {
    agent any

    stages{

        stage('Build Docker Image') {
            steps {
                script {
                    dockerapp = docker.build("dossantosmurilo/kube-news:${env.BUILD_ID}", '-f ./kube-news/src/Dockerfile ./kube-news/src')
                }
            }
        }
    }
}