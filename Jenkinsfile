pipeline {
    agent any
    environment {
        EXECUTE = 'true'
    }
    tools {nodejs "node"}
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/pablosiegers/DOTT'
            }
        }
        stage('Install Dependencies - Building App'){
            steps {
                sh 'npm install'
            }
        }
		stage('SonarQube') {
				when {
				    expression{env.EXECUTE}
                }
				steps {
					script {
				    def scannerHome = tool 'sonarqube';
					   	withSonarQubeEnv("sonarqube-container") {
						   sh "${tool("sonarqube")}/bin/sonar-scanner \
						    -Dsonar.organization=pablosiegers \
  							-Dsonar.projectKey=pablosiegers_DOTT \
  							-Dsonar.sources=. \
  							-Dsonar.host.url=https://sonarcloud.io "
					   }
				   }
				}
		}
        stage ('Unit Tests') {
				when {
				    expression{!env.EXECUTE}
                }
				steps {
					sh 'npm test -- ipv4validation'
					sh 'npm test'
				}
        }
		
    }
}
