pipeline {
	agent any
    environment {
        EXECUTE = 'true'
    }
		stages {
			stage('One') {
				steps {
					sh 'echo "First Stage"'
				}
			}

			stage('Two') {
				when {
                    expression{env.EXECUTE}
               	}
                steps {
					sh 'echo "Updating Second Stage, environment variable value:"'
                    sh 'echo ${EXECUTE}'
				}
			} 

			stage('Three') {
				when {
				    expression{!env.EXECUTE}
                }
				steps {
					sh 'echo "Executing third sstage because the value of the environment variable is: ${EXECUTE}"'
				}
			}
		}
}
