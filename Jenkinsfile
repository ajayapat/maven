pipeline
{
  agent any
  stages
  {
    stage('ContiniousDownload_Master')
    {
      steps
      {
          script{
              try{
                  git 'https://github.com/intelliqittrainings/maven.git' 
              }
              catch(Exception e1){
                  mail bcc: '', body: 'jenkin is unbale download dev code from git repo', cc: '', from: '', replyTo: '', subject: 'Download failed', to: 'git.team@gmail.com'
                  exit(1)
              }
          }
        
      }
    }
    stage('ContiniousBuild_Master')
    {
      steps
      {
         sh 'mvn package'
      }
    }
    stage('ContiniousDeployment_Master')
    {
      steps
      {
         deploy adapters: [tomcat9(credentialsId: 'e872fcda-b798-41a4-b2ea-ff2f7e9574b0', path: '', url: 'http://10.0.0.113:8080')], contextPath: 'testapp', war: '**/*.war'
      }
    }
    stage('ContiniousTesting_Master')
    {
      steps
      {
         git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
         sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline/testing.jar'
         
      }
    }
     stage('ContiniousDelivery_Master')
    {
      steps
      {
          input message: 'Need Approval from DM!', submitter: 'srinivas'
         deploy adapters: [tomcat9(credentialsId: 'e872fcda-b798-41a4-b2ea-ff2f7e9574b0', path: '', url: 'http://10.0.0.119:8080')], contextPath: 'prodapp', war: '**/*.war'
         
      }
    }
  }   
}
