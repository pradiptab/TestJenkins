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
				echo "Checkout"
			}
		}
		stage('Compile') {
			steps {
				echo "Compile"
				sh "mvn clean compile"
			}
		}
		// stage('Test') {
		// 	steps {
		// 		echo "Test"
		// 		sh "mvn test"
		// 	}
		// }
		// stage('Integration') {
		// 	steps {
		// 		echo "Integration Stage"
		// 		sh "mvn failsafe:integration-test failsafe:verify"
		// 	}
		// }
		stage('Package') {
			steps {
				echo "Package"
				sh "mvn package -DskipTests"
			}
		}
		stage('Build docker image') {
			steps {
				echo "Docker build"
				script {
					dockerImage = docker.build("pradiptab/ms-test:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push docker image') {
			steps {
				echo "Docker image push"
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push('')
						dockerImage.push("${env.BUILD_TAG}")
					}
				}
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
