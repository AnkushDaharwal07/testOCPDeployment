pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'ankush/myApp'  // Replace with your Docker Hub username and desired image name
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the GitHub repository
                git branch: 'main', url: 'git@github.com:AnkushDaharwal07/testOCPDeployment.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                // Build Docker image
                script {
                    docker.build("${env.DOCKER_IMAGE}")
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                // Run Docker container
                script {
                    docker.image("${env.DOCKER_IMAGE}").run('-d -p 5000:5000 --name myapp')
                }
            }
        }
    }

    post {
        always {
            // Cleanup - remove the Docker container
            script {
                sh 'docker stop myapp || true'
                sh 'docker rm myapp || true'
            }
        }
    }
}
