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
		stage('SonarQube') {
				when {
				    expression{env.EXECUTE}
                }
				steps {
					script {
				    def scannerHome = tool 'sonarqube';
					   	withSonarQubeEnv("sonarqube") {
						   sh "${tool("sonarqube")}/bin/sonar-scanner \
						  	-Dsonar.organization=pablosiegers \
							-Dsonar.projectKey=pablosiegers_DOTT \
							-Dsonar.sources=cidr_convert_api/node \
							-Dsonar.host.url=https://sonarcloud.io"
					   }
				   }
				}
		}
		stage('Install Dependencies - Building App'){
            steps {
                sh 'npm install'
            }
        }
        stage ('Unit Tests') {
				when {
				    expression{env.EXECUTE}
                }
				steps {
					sh 'npm run test'
				}
        }
		
    }
}
