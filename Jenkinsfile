def jobName = JOB_NAME
def projectName = jobName.split('/')[0]
pipeline{
    agent any
    stages{
     stage('Deploy'){
         steps{
             echo "echo Deploying to ${BRANCH_NAME}..."
             bat "mvn clean deploy -DmuleDeploy"
        }
      }
  }   
 }  
      
      
      
      
      
      
      
      
 