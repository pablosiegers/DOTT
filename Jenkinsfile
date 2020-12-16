pipeline {
    agent any
    environment {
        EXECUTE = 'true'
    }
    tools {nodejs "node"}
    stages {
        stage('Cloning Git 3') {
            steps {
                git 'https://github.com/pablosiegers/DOTT'
            }
        }
        stage('Install Dependencies'){
            steps {
                sh 'echo "Hola"'
                sh 'npm install'
            }
        }
		stage('SonarQube') {
				when {
				    expression{!env.EXECUTE}
                }
				steps {
					sh 'echo "SonarQube Stage"'
				}
		}
        stage ('Test') {
				when {
				    expression{env.EXECUTE}
                }
				steps {
					sh 'npm test -- ipv4validation.js'
					sh 'npm test'
				}
        }
		
    }
}
