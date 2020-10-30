pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'building docker image'
        script {
          sh 'docker build -t itspotorg/nginx-test:latest .'
        }
      }
    }
    stage('push to repo') {
      steps {
        echo 'Loggin in to dockerhub'
        withCredentials([string(credentialsId: 'dockerhub-pass', variable: 'dockerhubPassword'), string(credentialsId: 'dockerhub-username', variable: 'dockerhubUsername')]) {
          sh 'docker login -u ${dockerhubUsername} -p ${dockerhubPassword}'
        }
        echo 'Pushing image to dockerhub'
        sh 'docker push itspotorg/nginx-test:latest'
      }
    }
    stage('deploy') {
      steps {
        def deployCommand = 'touch ~/i-work.txt'
        echo 'starting deployment'
        echo 'constructig deploy command'
        echo 'Executing command on remote'
        sshagent(['nginx-test-prod']) {
          sh "ssh -o StrictHostKeyChecking=no ubuntu@ec2-18-130-53-186.eu-west-2.compute.amazonaws.com ${deployCommand}"
        }
      }
    }
    stage('cleanup') {
      steps {
        echo 'cleaning up ...'
        sh 'docker image rm itspotorg/nginx-test:latest'
      }
    }
  }
}