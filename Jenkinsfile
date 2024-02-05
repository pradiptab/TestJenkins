// Scripted
// node {
// 	echo "Build"
// 	echo "Test"
// 	echo "Integration"
// }

// DECLARATIVE
pipeline {
	// agent { docker { image 'maven:3.9.6'} }
	agent any
	environment { 
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "PATH - $PATH"
				echo "Building"
			}
		}
		stage('Compile') {
			steps {
				echo "Compile"
				sh "man clean compile"
			}
		}
		stage('Test') {
			steps {
				echo "Test"
				sh "man test"
			}
		}
		stage('Integration') {
			steps {
				echo "Integration Stage"
				sh "man failsafe:integration-test failsafe:verify"
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
