def jobName = JOB_NAME
def projectName = jobName.split('/')[0]
pipeline{
    agent any
    stages{
        stage('Checkout'){
            steps{
                 echo  "Build: ${projectName} for branch ${BRANCH_NAME}"
                 git(	
                 url: "https://https://sourcecode.jnj.com/.../....git",
				 credentialsId: '', // Pass Bitbucket Id by adding them in Jenkins credentials
				 branch: "${BRANCH_NAME}"				 
				)
			bat 'git clean -f'		//Remove untracked files from the working tree
			bat 'git reset --hard'  // resets after removing the untracked files
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
        stage('SonarQube'){
            steps{
                 echo "echo SonarQube ${BRANCH_NAME}..."
                 withSonarQubeEnv("${SonarQubeID}") {
                 bat "mvn sonar:sonar -DskipTests=true -Dsonar.projectName=${sonar_projectname} -Dsonar.projectDescription=${sonar_projectdescription} -Dsonar.branch.name=${git_branchname} -Dsonar.branch.target=${git_branchname}"
                }
            }    
        }
        stage('Deploy'){
         steps{
             echo "echo Deploying to ${BRANCH_NAME}..."
           }   
        }
    }
}

     
 