pipeline {
    agent any

    stages {
        stage ('Build Image') {
            steps {
                script {
                    dockerapp = docker.build("viniciusponte/mocked-api:${env.BUILD_ID}", '-f ./api/Dockerfile ./api')
                }
            }
        }      
        stage ('Push Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }  

        stage ('Deploy Kubernetes') {
            steps {
                script {
                    echo "Deploying to Kubernetes..."
                    withKubeConfig(caCertificate: '', clusterName: 'minikube', contextName: 'minikube', credentialsId:'minikube-jenkins-secret', namespace: 'default', restrictKubeConfigAccess: false, serverUrl: 'https://172.19.48.251:8443') {
                        bat 'kubectl apply -f ./api/k8s/deployment.yaml'
                    }
                }
            }
        }
    }
}