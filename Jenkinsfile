pipeline{
 agent any
  stages{
    stage('Build'){
      steps{
       echo "echo Building ${BRANCH_NAME}..."
       bat "mvn clean install -DskipTests=true"
       }
      }
   
  }   
 }  
      
      
      
      
      
      
      
      
 