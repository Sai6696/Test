def jobName = JOB_NAME
def projectName = jobName.split('/')[0]
pipeline{
    agent any
    stages{
        stage('Deploy'){
         steps{
             echo "Deploying to ${BRANCH_NAME}..."
           }  
        }
    }
}

     
 