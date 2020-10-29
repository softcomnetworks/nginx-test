pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'building docker image'
        // sh 'docker build -t itspotorg/nginx-test:latest .'
        docker build -t itspotorg/nginx-test:latest .
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