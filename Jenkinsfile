pipeline{
 agent any
  stages{
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
       bat "mvn clean package deploy -DmuleDeploy"
       }
      }
  }   
 }  
      
      
      
      
      
      
      
      
 