node
{
    def mvnhome = tool name: 'maven3.8.3', type: 'maven'
    stage('CheckoutCode')
    {
        git credentialsId: '87ca2fc4-0d24-4cb0-a135-389c89c09bd3', url: 'https://github.com/MithunTechnologiesProjects/maven-web-application.git'
        
    }
   stage('Build')
   {
     sh "${mvnhome}/bin/mvn clean package"
    
    }
   stage ('DeployingIntoTomcat')
    {
     sshagent(['714cebc4-68b3-4eaa-be46-316b0c3d4336']) 
     {
        sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@34.207.69.229:/opt/apache-tomcat-9.0.54/webapps/"      
     }
    }    
   stage('Sendingmail')
    {
        mail bcc: '', body: '''Hello there,

Build is completed''', cc: '', from: '', replyTo: '', subject: 'Build Job Is Completed', to: 'dbramayanam@gmail.com' 
    }
}
