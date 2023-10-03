pipeline {
	agent any
	stages {
		stage('Clone locally github project') {
			steps {
				git branch: 'main', credentialsId: 'github-test', url: 'git@github.com:DStefanow/sonarqube-maven-test.git'

				echo "Hello World"
			}
		}
	}
}
