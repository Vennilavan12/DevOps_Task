pipeline {
  agent any 
   environment {
    dockerImage=''
    DOCKERHUB_CREDENTIALS = 'docker'
    registry="vennilavan/devopstask"
  } 
  stages {
    stage ('Checkout') {
      steps { 
        checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Vennilavan12/DevOps_Task.git']])
        echo "Checkoutdone"
      }
    }
    stage ('Build') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage ('Push Image to Dockerhub') {
      steps {  
        script {
          docker.withRegistry('', DOCKERHUB_CREDENTIALS ) {
            dockerImage.push("latest")
          }
        } 
      }
    }
  }
}
