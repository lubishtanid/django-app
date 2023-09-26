pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('DockerHub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t lubishtanid/jenkins-testing .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push lubishtanid/jenkins-testing'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}