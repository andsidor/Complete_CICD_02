pipeline {
	agent any
	tools {
		nodejs 'NodeJS'
	}
	environment {
		SONAR_PROJECT_KEY = 'complete-cicd-02'

	}
	stages {
		stage('GitHub'){
			steps {
				git branch: 'main', credentialsId: 'jenkins-cicd', url: 'https://github.com/iQuantC/Complete_CICD_02.git'
			}
		}
		
		
		
		
	}
}