	pipeline {
    agent any

    environment {
        // Docker Hub credentials and repository info
        DOCKER_HUB_CREDENTIALS = 'DockerHub'  // Use the credentials ID from step 1
        DOCKER_HUB_REPO = 'ahmedembaby24590/dockerimage'  // Replace with your Docker Hub username and image name
        DOCKER_TAG = 'latest'  // You can change the tag to a version like 'v1.0'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your code from Git repository
                git branch: 'main', url: 'https://github.com/AhmedEmbaby-git/DepiProject.git', credentialsId:'jenkinskey' 

            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh "docker build -t ${DOCKER_HUB_REPO}:${DOCKER_TAG} ."
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub using credentials
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) {
                        // This block is necessary for Docker Hub login
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push the image to Docker Hub
                    sh "docker push ${DOCKER_HUB_REPO}:${DOCKER_TAG}"
                }
            }
        }
    }

    post {
        success {
            echo 'Docker image pushed successfully!'
        }
        failure {
            echo 'Failed to push Docker image.'
        }
    }
}

