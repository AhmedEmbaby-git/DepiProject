pipeline {
    agent any

     stages {
        stage('Checkout') {
            steps {
               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'jenkinskey', url: 'https://github.com/AhmedEmbaby-git/DepiProject']])
	    }
	}
	stage('Docker Login') {
            steps {
                script {
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

stage('Deploy to AWS EKS') {
    steps {
        script {
            echo 'Deploying to AWS Elastic Kubernetes Service (EKS)'
              {
                sh """
                # Configure AWS CLI with the specified credentials
                export AWS_ACCESS_KEY_ID=$( AWS_ACCESS_KEY_ID )
                export AWS_SECRET_ACCESS_KEY=$( AWS_SECRET_ACCESS_KEY)
                export AWS_DEFAULT_REGION=us-east-1 # Change to your desired region

                # Update kubeconfig for EKS
                aws eks --region us-east-1 update-kubeconfig --name Depi-Cluster

                # Check Kubernetes cluster information
                kubectl cluster-info
                
                # Update the image for the deployment
                kubectl set image deployment/app-deployment my-app-container=ahmedembaby24590/depi-image:depi-image
                
                # Check the rollout status
                kubectl rollout status deployment/app-deployment
                """
            }
        }
    }
}
        
