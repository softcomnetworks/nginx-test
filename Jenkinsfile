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
        echo 'starting deployment'
        sshagent(['nginx-test-prod']) {
          sh "ssh -o StrictHostKeyChecking=no ubuntu@ec2-18-130-53-186.eu-west-2.compute.amazonaws.com docker rm --force nginx-test-app"
          sh "ssh -o StrictHostKeyChecking=no ubuntu@ec2-18-130-53-186.eu-west-2.compute.amazonaws.com docker pull itspotorg/nginx-test:latest"
          sh "ssh -o StrictHostKeyChecking=no ubuntu@ec2-18-130-53-186.eu-west-2.compute.amazonaws.com docker run -d -p 80:80 --name nginx-test-app itspotorg/nginx-test:latest"
        }
      }
    }
    stage('cleanup') {
      steps {
        echo 'cleaning up ...'
        echo 'removing remote dangling images'
        sshagent(['nginx-test-prod']) {
          sh "ssh -o StrictHostKeyChecking=no ubuntu@ec2-18-130-53-186.eu-west-2.compute.amazonaws.com docker rmi -f $(docker images -f 'dangling=true' -q)"
        }
        echo 'removing local build image'
        sh 'docker image rm itspotorg/nginx-test:latest'
      }
    }
  }
}