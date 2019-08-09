 #node {
#	 stage("git checkout"){
#		checkout scm
#	 }
#	 stage("Print something"){
#		sh "pwd"
#	 }
# }
pipeline {
	agent { 
		docker { image 'node:7-alpine' } 
	}
	stages {
		stage('scm checkout') {
			steps	{
				scm checkout
			}
		}
		stage('check node version') {
			steps {
				sh 'node --version'
			}
	}
}
}
