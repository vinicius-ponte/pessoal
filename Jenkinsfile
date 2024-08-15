pipeline {
    agent any

    stages {
        stage('Build Image') {
            steps {
                script {
                    dockerapp = docker.build("vinicius-ponte/mocked-api", '-f ./api/Dockerfile ./api')
                }
            }
        }        
    }
}