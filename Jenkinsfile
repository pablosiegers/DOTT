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
					sh 'echo "SonarQube Stage"'
				}
		}
        stage ('Unit Tests') {
				try {
					sh 'npm test'
				}
				catch (exc) {
					echo 'Something failed, I should sound the klaxons!'
					throw
				}
        }
		
    }
}
