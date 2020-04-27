node{
	def jobName = JOB_NAME
	def projectName = jobName.split('/')[0]
try{
	stage('Deploy'){
             echo "echo Deploying to ${BRANCH_NAME}..."
             bat "mvn deploy -DmuleDeploy"
		}
    } catch(Exception e){
             echo "Build Failed: ${e}"
    }
}