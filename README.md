"# mule-cicd-sample" 

Command to deploy :
mvn clean package deploy -DmuleDeploy  -Danypoint.username=<<username>> -Danypoint.password=<<password>>
  
mvn clean package deploy -DmuleDeploy  -DmuleVersion=4.3.0 -Dusername=<<username>> -Dpassword=<<password>>
provide the anypoint usrname and password
