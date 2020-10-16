pipeline {
  agent {
    node {
      label 'base'
    }

  }
  stages {
    stage('build and tag image') {
      steps {
        container('base') {
          sh '''docker build -t denticle/builder-go .
docker tag denticle/builder-go denticle/builder-go'''
        }

      }
    }
    stage('docker push') {
      when{
        branch 'master'
      }
      steps {
        container('base') {
          withCredentials([usernamePassword(passwordVariable : 'DOCKER_PASSWORD' ,usernameVariable : 'DOCKER_USERNAME' ,credentialsId : 'dockerhub-id' ,)]) {
            sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'
          }
            sh 'docker push denticle/builder-go'
        }
      }
    }
  }
}
