pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'building docker image'
        script {
          docker.build "itspotorg/nginx-test:latest"
        }
        echo 'pushing image to dockerhub'
      }
    }
    stage('deploy') {
      steps {
        echo 'Loggin in to dockerhub'
        withCredentials([string(credentialsId: 'dockerhub-pass', variable: 'dockerhubPassword')]) {
          sh 'docker login -u sweptwings -p ${dockerhubPassword}'
        }
      }
    }

  }
}