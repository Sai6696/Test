def projectName = 'Test'
pipeline{
    agent any
    stages{
        stage('Checkout'){
            steps{
                 echo  "Build: ${projectName} for branch ${BRANCH_NAME}"
                 git(	
                 url: "https://github.com/Sai6696/Test.git",
				 credentialsId: 'Github',
				 branch: "${BRANCH_NAME}"				 
				)
			bat 'git clean -f'		
			bat 'git reset --hard'
			bat 'git checkout .'
                 
            }
        }
    stage('Build'){
      steps{
       echo "echo Building ${BRANCH_NAME}..."
       echo"{JOB_NAME}......."
       bat "mvn clean install -DskipTests=true"
       }
      }
    stage('Test'){
     steps{
       echo "echo Testing ${BRANCH_NAME}..."
       bat "mvn clean test"
       }
      }
  }   
 }  
      
      
      
      
      
      
      
      
 