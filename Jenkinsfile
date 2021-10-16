pipeline {
	agent any
	

	
	stages {
	

		
		stage('Build') {
			steps {
            	echo 'Application is in Building Phase'
            	sh 'mvn --version'
                sh 'mvn clean install'
            }
        }
        
        stage('Test') {
        	steps {
            	echo 'Application is in Testing Phase'
                sh 'mvn test'
            }
        }
        
        
        stage('SonarQube analysis') {
        	environment {
        		scannarhome = tool 'sonarqube-scannar'
        	}
        
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh "mvn clean package sonar:sonar"
                }
            }
        }
      stage("Quality Gate"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
      }
        
        
        stage('Deploy to Cloudhub') { 
        	environment {
            	ANYPOINT_CREDENTIALS = credentials('platform.credentials')
            }
            steps {
            	sh 'mvn package deploy -DmuleDeploy -DmuleVersion=4.4.0 -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -DworkerType=MICRO -Dworkers=1'
            }
         }
	}
	
	post {
		always {
			cleanWs()
		}
	}
}