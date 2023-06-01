pipeline
{
    agent any
    stages
    
    {
        stage('ContDownload')
        {
         steps
         {
             git 'https://github.com/intelliqittrainings/maven.git'
         }   
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
                sh 'scp /var/lib/jenkins/workspace/DeclarativePipelinemanual/webapp/target/webapp.war ubuntu@172.31.16.182:/var/lib/tomcat9/webapps/testapp.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipelinemanual/testing.jar'
            }
        }
    }
    post
    {
        success
        {
            input message: 'waiting for approval from DM!', submitter: 'srinivas'
            
            sh 'scp /var/lib/jenkins/workspace/DeclarativePipelinemanual/webapp/target/webapp.war ubuntu@172.31.23.167:/var/lib/tomcat9/webapps/prodapp.war'
        }
        failure
        {
          mail bcc: '', body: 'jenkins cd stage failed', cc: '', from: '', replyTo: '', subject: 'cd failed', to: 'koppada.parasuk@gmail.com'  
        }
    }
}
