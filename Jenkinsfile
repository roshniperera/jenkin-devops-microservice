pipeline {
	agent any

	// agent { docker { image 'maven:3.6.3'}}
	// agent { docker { image 'node:13.13'}}
	stages {
		stage('Build') {
			steps {
				// sh 'node --version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER -$env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}		
		stage('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
	} 
	
	post {
		always {
			echo 'Im awesome. I run aways'
		}
		success {
			mail bcc: '', body: 'Pipeline: Basic Steps', cc: '', from: 'roshni.byju@gmail.com', replyTo: '', subject: 'Build Successful', to: 'roshni.byju@gmail.com'
			echo 'I run when you are successful'
		}
		failure {
			mail bcc: '', body: 'Pipeline: Basic Steps', cc: '', from: 'roshni.byju@gmail.com', replyTo: '', subject: 'Build Failed', to: 'roshni.byju@gmail.com'
			echo 'I run when you fail'
		}

	}
}
