pipeline {
    agent any

    stages{

        stage ('Build Docker Image') {
            steps {
                script {
                    dockerapp = docker.build("dossantosmurilo/kube-news:${env.BUILD_ID}", '-f ./kube-news/src/Dockerfile ./kube-news/src')
                }
            }
        }

        stage ('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }                        
                }
            }
        }

        satge ('Deploy Kubernetes') {
            steps{
                withKubeconfig ([credentialsId: 'kubeconfig']) {
                     sh 'kubectl apply -f ./kube-news/src/k8s/deployment.yml'
                }
            }
        }
    }
}