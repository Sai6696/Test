def projectName = 'Test'
pipeline{
    agent any
    stages{
        stage('Checkout'){
            steps{
                 echo  "Build:  + ${projectName} +  for branch + env.BRANCH_NAME"
            }
        }
    stage('Build'){
      steps{
       echo "echo Building ${BRANCH_NAME}..."
       bat "mvn clean install -DskipTests=true"
       }
      }
    stage('Test'){
     steps{
       echo "echo Testing ${BRANCH_NAME}..."
       bat "mvn clean test"
       }
      }
    stage('Deploy'){
     steps{
       echo "echo Deploying to ${BRANCH_NAME}..."
       bat "mvn clean deploy -DmuleDeploy"
       }
     }
  }   
 }  
      
      
      
      
      
      
      
      
 