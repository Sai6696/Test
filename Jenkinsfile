def application ='mule-test-teja'
pipeline{
agent any
    stages{
        stage('Checkout'){
            steps{
             echo  "Build: ${projectName} for branch ${BRANCH_NAME}"
             bat 'git clean -f'		             
             bat 'git reset --hard'               
             bat 'git checkout .'              
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
            when{
               ${BRANCH_NAME} == 'develop' 
            }
         steps{
             echo "echo Deploying to ${BRANCH_NAME}..."
             bat "mvn clean deploy -Denvironment=DEV -Dapplication=${application}-md -DmuleDeploy "
            }  
             when{
               ${BRANCH_NAME} == 'QA' 
            }
         steps{
             echo "echo Deploying to ${BRANCH_NAME}..."
             bat "mvn clean deploy -Denvironment=QA -Dapplication=${application}-qa -DmuleDeploy "
            } 
        }
    }

}

     
 
