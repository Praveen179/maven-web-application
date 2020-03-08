node
{
     def mavenHome = tool name: "maven 3.6.3"
    
  stage('CheckOutCode') 
  {
    git branch: 'development', credentialsId: '04101c77-a43d-4e4e-bc83-0335455aabab', url: 'https://github.com/Praveen179/maven-web-application.git'
  }
   

  stage('Build')
   {
   sh "${mavenHome}/bin/mvn clean package"
   }
   
   stage('ExecuteSonarQubeReport')
    {
     sh "${mavenHome}/bin/mvn sonar:sonar"
    }
	
    stage('UploadArtifactIntoNexus')
     {
      sh "${mavenHome}/bin/mvn deploy"
     }
   
   stage('DeployAppIntoTomcat')
   {
    sshagent(['4961b912-cad5-4da0-a7f1-36175a062694'])
   {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.126.67.143:/opt/apache-tomcat-9.0.31/webapps/" 
   }
   }
    stage('SendEmailNotification')
   {
   emailext body: '''hi divya 
    happy birthday in advance''', subject: 'build status', to: 'divyava27@gmail.com'
   }
    
}
