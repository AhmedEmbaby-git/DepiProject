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
                    withCredentials([usernamePassword(credentialsId: 'DockerHub')])
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


        
