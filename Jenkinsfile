	pipeline {
    agent any

    environment {
        // Docker Hub credentials and repository info
        DOCKER_HUB_CREDENTIALS = 'DockerHub'  // Use the credentials ID from step 1
        DOCKER_HUB_REPO = 'ahmedembaby24590/depi-image'  // Replace with your Docker Hub username and image name
        DOCKER_IMAGE = "depi-image"
    }
        stages {
          stage('Pull Repository') {
            steps {
                echo 'Pulling the repository'
                sh 'git clone http://github.com/AhmedEmbaby-git/DepiProject.git' 
            }
        }

        stage('Login to Docker Hub') {
            steps {
               script {
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials-id') 
                
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

