pipeline {
	agent any
	
	tools {
		jdk "11.0.1"
		maven "3.8.3"
	}
	
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