pipeline {
	agent any
	tools {
		nodejs 'NodeJS'		
	}
	environment {
		SONAR_SCANNER_HOME = tool 'SonarCubeScanner'
		SONAR_PROJECT_KEY = 'complete-cicd'
		JOB_NAME_NOW = 'cicd02'
		IMAGE_TAG = 'latest'
		ECR_REGISTRY = '024848459679.dkr.ecr.us-east-1.amazonaws.com'
		ECR_REPO = 'jenkinsawsrepo'
		
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
					docker.build("${ECR_REGISTRY}/${ECR_REPO}:${IMAGE_TAG}")
				}
			}
		}
		stage('Trivy Scan') {
			steps {
				sh """ trivy image ${JOB_NAME_NOW}:latest """
			}
		}
		stage('Login ECR') {
			steps {
				sh """aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 024848459679.dkr.ecr.us-east-1.amazonaws.com """
			}
		}
		stage('Push to ECR') {
			steps {
				script{
					docker.image("${ECR_REGISTRY}/${ECR_REPO}:${IMAGE_TAG}").push()
				}
		}
		}
	
	}
}
