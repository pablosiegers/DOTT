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
				sh 'cd cidr_convert_api'
				sh 'pwd'
                sh 'npm install'
            }
        }
        stage ('Test') {
            steps {
                sh 'npm test'
            }
        }
		stage('Three') {
				when {
				    expression{env.EXECUTE}
                }
				steps {
					sh 'echo "Executing third sstage because the value of the environment variable is: ${EXECUTE}"'
				}
		}
    }
}
