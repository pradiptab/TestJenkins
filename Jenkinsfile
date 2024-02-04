// Scripted
// node {
// 	echo "Build"
// 	echo "Test"
// 	echo "Integration"
// }

// DECLARATIVE
pipeline {
	agent any 
	stages {
		stage('Build') {
			steps {
				echo "Building"
			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration') {
			steps {
				echo "Integration"
			}
		}
	}
	post {
		always {
			echo "I run always"
		}
		success {
			echo "I run when success"
		}
		failure {
			echo "I run when failed"
		}
	}
}
