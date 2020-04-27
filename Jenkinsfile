node{
	def jobName = JOB_NAME
	def projectName = jobName.split('/')[0]
try{
	stage('Checkout'){
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
	stage('Build'){
          
                 echo "echo Building ${BRANCH_NAME}..."
				 bat "mvn clean install -DskipTests=true"
        }
	stage('Test'){
                 echo "echo Testing ${BRANCH_NAME}..."
                 bat "mvn clean test"
        }
	stage('Deploy'){
             echo "echo Deploying to ${BRANCH_NAME}..."
             bat "mvn clean deploy -DmuleDeploy"
		}
    } catch(Exception e){
             echo "Build Failed: ${e}"
    }
}