// Define SonarQube project properties
def sonarHostUrl = 'http://172.17.0.3:9000/'

def sonarOptions = [
	projectName: 'jenkins-maven-test',
	projectKey: 'jenkins-maven-test',
	sonarToken: 'sqp_c37cef881510d1ba491cdfd69cf9c6019fbb4c3f'
]

pipeline {
	agent any
	parameters {
		choice(name: 'REPO',
			choices: [
				'sonarqube-maven-test'
			],
			description: 'Repo for clone'
		)

		string(name: 'BRANCH', defaultValue: 'main', description: 'Branch for checkout')
	}
	stages {
		stage('Clone locally github project') {
			steps {
				git branch: "${params.BRANCH}", credentialsId: 'github-test', url: "git@github.com:DStefanow/${params.REPO}.git"

				script {
					def sonarRunResult = sh(script: "mvn clean verify sonar:sonar \
							-Dmaven.test.skip=true \
							-Dsonar.projectKey=${sonarOptions.projectKey} \
							-Dsonar.projectName='${sonarOptions.projectName}' \
							-Dsonar.host.url=${sonarHostUrl} \
							-Dsonar.token=${sonarOptions.sonarToken}", returnStdout: true)
				}
			}
		}
	}
}
