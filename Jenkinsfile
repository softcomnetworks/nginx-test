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
          withCredentials([string(credentialsId: 'dockerhub-pass', variable: 'docker-pass'), string(credentialsId: 'dockerhub-pass', variable: 'docker-username')]) {
            sh 'docker login -u ${docker-username} -p ${docker-pass}'    
          }
      }
    }

  }
}