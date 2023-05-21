pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhubCredential')
  }
  stages {
    stage('Build') {
      steps {
        bat 'docker build -t efkay73/jenkins-docker-hub .'
      }
    }
    stage('Login') {
      steps {
	bat 'echo %DOCKERHUB_CREDENTIALS_USR%'
        bat 'echo %DOCKERHUB_CREDENTIALS_PSW% | docker login -u %DOCKERHUB_CREDENTIALS_USR% --password-stdin'
      }
    }
    stage('Push') {
      steps {
        bat 'docker push efkay73/jenkins-docker-hub'
      }
    }
  }
  post {
    always {
      bat 'docker logout'
    }
  }
}