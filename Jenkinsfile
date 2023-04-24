node
{
    def mavenHome = tool name: "maven-3.9.1"
    
    stage('CheckoutCode')
    {
    git branch: 'development', credentialsId: '5160036a-6448-4111-831a-c11cf9b3922d', url: 'https://github.com/gidellc/maven-web-application.git'    
    }
    
    stage('Build')
    {
    sh "${mavenHome}/bin/mvn clean package"
    }
    
     stage('ExecuteSonarQubeReport')
    {
    sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    
    stage('UploadArtifactintoNexus')
    {
    sh "${mavenHome}/bin/mvn deploy"
    }
    
     stage('DeployAppToTomcat')
    {
         
     sshagent (['b804a5c2-1d57-4fe9-b7e0-d362c1037501'])
    {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war  tomcat@10.0.0.183:/opt/apache-tomcat-9.0.73/webapps/"
    }
    
    }
    /*
    stage('SendEmailNotification')
    {
     mail bcc: '', body: '''pipeline infos
     Regards''', cc: 'nkanyou123@yahoo.com', from: '', replyTo: '', subject: 'pipeline alert', to: 'gidengnepi2016@gmail.com'
    }
    
    */
}
