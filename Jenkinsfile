pipeline {
  agent any
  stages {
    stage('Initialize'){
      def dockerHome = tool 'myDocker'
      env.PATH = "${dockerHome}/bin:${env.PATH}"
    }
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
        echo 'deploying to target'
      }
    }

  }
}