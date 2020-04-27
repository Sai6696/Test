def jobName = JOB_NAME
def projectName = jobName.split('/')[0]
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
    if(env.BRANCH_NAME == 'develop')
      	{
		steps{
       		echo "echo Building ${BRANCH_NAME}..."
       		bat "mvn clean install -DskipTests=true"
       }
       }else if(env.BRANCH_NAME == 'qa')
       {
       steps{
        echo "echo Building ${BRANCH_NAME}..."
        }
        }
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
      
      
      
      
      
      
      
      
 