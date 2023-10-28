pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out your source code from your version control system (e.g., Git)
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build your Docker image
                    docker.build("my-webserver")
                }
            }
        }

        stage('Deploy Docker Container') {
            steps {
                script {
                    // Start a Docker container based on the image you built
                    def dockerImage = docker.image("my-webserver")

                    // Map a port from the host to the container (e.g., 8082 to 80)
                    dockerImage.inside('-p 8082:80') {
                        // Start your web server or application within the container
                        sh 'docker run -d -p 80:80 my-webserver'
                    }
                }
            }
        }
    }
}
