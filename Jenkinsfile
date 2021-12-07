pipeline
{
  agent any
  stages
  {
    stage('ContiniousDownload_Loan')
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
    stage('ContiniousBuild_Loan')
    {
      steps
      {
         sh 'mvn package'
      }
    }
  }
 }   
