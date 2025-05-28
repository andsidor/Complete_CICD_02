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
		stage('Unit Tests') {
			steps {
				sh 'npm test'
				sh 'npm intall'
			}
		}
	}
}

