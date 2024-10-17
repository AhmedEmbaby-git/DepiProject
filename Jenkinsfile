	pipeline {
    agent any

    environment {
        // Docker Hub credentials and repository info
        DOCKER_HUB_REPO = 'ahmedembaby24590/depi-image'  // Replace with your Docker Hub username and image name
        DOCKER_IMAGE = "depi-image"
    }
       stage('Docker Login') {
            steps {
                script {
                    // Use Jenkins credentials to log in to Docker Hub
                    withCredentials([usernamePassword(credentialsId: 'DockerHub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
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

