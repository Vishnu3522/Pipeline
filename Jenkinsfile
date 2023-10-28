pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def dockerImage = docker.build("my-webapp-image")
                }
            }
        }

        stage('Deploy Docker Container') {
            steps {
                script {
                    dockerImage.inside('-p 8081:80') {
                        sh 'docker run -d -p 80:80 my-webserver'
                    }
                }
            }
        }
    }
}
