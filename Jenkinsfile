pipeline {
    agent any

    stages {
        stage('Build Image') {
            steps {
                script {
                    dockerapp = docker.build("vinicius-ponte/mocked-api:${env.BUILD_ID}", '-f ./api/Dockerfile ./api')
                }
            }
        }        
    }
}