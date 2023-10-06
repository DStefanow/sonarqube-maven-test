// Define SonarQube project properties
def sonarHostUrl = 'http://172.17.0.3:9000/'

def sonarOptions = [
	projectName: 'jenkins-maven-test',
	projectKey: 'jenkins-maven-test',
	sonarToken: 'sqp_c37cef881510d1ba491cdfd69cf9c6019fbb4c3f'
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
						-Dsonar.projectKey="${sonarOptions.projectKey}" \
						-Dsonar.projectName='"${sonarOptions.projectName}"' \
						-Dsonar.host.url=${sonarHostUrl} \
						-Dsonar.token="${sonarOptions.sonarToken}"
				"""
			}
		}
	}
}
