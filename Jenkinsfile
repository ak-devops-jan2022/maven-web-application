node{
    
    def mavenHome = tool name: "maven3.8.4"
    
   stage('CheckoutCode') {
       git branch: 'development', url: 'https://github.com/ak-devops-jan2022/maven-web-application.git'
   }
   
   stage('Build'){
       sh "${mavenHome}/bin/mvn clean package"
   }
   
   stage('ExecuteSonarQubeReport'){
       sh "${mavenHome}/bin/mvn sonar:sonar"
   }
   
   stage('UploadArtifactintoNexusRepo'){
       sh "${mavenHome}/bin/mvn deploy"
   }
  
  stage('DeploytoTomcat'){
      sshagent(['128e2ef4-f24b-410d-9630-e49c2963c77b']) {
       sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@54.161.251.71://opt/apache-tomcat-9.0.58/webapps/"
  }
}
     
}
