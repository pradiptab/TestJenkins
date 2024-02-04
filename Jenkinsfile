// Scripted
// node {
// 	echo "Build"
// 	echo "Test"
// 	echo "Integration"
// }

// DECLARATIVE
pipeline {
\\ 	agent any 
	agent { docker { image 'maven:3.9.6'} }
	stages {
		stage('Build') {
			steps {
				sh 'mvn --version'
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
			echo "PIPELINE complete"
		}
		success {
			echo "PIPELINE success"
		}
		failure {
			echo "PIPELINE failed"
		}
	}
}
