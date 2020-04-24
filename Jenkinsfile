Pipeline{
    agent any
    parameters { 
        string(name: 'deploy_environment', defaultValue: 'DEV', description: 'Application deployment environment') 
    }
    stages{
        stage('Build'){
            steps{
                script{
                    try{
                        sh "mvn clean install -DskipTests=true"
                    }
                    catch(Exception e){
                        echo "Build Failed: ${e}"
                    }
                }
            }
        }
        stage('Test'){
            steps{
                script{
                    try{
                        sh "mvn test"
                    }
                    catch(Exception e){
                        echo "Test Failed: ${e}"
                    }
                }
            }
        }
        stage('SonarQube'){
            steps{
                script{
                    try {
                        withSonarQubeEnv("${SonarQubeID}") {
                            sh "mvn sonar:sonar -DskipTests=true -Dsonar.projectName=${sonar_projectname} -Dsonar.projectDescription=${sonar_projectdescription} -Dsonar.branch.name=${git_branchname} -Dsonar.branch.target=${git_branchname}"
                        }
                    } catch (Exception e) {
                        echo "SonarQube Analysis failed: ${e}"
                    }
                }
            }
        }
        stage('Deploy'){
            steps{
                script{
                    try{
                            sh "mvn clean package deploy -DmuleDeploy -Dusername=${username} -Dpassword=${password} -Dapplicationname=${Dapplicationname} -Denvironment=${params.deploy_environment}"
                        }
                        catch (Exception e) {
                            echo "${params.deploy_environment} Deployemnt failed: ${e}"
                    }
                }
            }
        }      
    } 
}      