pipeline {
	agent any
	

	
	stages {
	
		
		
		stage('Build') {
			steps {
            	echo 'Application is in Building Phase'
            	bat 'mvn --version'
                bat 'mvn clean install'
            }
        }
        
        stage('Test') {
        	steps {
            	echo 'Application is in Testing Phase'
                bat 'mvn test'
            }
        }
        
        stage('Sonarqube') {
			environment {
				scannerHome = tool 'SonarQubeScanner'
			}
		
			steps {
				withSonarQubeEnv('sonarqube') {
					bat "${scannerHome}/bin/sonar-scanner"
					echo "**************************************"
				}
				timeout(time: 10, unit: 'MINUTES') {
					waitForQualityGate abortPipeline: true
				}
				
			}
				
    }

            
        
        stage('Deploy to Cloudhub') { 
        	environment {
            	ANYPOINT_CREDENTIALS = credentials('anypoint.credentials')
            }
            steps {
            	bat 'mvn package deploy -DmuleDeploy -DmuleVersion=4.4.0 -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -DworkerType=MICRO -Dworkers=1'
            }
         }
	}
	
	post {
		always {
			cleanWs()
		}
	}
}