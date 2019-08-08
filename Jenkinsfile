
def isMaster = env.BRANCH_NAME == 'master'
def isDevelop = env.BRANCH_NAME == 'staging'
GITSHA = sh(returnStdout: true, script: 'git rev-parse --short HEAD')

pipeline {
  agent any
  environment {
    registry = "sohel2020/jenkins-test"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }

  stages {
    stage('Cloning Git') {
      steps {
	    checkout scm
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build("${registry}:${env.BRANCH_NAME}-${GITSHA}")
        }
      }
    }
    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BRANCH_NAME-$GITSHA"
      }
    }
    }
}
