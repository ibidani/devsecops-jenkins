pipeline {
  agent any
  tools { 
        maven 'Maven_3_8_7'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn -ntp clean verify sonar:sonar -Dsonar.projectKey=initializ-buggyapp_bugapp -Dsonar.organization=initializ-buggyapp -Dsonar.host.url=https://sonarcloud.io'
			}
    }

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}
