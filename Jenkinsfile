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
                            sh 'mvn package deploy -DmuleDeploy -DmuleVersion=4.3.0 -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -DworkerType=MICRO -Dworkers=1 -Dregion=us-west-2'
                         }
                    }
         }
     }