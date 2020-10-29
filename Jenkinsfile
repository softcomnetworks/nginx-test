pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'building docker image'
        script {
          sh 'docker build -t itspotorg/nginx-test:latest .'
        }
        echo 'pushing image to dockerhub'
      }
    }
    stage('deploy') {
      steps {
        echo 'Loggin in to dockerhub'
        withCredentials([string(credentialsId: 'dockerhub-pass', variable: 'dockerhubPassword'), string(credentialsId: 'dockerhub-username', variable: 'dockerhubUsername')]) {
          sh 'docker login -u ${dockerhubUsername} -p ${dockerhubPassword}'
        }
        
        echo 'Pushing image to dockerhub'
        sh 'docker push itspotorg/nginx-test:lates'
      }
    }

  }
}