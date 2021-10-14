pipeline {
     agent any
         stages {
             stage('Build') {
                 steps {                   
                  withMaven(maven: 'mvn') {
                    echo 'Application is in Building Phase'
                  	sh "mvn clean package"
                  }
                 }
            
			}
		}
}