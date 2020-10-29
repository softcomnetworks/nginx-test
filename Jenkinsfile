pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'building docker image'
        script {
          // sh 'docker build -t itspotorg/nginx-test:latest .'
          docker.build "itspotorg/nginx-test:latest"
        }
        echo 'pushing image to dockerhub'
      }
    }
    stage('deploy') {
      steps {
        echo 'deploying to target'
      }
    }

  }
}