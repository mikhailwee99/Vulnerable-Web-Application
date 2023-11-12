pipeline {
	agent any
	stages {
		stage ('Checkout') {
			steps {
				git branch:'master', url: 'https://github.com/mikhailwee99/Vulnerable-Web-Application.git'
			}
		}
		stage('Code Quality Check via SonarQube') {
			steps {
				script {
					def scannerHome = tool 'SonarQube';
					withSonarQubeEnv('SonarQube') {
						sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. Dsonar.host.url=sonarqube:9000 -Dsonar.token=sqp_ccc405e61c44ca7d76ee796ae5ff50d3d1ae3f3b"
					}
				}
			}
		}
	}
	post {
		always {
			recordIssues enabledForFailure: true, tool: sonarQube()
		}
	}
}