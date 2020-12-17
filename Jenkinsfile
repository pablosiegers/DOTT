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
				sh 'npm install -D esm' //save the package for development purpose and this will install the ECMAScript to interpret and execute the tests
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
							-Dsonar.sources=. \
							-Dsonar.host.url=https://sonarcloud.io"
					   }
				   }
				}
		}
        stage ('Unit Tests') {
				when {
				    expression{env.EXECUTE}
                }
				steps {
					script {
						try {
							sh 'npm test'
						}
						catch (exc){
							sh 'echo "Unit test failed"'
						}
					}
				}
        }
		
    }
}
