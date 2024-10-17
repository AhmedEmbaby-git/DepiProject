	pipeline {
    agent any

    environment {
        // Docker Hub credentials and repository info
        DOCKER_HUB_CREDENTIALS = 'DockerHub'  // Use the credentials ID from step 1
        DOCKER_HUB_REPO = 'ahmedembaby24590/myapp'  // Replace with your Docker Hub username and image name
        DOCKER_TAG = 'latest'  // You can change the tag to a version like 'v1.0'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your code from Git repository
                git branch: 'main', url: 'http://github.com/AhmedEmbaby-git/DepiProject.git', credentialsId:'jenkinskey' 

            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub using credentials
                    docker.withRegistry('https://hub.docker.com/repository/docker/ahmedembaby24590/myapp/general', DOCKER_HUB_CREDENTIALS) {
                        // This block is necessary for Docker Hub login
                    }
                }
            }
	}
        stage('Build & push Dockerfile') {
            steps {
                sh 'ansible-playbook ansible-playbook.yml'
            }
        }
    }
}

