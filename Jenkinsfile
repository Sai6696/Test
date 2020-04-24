node{
      stage ('Checkout') {
			println "Build: " + projectName + " for branch " + env.BRANCH_NAME
			git(
				url: "https://https://sourcecode.jnj.com/${projectName}.git",
				branch: env.BRANCH_NAME,
                credentialsId: ''
			)		
			sh 'git clean -f'
			sh 'git reset --hard'
			sh 'git checkout .'
		}   
    stage('Build'){
        try{
               sh "mvn clean install -DskipTests=true"
           }
            catch(Exception e){
                echo "Build Failed: ${e}"
            }
        }
    stage('Test'){
        try{
                sh "mvn test"
           }
            catch(Exception e){
                echo "Test Failed: ${e}"
            }
        }
    stage('SonarQube'){
        try {
                withSonarQubeEnv("${SonarQubeID}") {
                sh "mvn sonar:sonar -DskipTests=true -Dsonar.projectName=${sonar_projectname} -Dsonar.projectDescription=${sonar_projectdescription} -Dsonar.branch.name=${git_branchname} -Dsonar.branch.target=${git_branchname}"
                }
            }catch (Exception e) {
                    echo "SonarQube Analysis failed: ${e}"
                }
            }
    stage ('Deploy') {
        if (fileExists("${projectName}")) {
            if (env.BRANCH_NAME=='Develop') {
                echo 'build Develop'
                withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] ){
                    echo "${tool mvn_version}"
                    def pom = readMavenPom file: "${projectName}/pom.xml"
                    def versionList = pom.version.replace("-SNAPSHOT", "").tokenize(".")
                    version = "${versionList[0]}.${versionList[1]}.${versionList[2]}"
                    group = pom.groupId.replace(".", "/")
                    echo "${group}"
                    sh "mvn deploy -Dusername=${username} -Dpassword=${password} -Dapplicationname=${Dapplicationname} -Denvironment=${params.deploy_environment}"                    
                }
            }
        }
    }
    }
}

    
    
