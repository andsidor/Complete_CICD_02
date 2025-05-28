pipeline {
	agent any
	tools {
		nodejs 'NodeJS'		
	}
	environment {
		SONAR_SCANNER_HOME = tool 'SonarCubeScanner'
		SONAR_PROJECT_KEY = 'complete-cicd'
		DOCKER_HUB_REPO = 'asidor23/complete-cicd'
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
				sh 'npm install'
			}
		}
		stage('SonarQube Analysis') {
			steps {
				withCredentials([string(credentialsId: 'complete-cics-token', variable: 'SONAR_TOKEN')]) {
					
					withSonarQubeEnv('SonarCube') {
						sh """
						${SONAR_SCANNER_HOME}/bin/sonar-scanner \
						-Dsonar.projectKey=${SONAR_PROJECT_KEY} \
						-Dsonar.sources=. \
						-Dsonar.host.url=http://sonarqube-dind:9000 \
						-Dsonar.login=${SONAR_TOKEN}
						"""
    
}
}
				
			}
	
		}
		stage('Docker Build Image') {
			steps {
				script{
					docker.build("${DOCKER_HUB_REPO}:latest")


					}

				}
			}
		}
}


