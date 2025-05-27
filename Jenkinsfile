pipeline {
	agent any
	tools {
		nodejs 'NodeJS'
		
	}
	
	stages {
		stage('GitHub'){
			steps {
				git branch: 'main', credentialsId: 'jenkins-cicd', url: 'https://github.com/iQuantC/Complete_CICD_02.git'
			}
		}
		}
		stage('uNIT TESTS'){
			steps {
				sh 'mvn test'
				sh 'npm intall'
				sh 'npm run test'
				
			}
		}
		
		
		
		
	}
}