pipeline{
 agent any
  stages{
    stage('Build'){
      steps{
       echo "echo Building ${BRANCH_NAME}..."
       sh "mvn clean install -DskipTests=true"
       }
      }
   
  }   
 }  
      
      
      
      
      
      
      
      
 