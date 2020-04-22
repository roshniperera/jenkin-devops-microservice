pipeline {
	agent any

	// agent { docker { image 'maven:3.6.3'}}
	// agent { docker { image 'node:13.13'}}

	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH" 
	}
	stages {
		stage('Checkout') {
			steps {
				// sh 'node --version'
				sh 'mvn --version'
				sh 'docker version'
				sh label: 'java_ver Label :', script: 'java -version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER -$env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}

		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage("Build Docker Image") {
			steps {
				// docker build -t roshniperera/currency-exchange-microservice:$env.BUILD_TAG
				script{
					dockerImage = docker.build("roshniperera/currency-exchange-microservice:${env.BUILD_TAG}")
				}
			}
		}
		stage("Push Docker Image") {
			steps {
				script{
					docker.withRegistry('', 'dockerhub')
					dockerImage.push()
					dockerImage.push('latest')
				}
				

			}
		}		
	} 
	
	
	post {
		always {
			echo 'Im awesome. I run aways'
		}
		success {
			// mail bcc: '', body: 'Pipeline: Basic Steps', cc: '', from: 'roshni.byju@gmail.com', replyTo: '', subject: 'Build Successful', to: 'roshni.byju@gmail.com'
			echo 'I run when you are successful'
		}
		failure {
			// mail bcc: '', body: 'Pipeline: Basic Steps', cc: '', from: 'roshni.byju@gmail.com', replyTo: '', subject: 'Build Failed', to: 'roshni.byju@gmail.com'
			echo 'I run when you fail'
		}

	}
}
