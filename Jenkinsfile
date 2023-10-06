// Define SonarQube project properties
def sonarHostUrl = 'http://172.17.0.3:9000'

def sonarOptions = [
	projectName: 'jenkins-maven-test',
	projectKey: 'jenkins-maven-test',
	sonarToken: 'sqb_b1b210c0eb53ec7b5194a8af0a385dad3d57c557'
]

pipeline {
	agent any
	stages {
		stage('Clone locally github project') {
			steps {
				git branch: 'main', credentialsId: 'github-test', url: 'git@github.com:DStefanow/sonarqube-maven-test.git'

				sh """
					mvn clean verify sonar:sonar \
						-Dmaven.test.skip=true \
						-Dsonar.projectKey='"${sonarOptions.projectKey}"' \
						-Dsonar.projectName='"${sonarOptions.projectName}"' \
						-Dsonar.host.url='"${sonarHostUrl}"' \
						-Dsonar.token='"${sonarOptions.sonarToken}"'
				"""
			}
		}
	}
}
