
pipeline{

   agent any

	//create dockerhub credential in github with your dockerhub Username and Password/Token
	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}
	
	stages {

		stage('gitclone') {

		      steps {
		         git 'https://github.com/toyosi11/propjectrep.git'
		      }
		}
		
		stage('Build') {
			steps {
			
			   sh 'docker build -t toyosi11/myapp:${BUILD_NUMBER} .'
			}
		}
		
		stage('Login') {
		
			steps {
			   sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login --username toyosi11 --password-stdin'    
			}
		}

		stage('Push') {
			
			steps {
			   sh 'docker push toyosi11/myapp:${BUILD_NUMBER}'
			}
		}
		}
	
	post {
	    always {
		sh 'docker logout'
	    }
    }

}

