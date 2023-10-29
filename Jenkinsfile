pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Pull the base image and build your Docker image
                    docker.image("my-base-image:latest").pull()
                    docker.build("my-webserver:latest")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Start a Docker container based on the image you built
                    def dockerImage = docker.image("my-webserver:latest")

                    // Map a port from the host to the container (e.g., 8080 to 80)
                    dockerImage.run('-p 8080:80')

                    // Output the container's IP address
                    def containerIP = dockerImage.inside('sh', '-c', 'hostname -i').trim()
                    echo "Website is hosted at http://$containerIP:8080/"
                }
            }
        }
    }
}
